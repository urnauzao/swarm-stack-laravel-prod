- Iniciar o Swarm na Aplicação Docker

```sh
docker swarm init
```

- Criar rede para o Swarm

```sh
docker network create -d overlay --attachable swarm
```

- Subir serviços no Swarm

```sh
docker stack deploy -c docker-swarm.yml application
```

- Derrubar serviços no Swarm

```sh
docker stack rm application
```

- Ver serviços em execução

```sh
docker service ls
```

- Ver containers em execução

```sh
docker stats
```

- Executar aplicação docker direto

```sh
docker run -p 80:80 urnau/php82-app-2023:v1
```

- Script para upar aplicação

```sh
sudo ./up.sh
```

- Script para derrubar aplicação

```sh
sudo ./down.sh
```

## EM CASO DE PROBLEMAS

- <b>Não consegui acessar o Localhost no navegador</b>, o que fazer?

  - Certifique-se que o yml possuí a configuração de porta.
  - Em caso do docker instalado no próprio WSL2, realize o passo a passo abaixo de instalação do IFCONFIG para obter o IP do WSL2.
  - Insira no navegador o IP obtido e então acesse-o.
  - Com isso você visualizará atrás do IP do WSL2 a sua aplicação. Detalhe, o IP pode mudar a cada vez que você reiniciar o PC ou o próprio WSL2.

- <b>Não consegui acessar a aplicação em produção pelo navegador</b>, o que fazer?

  - Certifique-se que seus containers docker estão em execução
  - Certifique-se que seu servidor de produção está com as portas de sua aplicação liberadas.
  - Certifique-se que você alterou o arquivo `nginx-sites.conf` com o endereco da sua aplicação / ip do servidor de produção.

- <b>Como saber se tenho um firewall?</b>
  - Em um servidor Linux Debian, execute o comando abaixo e procure por, `iptables`, `firewalld`, `ufw` ou `csf`. O que você encotrar desta lista é o firewall de sua máquina.

```sh
systemctl list-units --type=service --state=active
```

- <b>Como saber se o iptables está ativo:</b>
  - Execute o comando abaixo.

```sh
sudo iptables -L
```

- <b>Como criar usuário no Debian?</b>

```sh
sudo useradd -m usuarioX -s /bin/bash
sudo passwd usuarioX
sudo usermod -aG sudo usuarioX
```

- <b>Ver logs de erros de um serviço</b>

```sh
docker service ls
docker service ps --no-trunc application_web
```

- <b>Erro de Bridge Network, em caso de Iptables com OpenVZ</b><br>
  Se o provedor de hospedagem não permitir a modificação do arquivo `/proc/sys/net/bridge/bridge-nf-call-iptables`, é possível contornar o problema configurando o Docker para não tentar restringir a comunicação entre contêineres. Para fazer isso, você pode adicionar a seguinte linha ao arquivo `/etc/docker/daemon.json`, caso o arquivo não exista, crie-o. Em seu conteúdo adicione a chave "iptables".

```json
{
  "iptables": false
}
```
