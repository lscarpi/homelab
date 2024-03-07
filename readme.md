# Homelab

This repository contains the configuration files for my homelab. Feel free to use them as a reference for your own homelab.

### Hardware

- Raspberry Pi 5 (8GB) | 500GB Nvme SSD

### Software

- Ubuntu Server
- k3s
- Cloudflare Tunnel

### Services

- [Portainer](https://www.portainer.io/)
- [Traefik](https://doc.traefik.io/traefik/)
- [Redis](https://redis.io/)
- [RabbitMQ](https://www.rabbitmq.com/)
- [Mailpit](https://mailpit.org/)

# Setup Instructions

First, install ubuntu server on the raspberry pi. This can be easily achieved by using the [Raspberry Pi Imager](https://www.raspberrypi.org/software/).

Then, install k3s using the following the official [k3s installation guide](https://docs.k3s.io/quick-start).

After that, set up the cloudflare tunnel using the [this guide](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/private-net/cloudflared/).

> Don't forget to set up the private network IP ranges according to your network setup.

Copy the /etc/rancher/k3s/k3s.yaml file to your local machine at ~/.kube/config.
It might be necessary to change the Server IP, as it could be set to the private IP of the raspberry pi. Change it to the IP address of the PI in your network.

> Now, connecting to your k3s cluster should be as easy as running `kubectl get nodes`. To do this when outside your own network, you can connect to Clouflare WARP.

It is highly recommended that you set an Application in Zero Trust to secure your cluster. By doing so, you can control who can access your cluster and what they can do. More information can be found [here](https://developers.cloudflare.com/cloudflare-one/applications/configure-apps/self-hosted-apps/).

Now, it's time to deploy Portainer with the help of Helm. To do so, follow the instructions in the [official Portainer documentation](https://docs.portainer.io/v/2.14/start/install/server/kubernetes/baremetal#deploy-using-helm).

With Portainer installed, you can set a public access to it in the Cloudflare Tunnel. It can be achieved by:

- Go to Zero Trust > Networks ->Tunnels
- Click on the tunnel you want to use and then click "Configure"
- In Public Hostname, add the hostname you want to use for your Portainer instance. It can be something like `portainer.yourdomain.com`.
- The type will be HTTP and the destination will be the network IP of your raspberry pi, on the port 30777.
- Click Save and wait for the tunnel to be updated.

Now, you can access your Portainer instance by going to `portainer.yourdomain.com`.

From here, you can deploy the rest of the services using the Portainer UI or by using the kubectl command line.