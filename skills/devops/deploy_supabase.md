---
name: Deploy supabase
description: "installations"
grade: B
tags: [tag1, tag2]
pros:
  - "easy"
cons:
  - "technical"
---

# Deploy supabase

## Best Practice
(Describe the best practice pattern here)

## Snippet
<!-- JAAVIS:EXEC -->
```bash
brew install supabase/tap/supabase
supabase init
supabase login
supabase start

```
brew upgrade supabase
supabase db diff -f my_schema
supabase db dump --local --data-only > supabase/seed.sql
supabase stop --no-backup
supabase stop
supabase login
supabase status
