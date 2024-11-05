O comando `docker pull` é usado para baixar uma imagem do repositório de imagens do Docker (Docker Hub) ou de outro registro configurado. Esse comando facilita a obtenção de imagens que você pode usar para criar e executar contêineres em sua máquina local.

## Sintaxe
---
```bash
docker pull <imagem>:<tag>
```
- `<imagem>`: O nome da imagem que você deseja baixar. Se você não especificar um repositório, o Docker buscará no Docker Hub.
- `<tag>`: A versão específica da imagem. Se omitida, o Docker baixa a versão `latest`.
## Exemplos
---
1. Baixar a imagem mais recente do Nginx
```
docker pull nginx
```
2. Baixar uma versão específica do MySQL
```
docker pull mysql:5.7
```
3. Baixar uma imagem de um repositório privado:
```
docker pull myregistry.com/meu_usuario/minha_imagem:1.0
```

## Comandos relacionados
---
- [[docker images]]
- [[docker rmi]]