# Tailscale Userspace Sidecar

Connect a K8s pod to your Tailscale tailnet.

This document is derived from the [Tailscale documentation](https://tailscale.com/kb/1185/kubernetes).

## Create Secret

To connect the sidecar to your tailnet, you will need to create a new [auth key](https://tailscale.com/kb/1085/auth-keys) and add it as a secret to your K8s cluster:

```shell
export TS_AUTHKEY=enter_your_ts_authkey
kubectl create secret generic tailscale-auth --from-literal=TS_AUTHKEY=$TS_AUTHKEY
```

## Deploy NGINX with Tailscale Sidecar

```shell
kubectl apply -k ./tailscale
```

## Deploy Jupyter Notebook

```shell
k apply -k ./tailscale/patches/jupyter-notebook
k logs jupyter-notebook | grep token=
```

This should output the token, you'll need to copy, then you can access the Jupyter Notebook via [https://jupyter-notebook:8888](https://jupyter-notebook:8888)
