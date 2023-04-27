# Upgrading to a new version

1. Update your helm repo

    ```bash
    helm repo update crossplane-stable
    ```

2. If you need to see what versions are available you can list them:

    ```bash
    helm search repo -l crossplane-stable
    ```

3. Pull down the new version of the chart

    ```bash
    helm pull crossplane-stable/crossplane --version v1.11.1
    ```

4. Extract the resulting tar to the `chart dir and strip the first directory

    ```bash
    tar -zxf crossplane-1.11.1.tgz -C chart --strip-components=1
    ```

5. Review the differences, add any missing info to `values.yaml` or `Chart.yaml`

6. Remove the tarball

    ```bash
    rm -rf crossplane-1.11.1.tgz
    ```

7. Update the README

    ```bash
    curl -LO https://repo1.dso.mil/big-bang/apps/library-charts/gluon/-/raw/master/docs/README.md.gotmpl && curl -LO https://repo1.dso.mil/big-bang/apps/library-charts/gluon/-/raw/master/docs/.helmdocsignore && curl -LO https://repo1.dso.mil/big-bang/apps/library-charts/gluon/-/raw/master/docs/_templates.gotmpl && docker run --rm -v "`pwd`:/helm-docs" -u $(id -u) jnorwood/helm-docs:v1.10.0 -s file -t /helm-docs/README.md.gotmpl -t /helm-docs/_templates.gotmpl --dry-run > README.md && rm .helmdocsignore README.md.gotmpl _templates.gotmpl
    ```

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
