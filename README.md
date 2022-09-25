# OpenVpn-client-to-client-config

docker dah di install dan tau cara pakai

ketik command ni 

OVPN_DATA="gungsurya"

docker volume create --name $OVPN_DATA

docker run -v $OVPN_DATA:/etc/openvpn --rm agungsurya/agungsurya-openvpn:v1 ovpn_genconfig -u udp://202.145.2.100 #sesuaikan dengan ip serevr kamu

docker run -v $OVPN_DATA:/etc/openvpn --rm -it agungsurya/agungsurya-openvpn:v1 ovpn_initpki #wait tunggu

docker run -v $OVPN_DATA:/etc/openvpn -d -p 11109:1194/udp --cap-add=NET_ADMIN agungsurya/agungsurya-openvpn:v1 # mau port external berapa contoh 11109

docker run -v $OVPN_DATA:/etc/openvpn --rm -it agungsurya/agungsurya-openvpn:v1 easyrsa build-client-full gung nopass #(gung) = nama client mu

docker run -v $OVPN_DATA:/etc/openvpn --rm agungsurya/agungsurya-openvpn:v1 ovpn_getclient gung > gung.ovpn #sesuaikan namanya

import config gung.ovpn ke ovpn client #note config ada di directory pada saat dimana kamu ketikan command tadi




# selanjutnya konfigurasi client-to-client connection

docker ps #cek nama kontainer 

docker exec -it tender_gagarin /bin/bash  #contohnya namanya misal tender_gagarin

masuk ke shell ny container

ketik command

nano /etc/openvpn/openvpn.conf

kalau gada nano download sendiri (apk add nano)

tambahkan di konfigurasi

client-to-client

exit dan restart container

coba konek 2 client dan ping

jng lupa buat dua sertifikat untuk client lg satu

# referensi

https://hub.docker.com/r/agungsurya/agungsurya-openvpn
