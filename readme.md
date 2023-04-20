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
