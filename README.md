# Passgen Operator

## Overview
The Passgen Operator provides Kubernetes native deployment of the 
[passgen](https://github.com/giannisalinetti/passgen) tool used to offer a 
basic web-based password generator.

The operator provides a Customer Resource Definition and the logic to create
the passgen deployment, along with the certificates secret, service and 
the OpenShift route.

## The Passgen CRD
The following parameters can be customized:
- **size**: tune the number of replicas
- **imageName**: name of the passgen image. Default is *quay.io/gbsalinetti/passgen*
- **imageTag**: the passgen image tag. Default is *latest*
- **hostname**: custom hostname for the OpenShift route

## Operator Installation
First install the CRD:
```
$ make install
```

Build and push the passgen-operator image:
```
$ IMG=<some-registry>/<project-name>:<tag> make docker-build docker-push
```

Deploy the passgen-operator in your cluster:
```
$ IMG=<some-registry>/<project-name>:<tag> make deploy
```

## CR Installation
Install the Passgen custom resource using the config sample or generating 
a new CR.

The following example shows the usage of the config sample:
```
apiVersion: passgen.example.com/v1
kind: Passgen
metadata:
  name: passgen-sample
spec:
  size: 1
  imageName: quay.io/gbsalinetti/passgen
  imageTag: latest
  hostname: passgen.apps.ocp4.example.com
```

Install it with the kubectl CLI:
```
$ kubectl apply -f config/samples/passgen_v1_passgen.yaml
```

## CR Removal
Uninstall the Passgen custom resource
```
$ kubectl delete -f config/samples/passgen_v1_passgen.yaml
```

## Operator Removal
Using the Makefile the operator removal is very easy:
```
$ make undeploy
```

Remove the CRD:
```
$ kubectl delete crd/passgens.passgen.example.com
```

## Contributing
Contributions to this project are welcome.

## Maintainers
Gianni Salinetti <gsalinet@redhat.com>


