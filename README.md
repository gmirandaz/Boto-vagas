# Boto Vagas
App ao vivo:https://boto-global-job-scout.lovable.app/

Coleta diária de vagas de emprego, organizada em banco de dados e exibida em um app web.

## Problema

Procurar vagas em vários sites é repetitivo. Quero um lugar único, atualizado automaticamente, onde as vagas aparecem organizadas por cargo.

## Como funciona

```
Schedule Trigger → HTTP Request → Split Out → Edit Fields → Supabase → Lovable
```

1. **Schedule Trigger** (n8n): roda todo dia às 7h.
2. **HTTP Request**: busca as vagas na API pública da Arbeitnow.
3. **Split Out**: separa a lista em uma vaga por item.
4. **Edit Fields**: escolhe os campos úteis (cargo, empresa, link, local, data).
5. **Create a row** (Supabase): grava as vagas na tabela `vagas`. O campo `link` é único, então vagas repetidas são ignoradas.
6. **App no Lovable**: lê a tabela e mostra as vagas com busca por cargo e palavra-chave.

## Ferramentas

- n8n (automação, rodando localmente com Docker)
- Supabase (banco de dados PostgreSQL e permissões por RLS)
- Lovable (interface do app)
- Arbeitnow (fonte pública de vagas)

## Arquivos

- `fluxo-n8n.json`: fluxo exportado do n8n. As credenciais não estão incluídas.

## Limitações

- A fonte tem vagas principalmente internacionais e remotas, não brasileiras.
- A coleta roda na máquina onde o n8n está ativo. Se ela estiver desligada, o app continua no ar, mas mostra a última coleta.
- O nível da vaga é identificado pelas palavras do título, o que pode gerar falsos positivos.

## Próximos passos

- Hospedar o n8n na nuvem para a coleta rodar sem depender de um computador.
- Adicionar fontes brasileiras, com permissão de uso.
- Classificar o nível de cada vaga com uma coluna própria no banco.

## Autor

Gabriel
