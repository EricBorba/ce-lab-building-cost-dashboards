# CLI Commands — Lab M7.09: Building Cost Dashboards

All commands executed successfully, in chronological order.

---

## Step 1: Verify Billing Metrics

```bash
aws cloudwatch list-metrics \
  --namespace "AWS/Billing" \
  --metric-name "EstimatedCharges" \
  --region us-east-1
```

---

## Step 2: Discover Cost Alarms

```bash
aws cloudwatch describe-alarms \
  --alarm-name-prefix "Cost" \
  --query "MetricAlarms[].AlarmArn" \
  --output json \
  --region us-east-1
```

```bash
aws cloudwatch describe-alarms \
  --query "MetricAlarms[].{Name:AlarmName,Arn:AlarmArn}" \
  --output table \
  --region us-east-1
```

---

## Step 3: Deploy Engineering Cost Dashboard

```bash
aws cloudwatch put-dashboard \
  --dashboard-name EngineeringCostDashboard \
  --dashboard-body file://dashboards/engineering-cost-dashboard.json \
  --region us-east-1
```

```bash
aws cloudwatch list-dashboards --region us-east-1
```

---

## Step 4: Deploy Executive Summary Dashboard

```bash
aws cloudwatch put-dashboard \
  --dashboard-name ExecutiveCostSummary \
  --dashboard-body file://dashboards/executive-summary-dashboard.json \
  --region us-east-1
```

```bash
aws cloudwatch list-dashboards --region us-east-1
```

---

## Step 5: Rename Screenshots

```bash
cd screenshots && \
mv "Screenshot 2026-06-08 at 09.25.49.png" "billing-metrics-verification.png" && \
mv "Screenshot 2026-06-08 at 09.32.18.png" "alarm-arns-discovery.png" && \
mv "Screenshot 2026-06-08 at 09.32.43.png" "engineering-dashboard-deploy.png" && \
mv "Screenshot 2026-06-08 at 09.33.06.png" "engineering-dashboard-verified.png" && \
mv "Screenshot 2026-06-08 at 09.35.10.png" "executive-dashboard-deploy.png" && \
mv "Screenshot 2026-06-08 at 09.35.50.png" "both-dashboards-listed.png" && \
mv "Screenshot 2026-06-08 at 09.44.50.png" "engineering-dashboard.png" && \
mv "Screenshot 2026-06-08 at 09.45.13.png" "executive-dashboard.png"
```

---

## Step 6: Git & GitHub

```bash
git init
git add .
git commit -m "Complete lab M7.09: Building Cost Dashboards"
```

```bash
gh repo create ce-lab-building-cost-dashboards \
  --public \
  --description "AWS CloudWatch cost dashboards — Engineering and Executive dashboards with billing metrics, budget utilization, and alarm status deployed via CLI." \
  --source /Users/ericborba/Documents/Projetos/cloud-engineering/lab62/ce-lab \
  --push \
  --remote origin
```

```bash
gh repo edit EricBorba/ce-lab-building-cost-dashboards \
  --add-topic aws \
  --add-topic cloudwatch \
  --add-topic finops \
  --add-topic cost-optimization \
  --add-topic aws-billing \
  --add-topic dashboards \
  --add-topic aws-cli \
  --add-topic cloud-engineering
```
