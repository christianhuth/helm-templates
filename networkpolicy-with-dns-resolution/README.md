# Enable DNS resolution in Helm

```bash
helm template --enable-dns .
```

## Define your own hostname for DNS resolution

```bash
helm template --enable-dns --set hostname=${YOURHOSTNAME} .
```
