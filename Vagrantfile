Vagrant.configure("2") do |config|
  config.vm.box = "fedora/34-cloud-base"
  config.vm.network "forwarded_port", guest: 6445, host: 6445, protocol: "tcp", id: "kcp"
  config.vm.network "forwarded_port", guest: 8080, host: 8081, protocol: "tcp", id: "podman-rest-api"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.name = "podman"
  end

  config.vm.provision "shell", inline: <<-SHELL
    dnf install -y podman

    groupadd -f -r podman

    #systemctl edit podman.socket
    mkdir -p /etc/systemd/system/podman.socket.d
    cat >/etc/systemd/system/podman.socket.d/override.conf <<EOF
[Socket]
SocketMode=0660
SocketUser=root
SocketGroup=podman
EOF
    systemctl daemon-reload
    echo "d /run/podman 0770 root podman" > /etc/tmpfiles.d/podman.conf
    sudo systemd-tmpfiles --create

    systemctl enable podman.socket
    systemctl start podman.socket

    usermod -aG podman $SUDO_USER
  SHELL
end
