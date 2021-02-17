# documentation

```
export DATASET_NAME=ds000206
datalad create -c text2git --initial-branch main -D "Test Dataset for NiPreps derived from OpenNeuro's ${DATASET_NAME}" ${DATASET_NAME}
datalad create-sibling-osf --title "NiPreps testing - ${DATASET_NAME}" -s osf --public --category data -d ./${DATASET_NAME}
datalad create-sibling-github --github-organization nipreps-data --github-login $USER -d ./${DATASET_NAME} -s github ${DATASET_NAME} --publish-depends osf-storage

cd ${DATASET_NAME}
datalad create -c text2git --initial-branch main -D "Test Dataset for NiPreps derived from OpenNeuro's ${DATASET_NAME} [derivatives]" derivatives
datalad create-sibling-osf --title "NiPreps testing - ${DATASET_NAME} [derivatives]" -s osf --public --category data -d ./derivatives
datalad create-sibling-github --github-organization nipreps-data --github-login $USER -d ./derivatives -s github ${DATASET_NAME}-derivatives --publish-depends osf-storage
# datalad siblings configure -d ./derivatives -s github --publish-by-default +refs/heads/*:refs/remotes/github/*
```
