---
title: GitHub Command Referenced
---

## GitHub SSH Alias

Use a custom SSH alias so repositories automatically use Mars's GitHub SSH key instead of the default GitHub identity.

Example remote:

```bash
git remote set-url origin git@github-marsuvesvex:MarsuvesVex/<repo>.git
```

## Example SSH config:
```bash
Host github-marsuvesvex
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_mars
    IdentitiesOnly yes
```


## Add Github bulk tags

```bash
❯ topics=(
  golang
  go
  microservices
  template
  docker
  docker-compose
  nats
  event-driven
  postgres
  redis
  traefik
  nginx
  backend
  saas
  boilerplate
  architecture
  jetstream
  worker
  event-bus
  scaffold
)

gh repo edit $(printf ' --add-topic %q' "${topics[@]}")
```