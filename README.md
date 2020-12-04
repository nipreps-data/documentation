# documentation

```
export DATASET_NAME=ds000206
datalad create -c text2git -D "Test Dataset for NiPreps derived from OpenNeuro's ${DATASET_NAME}" ${DATASET_NAME}
datalad create-sibling-github --github-organization nipreps-data --github-login $USER -d ./${DATASET_NAME} -s github ${DATASET_NAME}
datalad create-sibling-osf --title "NiPreps testing - ${DATASET_NAME}" -s osf --public --category data -d ./${DATASET_NAME}
datalad siblings configure -d ./${DATASET_NAME} -s github --publish-depends osf
datalad siblings configure -d ./${DATASET_NAME} -s github --publish-by-default +refs/heads/*:refs/remotes/github/*
```


