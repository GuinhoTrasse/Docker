## Como rodar com Docker

Arquitetura: 2 containers ligados pelo Docker Compose.

| Container | Função |
|---|---|
| proxy | nginx: recebe as requisições na porta 8080 e repassa para o app |
| app | Flask rodando com gunicorn: contém o sistema e o banco SQLite |

Fluxo: navegador -> nginx (porta 8080) -> Flask/gunicorn (porta 8000, só na rede interna) -> banco SQLite no volume `dados`.

Os dados ficam em dois volumes (`dados` para o banco e `uploads` para os comprovantes) e continuam depois de parar os containers.

### Passos

1. Instalar o Docker Desktop e deixá-lo aberto.
2. Subir tudo: `docker compose up -d --build`
3. Popular o banco (só na primeira vez): `docker compose exec app python popular.py`
4. Abrir http://localhost:8080 (contas de teste na tabela mais abaixo).
5. Parar: `docker compose down` (não usar `-v`, que apaga os dados).
