# Upgrading to a new version

TBD

# How to test Crossplane

TBD

# Modifications made to upstream chart

This is a high-level list of modifications that Big Bang has made to the upstream helm chart. You can use this as as cross-check to make sure that no modifications were lost during an upgrade process.

## chart/values.yaml

- Replace `image.repository` value with `registry1.dso.mil/ironbank/opensource/crossplane/crossplane`
- Add `imagePullSecrets` value
- Add `istio` key and values

## chart/Chart.yaml

- Add Big Bang version
- Add `bigbang.dev/applicationVersions` annotation
- Add `helm.sh/images` annotation

## chart/templates/bigbang/peerauthentication.yaml

- Add peerAuthentication template

## chart/templates/bigbang/networkpolicies/default-deny-all.yaml

- Add deny all networkPolicy

## chart/templates/bigbang/networkpolicies/egress-dns.yaml

- Add allow egress policy for DNS

## chart/templates/bigbang/networkpolicies/namespace-allow.yaml

- Add allow namespace policy
