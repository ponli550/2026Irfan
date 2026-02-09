---
name: Deploy chkSupabase
description: "Local with k8s"
grade: Grade
tags: [tag1, tag2]
pros:
  - "Easy"
cons:
  - "Technical"
---

# Deploy chkSupabase

## Best Practice
(Describe the best practice pattern here)

## Snippet
'<!-- jcapy:EXEC -->
```bash
kubectl get pods -l app=a-deployment
```
<!-- jcapy:EXEC -->
```bash
supabase link
supabase migration list
kubectl get service a-service
supabase status
echo "run kubectl get pods --all-namespaces"
echo "kubectl describe deployment a-deployment"
echo "supabase link --project-ref <your-project-id>"
echo "supabase db remote commit"
```

