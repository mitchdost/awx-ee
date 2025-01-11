# changes mdo

EE stands for execution-environment

## Additions from mdo

### Changed files

I needed a execution-environment with additional binaries.

`execution-environment.yml`

```diff
+jmespath
+python-gitlab
```

## Building and pushing the image

### Prepare this project

- check this repo
- create a venv containing `ansible-builder`
- adjust `execution-environment.yml`

### Prepare gitlab

see [docs-software/git/gitlab.md] for the login url and image path

### Build and push the image with docker

- store tag name in variable

  ```bash
  # awx-setup is the basename of the gitlab project
  # awx-ee ist the image name
  image_name_tag=registry.gitlab.com/mitchdost-themes/awx/awx-setup/awx-ee:0.4
  ```

- docker login

  ```bash
  # i.e. registry.gitlab.com
  docker login ${image_name_tag%%/*}
  ```

- build the image

  ```bash
  ansible-builder build --tag ${image_name_tag:?} --container-runtime docker -f execution-environment.yml
  ```

- push the image

  ```bash
  docker push ${image_name_tag:?}
  ```

<!-- Link Collection: -->

[docs-software/git/gitlab.md]: <https://gitlab.com/mitchdost/docs-software/-/blob/main/git/gitlab.md>
