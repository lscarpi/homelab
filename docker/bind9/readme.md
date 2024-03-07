# Bind9 running inside Docker

If you want to use Bind9 inside a Docker container, there is a config to be changed in Ubuntu

Edit /etc/systemd/resolved.conf and change the line `DNSStubListener=yes` to `DNSStubListener=no`

Then, restart the systemd-resolved service with `sudo systemctl restart systemd-resolved`