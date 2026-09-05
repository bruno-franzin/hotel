## Stack e entrada
- Backend único em `app.py`: Flask, Flask-CORS, Agno/OpenAI e Supabase.
- Interface inteira em `static/index.html`, com CSS e JavaScript inline; não há etapa de build nem outro pacote frontend.
- `requirements.txt` é a fonte versionada das dependências Python.

## Execução
- No Windows, iniciar na porta 8000 com: `& .\.venv\Scripts\python.exe app.py`
- O startup chama `load_dotenv()` e cria o cliente Supabase imediatamente. O `.env` precisa fornecer `SUPABASE_URL`, `SUPABASE_KEY` e `OPENAI_API_KEY`; não leia nem exponha seus valores.
- O servidor usa `host="0.0.0.0"` e `debug=True` quando executado diretamente.

## Fluxo da aplicação
- `GET /` serve `static/index.html`; `GET /imagens/<arquivo>` serve arquivos de `imagens/`.
- `POST /perguntar` recebe JSON com `pergunta`, executa o agente `gpt-4o-mini` e retorna `{mensagem}`.
- `POST /reservas` insere o JSON recebido na tabela Supabase `reservas`; `GET /reservas` lista seus registros.
- O frontend usa essas rotas para o chat, criação de reservas e listagem de reservas confirmadas.

## Verificação e limites
- Não há testes, linter, typecheck, CI ou configuração de build no repositório; após mudanças, faça ao menos uma verificação manual pelo servidor local.
- Preserve a descrição do agente de hotel em `app.py` ao alterar o backend.
- Responda em PT-BR e mantenha comentários úteis para leitores iniciantes quando adicionar lógica não óbvia.
