---
tags: [tag1, tag2]
grade: A DEMO DEPLOY
---

# Deploy Demo Deploy

> y

## Pros
  - "B"

## Cons
  - "Simple"
  - "Fast"

## Implementation
<!-- jcapy:EXEC -->
```bash
No scaling
#!/bin/bash
echo "Deploying demo application..."
docker build -t demo-app .
docker run -d -p 8080:80 demo-app
echo "Deployment complete."
```
        