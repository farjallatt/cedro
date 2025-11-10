# Cedro SO - Sistema de Gestão para Clínicas e Terapeutas

Sistema completo de gestão desenvolvido para clínicas e profissionais de saúde mental, oferecendo ferramentas integradas para gerenciamento de pacientes, agenda, CRM, prontuários eletrônicos, financeiro e muito mais.

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Tecnologias](#tecnologias)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Configuração](#configuração)
- [Scripts Disponíveis](#scripts-disponíveis)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Documentação](#documentação)
- [Desenvolvimento](#desenvolvimento)
- [Contribuindo](#contribuindo)

## 🎯 Sobre o Projeto

Este projeto centraliza fluxos de automação para atendimento e fechamento comercial usando o n8n. Ele integra canais de mensagem (ex.: WhatsApp via provedor/Chatwoot), Redis para orquestração de filas, Postgres para persistência, Asaas para clientes/cobranças e um agente LLM (LangChain) que decide e aciona ferramentas durante a conversa.

### O que é o n8n?
O n8n é uma plataforma de automação de fluxos (workflows) de código aberto. Você cria pipelines visuais conectando “nós” (nodes) que recebem eventos, transformam dados, chamam APIs, acessam bancos e muito mais. Cada fluxo exportado em JSON pode ser versionado neste repositório e importado na UI do n8n.


### Principais Características

- **Interface Moderna**: Design system MotherDuck com componentes consistentes e acessíveis
- **Performance Otimizada**: Utiliza React Query para cache inteligente e atualizações em tempo real
- **Segurança**: Autenticação robusta com Supabase Auth
- **Escalável**: Arquitetura preparada para crescimento
- **Integrações**: n8n para automações e workflows personalizados

## ✨ Funcionalidades

### 👥 Gestão de Pacientes
- Cadastro completo de pacientes
- Histórico de atendimentos
- Planos de tratamento
- Filtros e buscas avançadas

### 📅 Agenda
- Agendamento de consultas
- Gestão de disponibilidade de terapeutas
- Exceções de horário (bloqueios e horários extras)
- Status de atendimentos (agendado, confirmado, concluído, cancelado, etc.)

### 📊 CRM
- Gestão de leads
- Pipeline de vendas (Kanban)
- Histórico de interações
- Conversão de leads em pacientes

### 📝 Prontuários Eletrônicos
- Criação e edição de prontuários
- Processamento de áudio com transcrição (Whisper API)
- Geração automática de resumos com IA (Groq/OpenAI)
- Visualização e edição de registros médicos

### 💰 Financeiro
- Gestão de faturas
- Integração com gateway de pagamento (Asaas)
- Controle de recebimentos
- Relatórios financeiros

### 📈 Dashboard
- KPIs em tempo real
- Gráficos de receita e performance
- Funil de conversão CRM
- Widgets informativos (pacientes pausados, faturas vencidas, leads recentes)

### 🔄 Automações (n8n)
- Workflows personalizados
- Integração com sistemas externos
- Automação de processos repetitivos

## 🛠 Tecnologias

### Frontend
- **Next.js 14** - Framework React com App Router
- **React 18** - Biblioteca UI
- **TypeScript** - Tipagem estática
- **Tailwind CSS** - Estilização utilitária
- **Radix UI** - Componentes acessíveis
- **TanStack Query** - Gerenciamento de estado servidor
- **React Hook Form** - Formulários
- **Zod** - Validação de schemas

### Backend
- **Supabase** - Backend as a Service (PostgreSQL, Auth, Storage)
- **Next.js API Routes** - Endpoints da API
- **MinIO** - Armazenamento de objetos (S3-compatible)

### Processamento de Áudio
- **FFmpeg** - Processamento de áudio no servidor
- **Whisper API** - Transcrição de áudio
- **Groq/OpenAI** - Geração de resumos com IA

### Testes
- **Vitest** - Framework de testes
- **React Testing Library** - Testes de componentes
- **jsdom** - Ambiente DOM para testes

### Automação
- **n8n** - Plataforma de automação de workflows

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Node.js** 18+ e npm/yarn
- **Git** para controle de versão
- Conta no **Supabase** (para banco de dados e autenticação)
- Conta no **MinIO** ou S3-compatible (para armazenamento)
- Chaves de API para:
  - Whisper API (OpenAI)
  - Groq ou OpenAI (para processamento de IA)

## 🚀 Instalação

1. **Clone o repositório**
```bash
git clone https://github.com/seu-usuario/cedro-so.git
cd cedro-so
```

2. **Instale as dependências**
```bash
npm install
# ou
yarn install
```

3. **Configure as variáveis de ambiente**
```bash
cp .env.example .env.local
```

4. **Preencha as variáveis de ambiente** (veja seção [Configuração](#configuração))

5. **Execute as migrações do banco de dados** (se necessário)

6. **Inicie o servidor de desenvolvimento**
```bash
npm run dev
```

O projeto estará disponível em `http://localhost:3000`

## ⚙️ Configuração

Crie um arquivo `.env.local` na raiz do projeto com as seguintes variáveis:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=sua-url-do-supabase
NEXT_PUBLIC_SUPABASE_ANON_KEY=sua-chave-anonima
SUPABASE_SERVICE_ROLE_KEY=sua-chave-de-servico

# MinIO / S3
MINIO_ENDPOINT=seu-endpoint-minio
MINIO_PORT=9000
MINIO_ACCESS_KEY=sua-access-key
MINIO_SECRET_KEY=sua-secret-key
MINIO_BUCKET=nome-do-bucket
MINIO_USE_SSL=false

# APIs de Processamento
OPENAI_API_KEY=sua-chave-openai
GROQ_API_KEY=sua-chave-groq

# n8n (opcional)
N8N_WEBHOOK_URL=url-do-webhook-n8n

# Outras configurações
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### Configuração do Supabase

1. Crie um projeto no [Supabase](https://supabase.com)
2. Configure o schema `cedro` no banco de dados
3. Execute as migrações necessárias
4. Configure as políticas RLS (Row Level Security) conforme necessário

### Configuração do MinIO

1. Configure um servidor MinIO ou use um serviço S3-compatible
2. Crie um bucket para armazenar os arquivos de áudio
3. Configure as credenciais de acesso

## 📜 Scripts Disponíveis

```bash
# Desenvolvimento
npm run dev          # Inicia servidor de desenvolvimento
npm run build        # Cria build de produção
npm start            # Inicia servidor de produção

# Qualidade de Código
npm run lint         # Executa ESLint
npm run typecheck    # Verifica tipos TypeScript

# Testes
npm run test         # Executa testes com Vitest
npm run test:ui      # Abre interface visual de testes
npm run test:coverage # Gera relatório de cobertura
```

## 📁 Estrutura do Projeto

```
cedro-so/
├── src/
│   ├── app/                    # Rotas Next.js (App Router)
│   │   ├── api/                # API Routes
│   │   │   ├── audio/          # Processamento de áudio
│   │   │   ├── medical-records/ # Prontuários
│   │   │   └── n8n/            # Callbacks n8n
│   │   ├── agenda/             # Página de agenda
│   │   ├── crm/                # Página de CRM
│   │   ├── dashboard/          # Dashboard principal
│   │   ├── pacientes/         # Gestão de pacientes
│   │   ├── prontuarios/        # Prontuários eletrônicos
│   │   └── financeiro/         # Módulo financeiro
│   ├── components/             # Componentes React
│   │   ├── ui/                 # Componentes base (shadcn/ui)
│   │   ├── agenda/             # Componentes de agenda
│   │   ├── crm/                # Componentes de CRM
│   │   ├── dashboard/          # Componentes de dashboard
│   │   └── layout/             # Componentes de layout
│   ├── lib/                    # Utilitários e helpers
│   │   ├── api/                # Funções de API
│   │   ├── supabase/           # Cliente Supabase
│   │   └── utils.ts            # Funções utilitárias
│   ├── hooks/                  # Custom hooks React
│   ├── providers/              # Context providers
│   └── data/                   # Dados mock (desenvolvimento)
├── n8n/                        # Workflows n8n
│   ├── atendimento.json        # Workflow de atendimento
│   ├── closer.json             # Workflow de fechamento
│   └── disparo.json            # Workflow de disparo
├── .agent/                     # Documentação técnica
├── public/                     # Arquivos estáticos
└── build/                      # Build de produção
```

## 📚 Documentação

Documentação completa disponível na pasta `.agent/`:

- **DOCUMENTATION_SUMMARY.txt** - Índice geral da documentação
- **01-project-architecture.md** - Arquitetura do sistema
- **02-database-schema.md** - Schema do banco de dados
- **03-design-system.md** - Design system MotherDuck
- **04-sop.md** - Procedimentos operacionais padrão
- **05-recent-updates.md** - Atualizações recentes

### Design System

O projeto utiliza o **Design System MotherDuck** com:
- Paleta de cores: Dark (#383838), Teal (#16AA98), Beige (#F4EFEA), Blue (#6FC2FF)
- Tipografia: Space Mono (títulos), Inter (corpo)
- Sistema de espaçamento: 8px-40px
- Componentes acessíveis com Radix UI

Visualize os componentes em: `/design-system`

## 💻 Desenvolvimento

### Padrões de Código

- **Sempre use o schema `cedro`** nas queries do banco (não `public`)
- Crie funções puras de API em `src/lib/api/`
- Envolva dados com hooks do React Query
- Use `queryKeys` factory de `react-query-patterns.ts`
- Aplique o design system MotherDuck em toda UI
- Trate erros com notificações toast apropriadas
- Use TypeScript em modo strict (sem `any` sem comentários)

### Adicionando uma Nova Feature

1. Consulte a documentação em `.agent/04-sop.md`
2. Crie as funções de API em `src/lib/api/`
3. Crie hooks customizados em `src/hooks/`
4. Desenvolva componentes seguindo o design system
5. Adicione testes quando apropriado
6. Atualize a documentação se necessário

### Estrutura de uma Query

```typescript
// src/lib/api/feature.ts
export async function getFeatureById(id: string) {
  const { data } = await supabase
    .schema('cedro')  // Sempre use schema cedro
    .from('table_name')
    .select('*')
    .eq('id', id)
    .single();
  
  return data;
}

// src/hooks/use-feature.ts
export function useFeature(id: string | undefined) {
  return useQuery({
    queryKey: queryKeys.features.detail(id),
    queryFn: () => getFeatureById(id!),
    enabled: !!id,
    ...QUERY_OPTIONS_DETAIL
  });
}
```

## 🤝 Contribuindo

Contribuições são bem-vindas! Por favor:

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

### Checklist antes de fazer commit

- [ ] Código segue os padrões do projeto
- [ ] Testes passam (`npm run test`)
- [ ] TypeScript não apresenta erros (`npm run typecheck`)
- [ ] Linter não apresenta erros (`npm run lint`)
- [ ] Design system foi aplicado corretamente
- [ ] Documentação foi atualizada (se necessário)

## 📄 Licença

Este projeto é privado e de uso interno.

## 📞 Suporte

Para dúvidas ou problemas:
- Consulte a documentação em `.agent/`
- Verifique os exemplos em `/design-system`
- Revise os testes para padrões de implementação

---

**Desenvolvido com ❤️ para profissionais de saúde mental**

