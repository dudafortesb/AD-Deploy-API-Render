# API de Upload e Download de Arquivos

API desenvolvida em Python com Flask para receber arquivos e permitir seu download.

## Tecnologias
- Python
- Flask
- SQLite
- Gunicorn (servidor para produção)

## Como executar localmente

1. Crie e ative um ambiente virtual (opcional, mas recomendado).
2. Instale as dependências:

```bash
pip install -r requirements.txt
```

3. Inicie a API:

```bash
python app.py
```

A aplicação ficará disponível em `http://127.0.0.1:10000`.

## Rotas

### Enviar arquivo
- **Método:** POST
- **Endpoint:** `/uploads/upload`
- **Campo do formulário:** `file`
- **Tipos permitidos:** png, jpg, jpeg, gif, pdf e txt.
- **Tamanho máximo:** 30 KB (limite verificado no tamanho da requisição).

Exemplo com cURL:

```bash
curl -X POST -F "file=@exemplo.pdf" http://127.0.0.1:10000/uploads/upload
```

### Baixar arquivo
- **Método:** GET
- **Endpoint:** `/downloads/download/<nome_do_arquivo>`

Exemplo:

```text
http://127.0.0.1:10000/downloads/download/exemplo.pdf
```

## Publicação no Render

1. Crie um repositório no GitHub e envie todos os arquivos deste projeto.
2. No Render, crie um **Web Service** e conecte o repositório.
3. Configure:
   - **Runtime:** Python
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn app:app`
4. Faça o deploy. O Render fornecerá uma URL pública.

## Observação sobre arquivos e banco de dados

O projeto grava os arquivos na pasta `uploads` e usa SQLite no arquivo `database.db`. Em hospedagens com armazenamento efêmero, esses dados podem ser perdidos quando a instância reinicia ou é recriada. Para manter os arquivos e o banco entre reinicializações, configure um disco persistente no serviço e ajuste os caminhos da aplicação para esse disco.
