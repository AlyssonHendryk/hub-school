# HUB SCHOOL — monorepo pessoal

Cópia independente dos códigos backend e frontend do HUB SCHOOL, sem histórico Git dos repositórios de origem e sem arquivos de ambiente locais.

## Estrutura

- backend/: API Python/FastAPI, autenticação Supabase JWT, PostgREST, Storage e testes offline.
- frontend/: aplicação Next.js/TypeScript com Supabase Auth, interface acadêmica e testes locais.
- Cada projeto possui seu próprio README.md com contratos, limitações e instruções detalhadas.

## Requisitos

- Python 3.11 ou superior.
- Node.js 20.9 ou superior e npm.
- Projeto Supabase com Auth, tabelas, RLS e bucket compatíveis já configurados para usar dados reais.

## Backend (PowerShell)

    cd backend
    py -3 -m venv .venv
    .\.venv\Scripts\Activate.ps1
    python -m pip install -r requirements.txt
    Copy-Item .env.example .env
    python -m uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload

Preencha localmente SUPABASE_URL, SUPABASE_JWT_ISSUER e uma chave pública SUPABASE_PUBLISHABLE_KEY ou SUPABASE_ANON_KEY. A API usa GET /health e oferece Swagger em http://127.0.0.1:8000/docs. Para testes offline, execute python -m pytest tests -q -s -p no:cacheprovider em ambiente com diretório temporário gravável.

## Frontend (outro terminal PowerShell)

    cd frontend
    npm.cmd ci
    Copy-Item .env.example .env.local
    npm.cmd run dev

Preencha NEXT_PUBLIC_SUPABASE_URL e NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY do mesmo projeto do backend. Em desenvolvimento, NEXT_PUBLIC_API_URL pode apontar para http://127.0.0.1:8000. Abra http://localhost:3000. Para validar: npx.cmd tsc --noEmit --incremental false; npm.cmd run lint; node --test tests/events.test.cjs tests/onboarding.test.cjs; npm.cmd run build.

Nunca use service_role no navegador ou como substituto do JWT de usuário. Não publique .env, .env.local, senhas ou tokens. Os scripts backend em scripts/ podem acessar serviços reais; execute-os apenas manualmente e quando autorizado.

## Limitações

A exclusão de anotações com anexos é bloqueada quando o backend encontra anexos, mas um upload concorrente ainda pode causar arquivo órfão. Consulte os READMEs dos dois projetos para outras limitações e pendências de validação real.
