# CRDs-catalog-custom

## repo clone
git clone git@github.com:husira/CRDs-catalog-custom.git; cd CRDs-catalog-custom;

## experimental/gateway.networking.k8s.io: update JSON schemas of experimental Gateway API
```
GATEWAY_API_VERSION="v1.1.0";
rm -rf experimental/gateway.networking.k8s.io; mkdir -p experimental/gateway.networking.k8s.io; cd experimental/gateway.networking.k8s.io;
git clone git@github.com:kubernetes-sigs/gateway-api.git; cd gateway-api;
git switch --detach "${GATEWAY_API_VERSION}"; cd ..;
curl -sO https://raw.githubusercontent.com/yannh/kubeconform/master/scripts/openapi2jsonschema.py && chmod 755 openapi2jsonschema.py; 
find gateway-api -wholename '*/config/crd/experimental/*.yaml' ! -name 'kustomization.yaml' -exec python3 openapi2jsonschema.py {} \; && rm -f openapi2jsonschema.py; rm -rf gateway-api/;
```
