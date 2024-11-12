# k3s-deployment

## Environment

- Debian 12 bookworm (raspberry pi)
- Raspberry Pi 5

## Steps

1. Enable cgroups. Steps [here](https://docs.k3s.io/installation/requirements?os=pi#cgroups).
1. Install dependencies.

    ```bash
    apt install iptables
    ```

1. Run install script. Steps [here](https://docs.k3s.io/quick-start#install-script).

    ```bash
    curl -sfL https://get.k3s.io | sh -
    ```

1. Validate cluster ingress in iptables.

    ```bash
    iptables -t nat -L KUBE-NODEPORTS -n -v
    ```

1. Setup NFS for statefulsets.

    ```bash
    apt install nfs-kernel-server
    mkdir /mnt/kube_pv
    # mount external drive to /mnt/kube_pv
    echo "/mnt/kube_pv 10.0.4.0/24(rw,sync,no_subtree_check,no_root_squash)" >> /etc/exports
    ```

1. Install gateway API CRDs. Steps [here](https://gateway-api.sigs.k8s.io/guides/#installing-gateway-api).
1. Bootstrap FluxCD. Steps [here](https://fluxcd.io/flux/installation/bootstrap/github/).
