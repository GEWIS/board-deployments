# google-calendar-sync

Deployed by Flux (`k8s-apps` → `board/google-calendar-sync`) into the `board` namespace.

## Seal the people secret

`secret.yaml` is a placeholder. Fill it with one `<member>.env` per board member,
seal it, and commit **only** the sealed output — never the plaintext.

Install kubeseal (Linux amd64, v0.38.4):

```sh
curl -OL https://github.com/bitnami/sealed-secrets/releases/download/v0.38.4/kubeseal-0.38.4-linux-amd64.tar.gz
tar -xzf kubeseal-0.38.4-linux-amd64.tar.gz kubeseal && sudo install -m 755 kubeseal /usr/local/bin/kubeseal
```

Seal offline against the GEWIS cert, bound to namespace `board`:

```sh
kubeseal --cert https://sealed-secrets.gewis.nl/v1/cert.pem \
  --format yaml --namespace board \
  < secret.yaml > secret.sealed.yaml
```
