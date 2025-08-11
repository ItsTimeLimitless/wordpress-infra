WordPress on AWS using CloudFormation, ECS Fargate, RDS, EFS, and Jenkins CI/CD. Prod is always on; Dev auto-pauses outside 9 AM–6 PM ET.

WordPress on AWS using CloudFormation (VPC, ECS Fargate, RDS, EFS), plus Jenkins CI/CD.
Repo structure:
infra/: CloudFormation templates (network.yaml, data.yaml, app.yaml, schedules.yaml)
app/: Dockerfile and wp-config.php
jenkins/: Jenkinsfile and pipeline docs
docs/: diagrams and runbooks
Branches:
main: stable
prod: release
dev: active development
