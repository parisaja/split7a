#!/bin/bash
red='\e[1;31m'
green='\e[0;32m'
NC='\e[0m'
ns_domain_cloudflare1() {
apt install jq curl -y
clear

sub=f$(tr -dc 'a-z0-9' </dev/urandom | head -c5)
DOMAIN=baguno.my.id
SUB_DOMAIN=${sub}.baguno.my.id
CF_ID=pharaohmod075@gmail.com
CF_KEY=c4775ef3fd35012ce9f7dc124b7ba80235a81

set -euo pipefail
IP=$(wget -qO- ipinfo.io/ip);
     
     #wildcard
RECORD1=$(curl -sLX GET "https://api.cloudflare.com/client/v4/zones/${ZONE}/dns_records?name=*.${SUB_DOMAIN}" \
     -H "X-Auth-Email: ${CF_ID}" \
     -H "X-Auth-Key: ${CF_KEY}" \
     -H "Content-Type: application/json" | jq -r .result[0].id)

if [[ "${#RECORD1}" -le 10 ]]; then
     RECORD=$(curl -sLX POST "https://api.cloudflare.com/client/v4/zones/${ZONE}/dns_records" \
     -H "X-Auth-Email: ${CF_ID}" \
     -H "X-Auth-Key: ${CF_KEY}" \
     -H "Content-Type: application/json" \
     --data '{"type":"A","name":"'*.${SUB_DOMAIN}'","content":"'${IP}'","ttl":120,"proxied":false}' | jq -r .result.id)
fi

RESULT1=$(curl -sLX PUT "https://api.cloudflare.com/client/v4/zones/${ZONE}/dns_records/${RECORD1}" \
     -H "X-Auth-Email: ${CF_ID}" \
     -H "X-Auth-Key: ${CF_KEY}" \
     -H "Content-Type: application/json" \
     --data '{"type":"A","name":"'*.${SUB_DOMAIN}'","content":"'${IP}'","ttl":120,"proxied":false}')

echo ""
echo "Wildcard : *.$SUB_DOMAIN"
echo -e "Done Record Domain= ${SUB_DOMAIN} For VPS"
sleep 1
}
ns_domain_cloudflare1