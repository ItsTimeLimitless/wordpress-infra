# Network
aws cloudformation deploy \
  --stack-name dev-wp-network \
  --template-file infra/network.yaml \
  --parameter-overrides EnvName=dev \
  --capabilities CAPABILITY_NAMED_IAM

# Data
aws cloudformation deploy \
  --stack-name dev-wp-data \
  --template-file infra/data.yaml \
  --parameter-overrides EnvName=dev \
  --capabilities CAPABILITY_NAMED_IAM

# App (example ImageTag; adjust as needed)
aws cloudformation deploy \
  --stack-name dev-wp-app \
  --template-file infra/app.yaml \
  --parameter-overrides EnvName=dev ImageTag=latest DesiredCount=1 \
  --capabilities CAPABILITY_NAMED_IAM

# Schedules (dev only; substitute your cluster/service from app outputs)
aws cloudformation deploy \
  --stack-name dev-wp-schedules \
  --template-file infra/schedules.yaml \
  --parameter-overrides ClusterNameParam=dev-wp-cluster ServiceNameParam=dev-wp-service \
  --capabilities CAPABILITY_NAMED_IAM