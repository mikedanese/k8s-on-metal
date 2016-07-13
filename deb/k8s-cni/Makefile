CNI_RELEASE = 8a936732094c0941e1543ef5d292a1f4fffa1ac5

bin/cnitool bin/dhcp bin/ipvlan bin/ptp bin/flannel bin/macvlan bin/host-local bin/tuning bin/loopbackbin/bridge:
	curl -sSL --retry 5 https://storage.googleapis.com/kubernetes-release/network-plugins/cni-$(CNI_RELEASE).tar.gz | tar xz

deb: bin/cnitool bin/dhcp bin/ipvlan bin/ptp bin/flannel bin/macvlan bin/host-local bin/tuning bin/loopbackbin/bridge
	dpkg-buildpackage
