# Enable DNS resolution in Helm

```bash
helm template --enable-dns .
```

## Define your own hostname for DNS resolution

```bash
helm template --enable-dns --set hostname=${YOURHOSTNAME} .
```

## Read my Blog article about DNS resolution in Helm

https://blog.knell.it/get-rid-of-hard-coded-ips-in-your-helm-charts/
