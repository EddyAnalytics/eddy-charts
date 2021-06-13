# Helm Chart for the Eddy Analytics Platform

Installation instructions:

1. Edit values.yaml to your liking, defaults should work
1. `helm dependency update`
1. `export RELEASE_NAME=eddy-demo`
1. `helm upgrade --cleanup-on-fail --install $RELEASE_NAME . --namespace eddy  --values values.yaml`

Subsequent upgrades:

1. `export RELEASE_NAME=eddy-demo`
1. `export MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace eddy $RELEASE_NAME-mysql -o jsonpath="{.data.mysql-root-password}" | base64 --decode)`
1. `helm upgrade --cleanup-on-fail --install $RELEASE_NAME . --namespace eddy  --values values.yaml --set mysql.auth.rootPassword=$MYSQL_ROOT_PASSWORD`