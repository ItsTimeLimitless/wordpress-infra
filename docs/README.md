### Documentation

This folder contains architecture diagrams, runbooks, and operational notes for the WordPress on AWS project.

#### Architecture blueprint
- Diagram (blueprint style): https://cdn.abacus.ai/images/be578ca6-4116-44ee-bcb1-69575371adab.png
- High-level flow: Users → Route 53 → ALB → ECS (WordPress) → RDS (MySQL) and EFS (wp-content).  
  Dev service scales to 0 outside business hours via EventBridge Scheduler. CloudWatch handles logs, metrics, alarms. Jenkins builds/pushes Docker image to ECR and deploys CloudFormation stacks.

#### Runbooks
- Initial setup:
  1) Deploy network stack, then data (RDS), then app (ECS/ALB), then schedules (dev only).
  2) Complete WordPress installer via the ALB DNS.
- Routine operations:
  1) CI/CD via Jenkins: build image, push to ECR, update stacks.
  2) Monitor CloudWatch alarms and Synthetics canary.
- Backup and restore:
  1) RDS automated backups and snapshots.
  2) EFS protected via AWS Backup (recommended).
- Security:
  1) HTTPS via ACM on ALB (prod), optional WAF.
  2) Secrets in Secrets Manager; least-privilege IAM roles.

#### File index
- network.yaml: VPC, subnets, IGW, NAT, EFS, security groups.
- data.yaml: RDS (MySQL) and Secrets Manager.
- app.yaml: ECR, ECS cluster/service, task definition, ALB, logs.
- schedules.yaml: EventBridge Scheduler rules for dev business hours.

#### TODO
- Add step-by-step screenshots for AWS Console deployments.
- Add canary script details and alarm thresholds.
- Document cost tips (NAT, Fargate, RDS sizing) and region notes.