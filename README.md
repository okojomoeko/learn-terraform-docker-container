# learn-terraform-docker-container

terraform練習用のrepo。

macbook air M1を使っており、docker providerの実行はRancher Desktopを使っているので、
サンプルをそのまま動かすと
`Error pinging Docker server: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?`
と言われてしまう。

そのため、terraformでdocker providerを使うときは引数で入力するようにした。

```terraform
variable "docker_sock" {
  type        = string
  description = "Apply when Docker socket path is not default"
  default = "unix:///var/run/docker.sock"
}
```

`docker context ls`でsocketを確認して、自分が好きなdocker sockを入力したいときは下記みたいにする。

```shell
DOCKER_SOCK="docker_sock=unix:///Users/$USER/.rd/docker.sock"
terraform plan -var=$DOCKER_SOCK
terraform apply -var=$DOCKER_SOCK
terraform destroy -var=$DOCKER_SOCK
```
