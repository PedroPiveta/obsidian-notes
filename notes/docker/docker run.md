O comando `docker run` é utilizado para criar e iniciar um novo contêiner a partir de uma imagem Docker. Este comando é fundamental para executar aplicações em contêineres. Ele permite especificar várias opções, como mapeamento de portas, montagem de volumes, e variáveis de ambiente.

## Sintaxe
---
```bash
docker run [opções] <imagem> [comando] [argumentos]
```
## Principais opções
---
- `-d` ou `--detach`: Executa o contêiner em segundo plano (modo destacado).
- `-it`: Permite a interação com o contêiner via terminal. O `-i` mantém a entrada padrão aberta, enquanto o `-t` aloca um terminal.
- `--name <nome>`: Atribui um nome ao contêiner.
- `-p <host_port>:<container_port>`: Mapeia uma porta do host para uma porta do contêiner.
- `-v <host_path>:<container_path>`: Monta um volume, permitindo persistir dados ou compartilhar diretórios entre o host e o contêiner.
- `--env <VAR>=<valor>`: Define variáveis de ambiente dentro do contêiner.
## Exemplos
---
1. **Executar um contêiner Nginx em segundo plano:**
```bash
docker run -d --name meu_nginx nginx
```
2. **Executar um contêiner MySQL interativo:**
```bash
docker run -it --name meu_mysql -e MYSQL_ROOT_PASSWORD=minhasenha mysql
```
3. **Executar um contêiner com mapeamento de portas:**
```bash
`docker run -d -p 8080:80 --name meu_nginx nginx`
```
4. **Executar um contêiner com um volume montado:**
```bash
`docker run -d -v /minha/pasta:/dados --name meu_nginx nginx`
```
## Explicação
---
O `docker run` não só cria um novo contêiner a partir da imagem especificada, mas também o inicia imediatamente. O Docker utiliza o sistema de arquivos em camadas, permitindo que as imagens sejam mais eficientes, pois compartilham camadas comuns. Quando o contêiner é finalizado, os dados não persistidos são perdidos a menos que um volume tenha sido montado.