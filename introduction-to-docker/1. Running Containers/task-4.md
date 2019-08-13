# Docker Essentials: Task Four

The MariaDB container keeps crashing and paging me. Can't you
keep this thing alive?!

## Additional Tasks:

1. Add health-checks

2. Add restart policies

3. Add cpu, memory, and pid limits

4. Harden your security: make your disk R/O

### Test

1. Try `apt update` with memory limit of 10MB
2. Stop & Kill your containers
3. Kill processes inside your containers
4. Ensure your new configuration works with `stress`

Use `stats` to monitor containers:

```shell
docker stats
```

#### Stress Commands

```shell
apt update && apt install --yes stress
stress --vm 2 --vm-bytes 128M
```

```shell
# Feeling brave?
:(){ :|: & };:
```
