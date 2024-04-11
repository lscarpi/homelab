# Homelab

This repository contains the configuration files for my homelab. Feel free to use them as a reference for your own homelab.

### Hardware

- Raspberry Pi 5 (8GB) | 500GB Nvme SSD
- Raspberry Pi 5 (8GB) | 500GB Nvme SSD
- Raspberry Pi 5 (8GB) | 500GB Nvme SSD

### Software

- Ubuntu Server
- k3s
- docker
- Cloudflare Tunnel

### Services

- [Pi-hole](https://pi-hole.net/)
- [Cert-Manager](https://cert-manager.io/)
- [Portainer](https://www.portainer.io/)
- [Traefik](https://doc.traefik.io/traefik/)
- [Redis](https://redis.io/)
- [RabbitMQ](https://www.rabbitmq.com/)
- [Mailpit](https://mailpit.axllent.org/)

# Setup Instructions

First, install ubuntu server on the raspberry pi. This can be easily achieved by using the [Raspberry Pi Imager](https://www.raspberrypi.org/software/).

After OS installation, install docker using [this guide](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script) or [this guide](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).

These [extra steps](https://docs.docker.com/engine/install/linux-postinstall/) are also recommended.

Run the adguard service. That will give you dns resolution for your network for the local domain. Make sure to login into adguard and set your local domains in the Filters -> DNS Rewrites section.

> Don't forget to add the DNS server to your router's DHCP settings.

Then, install k3s using the following the official [k3s installation guide](https://docs.k3s.io/quick-start).

> Because of Rancher, the currently supported version is 1.27.11+k3s1.

After that, set up the cloudflare tunnel using the [this guide](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/private-net/cloudflared/).

> Don't forget to set up the private network IP ranges according to your network setup.

Copy the /etc/rancher/k3s/k3s.yaml file to your local machine at ~/.kube/config.
It might be necessary to change the Server IP, as it could be set to the private IP of the raspberry pi. Change it to the IP address of the PI in your network.

> Now, connecting to your k3s cluster should be as easy as running `kubectl get nodes`. To do this when outside your own network, you can connect to Clouflare WARP.

It is highly recommended that you set an Application in Zero Trust to secure your cluster. By doing so, you can control who can access your cluster and what they can do. More information can be found [here](https://developers.cloudflare.com/cloudflare-one/applications/configure-apps/self-hosted-apps/).

Now, it's time to deploy Rancher with the help of Helm. To do so, follow the instructions in the [Rancher Installation](k8s/apps/rancher/readme.md) guide.

With Rancher installed, you can set a public access to it in the Cloudflare Tunnel. It can be achieved by:

- Go to Zero Trust > Networks ->Tunnels
- Click on the tunnel you want to use and then click "Configure"
- In Public Hostname, add the hostname you want to use for your Rancher instance. It can be something like `rancher.yourdomain.com`.
- Click Save and wait for the tunnel to be updated.

Now, you can access your Rancher instance by going to `rancher.yourdomain.com`.

From here, you can deploy the rest of the services using the Rancher UI or by using the kubectl command line.

After deploying the services, if you wish to expose them to the internet, you can do so by following the same steps as for the Rancher service. Through the Cloudflare Public Hostnames.
