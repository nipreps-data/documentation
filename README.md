# Documentation

## Dataset setup

Given a dataset, such as `ds000206`, prepare:

```bash
export DATASET_NAME=ds000206
datalad create -c text2git -D "Test Dataset for NiPreps derived from OpenNeuro's ${DATASET_NAME}" ${DATASET_NAME} --initial-branch main
cd $DATASET_NAME
datalad create -d . -c text2git -D "Test Dataset for NiPreps derived from OpenNeuro's ${DATASET_NAME} [derivatives]" ${DATASET_NAME}/derivatives --initial-branch main
```

## Setting up GIN siblings

This requires datalad 0.16 (still in development).

```bash
datalad create-sibling-gin nipreps-data/${DATASET_NAME} -s gin
git annex enableremote gin
datalad create-sibling-gin -d derivatives nipreps-data/${DATASET_NAME}-derivatives -s gin
git -C derivatives annex enableremote gin
```

Note that because we use `main` and GOGS still assumes `master` will be the default branch in many places,
you will need to update these manually in the repository settings.

## Setting up OSF siblings

```bash
datalad create-sibling-osf --title "NiPreps testing - ${DATASET_NAME}" -s osf --public --category data -d ./${DATASET_NAME}
datalad create-sibling-osf --title "NiPreps testing - ${DATASET_NAME} [derivatives]" -s osf --public --category data -d ./derivatives
```

## Setting up GitHub siblings

If you've set up OSF siblings, set:

```bash
OSF="--publish-depends osf-storage"
```

In any case:

```bash
datalad create-sibling-github --github-organization nipreps-data --github-login $USER -d ./${DATASET_NAME} -s github ${DATASET_NAME} ${OSF}
datalad create-sibling-github --github-organization nipreps-data --github-login $USER -d ./derivatives -s github ${DATASET_NAME}-derivatives ${OSF}
# datalad siblings configure -d ./derivatives -s github --publish-by-default +refs/heads/*:refs/remotes/github/*
```
