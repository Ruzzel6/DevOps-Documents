
To Check the cost:

aws ce get-cost-and-usage --time-period Start=$(date -d '7 days ago' +%Y-%m-%d),End=$(date +%Y-%m-%d) --granularity DAILY --metrics BlendedCost --region us-west-2
```
Better way to verify actual current costs — check unblended cost + forecast

aws ce get-cost-forecast \
  --time-period Start=$(date +%Y-%m-%d),End=$(date -d '+7 days' +%Y-%m-%d) \
  --metric BLENDED_COST \
  --granularity DAILY
```
aws eks list-clusters --region us-west-2
aws ec2 describe-instances --region us-west-2 --filters "Name=instance-state-name,Values=running" --query "Reservations[].Instances[].{ID:InstanceId,Type:InstanceType,LaunchTime:LaunchTime}"
aws ec2 describe-nat-gateways --region us-west-2 --filter "Name=state,Values=available" --query "NatGateways[].{ID:NatGatewayId,State:State}"
