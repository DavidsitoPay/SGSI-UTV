# SGSI-UTV AWS infrastructure (CloudFormation)

Account profile `utv`, region `us-east-2`. Every command uses `--profile utv`.

## 1. Stacks

| Order | Stack | Contents | Lifecycle |
|---|---|---|---|
| 1 | `utv-network` | VPC, subnets, route tables, security groups, NACLs, flow logs | Permanent |
| 2 | `utv-identity` | MFA-gated admin/auditor roles, EC2 and Backup roles | Permanent |
| 3 | `utv-operations` | CloudTrail, S3 trail bucket, 7 security alarms, SNS topic, Backup vault and plan, 2 budgets | Permanent |
| 4 | `utv-workload` | 1 EC2 t3.micro, 1 RDS PostgreSQL db.t4g.micro, their 2 alarms | On demand |

The account password policy is applied from `password-policy.json` (no CloudFormation resource exists for it).

## 2. First-time deploy

```
export MSYS_NO_PATHCONV=1; P="--profile utv --region us-east-2"; T="--tags Project=SGSI-UTV --no-fail-on-empty-changeset"
aws cloudformation deploy --stack-name utv-network    --template-file infra/aws/network.yaml    $T --capabilities CAPABILITY_IAM $P
aws cloudformation deploy --stack-name utv-identity   --template-file infra/aws/identity.yaml   $T --capabilities CAPABILITY_NAMED_IAM $P
aws cloudformation deploy --stack-name utv-operations --template-file infra/aws/operations.yaml $T --capabilities CAPABILITY_IAM $P --parameter-overrides AlertEmail=<your-email>
aws iam update-account-password-policy --cli-input-json file://infra/aws/password-policy.json --profile utv
```

## 3. Workload up

```
aws cloudformation deploy --stack-name utv-workload --template-file infra/aws/workload.yaml $T $P
```

## 4. Workload down

```
aws cloudformation delete-stack --stack-name utv-workload $P && aws cloudformation wait stack-delete-complete --stack-name utv-workload $P
```

## 5. Full teardown

1. Workload down (section 4).
2. List and delete recovery points: `aws backup list-recovery-points-by-backup-vault --backup-vault-name utv-backup-vault --query "RecoveryPoints[].RecoveryPointArn" --output text $P`, then `aws backup delete-recovery-point --backup-vault-name utv-backup-vault --recovery-point-arn <arn> $P` for each.
3. Empty the trail bucket: `aws s3 rm s3://utv-cloudtrail-<account>-us-east-2 --recursive --profile utv`.
4. Delete the stacks in order `utv-operations`, `utv-identity`, `utv-network`, waiting for each.
5. `aws iam delete-account-password-policy --profile utv`.

## 6. Manual steps

- Confirm the SNS subscription email sent by AWS after deploying `utv-operations`; alarms and budgets do not notify until it is confirmed.
- The web server uses a self-signed certificate; accept the browser warning.

## 7. Cost

- Permanent stacks have no public IPv4 address, RDS instance, NAT gateway or VPC endpoint.
- The workload is billed only while it is up.
- A stopped RDS instance restarts automatically after 7 days, so the workload is deleted and recreated instead of stopped.
- No final RDS snapshot is taken on delete because the database is empty.
