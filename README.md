# Sistema de Agendamento de Exames de Biorressonância

## 📋 Visão Geral

Sistema web responsivo completo para agendamento de exames de biorressonância, desenvolvido com Next.js 15, TypeScript e Tailwind CSS. Inclui chatbot integrado com persona de Naturopata Sênior, painel administrativo e simulação de integração WhatsApp.

## 🚀 Funcionalidades Principais

### 🏠 Página Inicial
- Apresentação da tecnologia de biorressonância
- Explicação sobre tratamentos com nanotecnologia
- Design responsivo e moderno
- Call-to-actions para agendamento

### 📅 Sistema de Agendamento
- Seleção de pontos de atendimento
- Calendário interativo para escolha de datas
- Seleção de horários disponíveis
- Formulário de dados pessoais
- Confirmação automática via WhatsApp (simulado)

### 🤖 Chatbot Naturopata Sênior
- Persona especializada em biorressonância
- Respostas inteligentes sobre procedimentos
- Explicações sobre nanotecnologia
- Orientações de preparo para exames
- Direcionamento para agendamento

### 🔧 Painel Administrativo
- CRUD completo de pontos de atendimento
- Visualização de agendamentos
- Dashboard com estatísticas
- Filtros e busca avançada
- Gerenciamento de horários e capacidade

### 📱 Integração WhatsApp (Simulada)
- Confirmações automáticas de agendamento
- Lembretes e orientações
- Log de conversas
- Respostas automatizadas do naturopata

## 🛠️ Tecnologias Utilizadas

### Frontend
- **Next.js 15** - Framework React com App Router
- **TypeScript** - Tipagem estática
- **Tailwind CSS** - Estilização utilitária
- **shadcn/ui** - Componentes acessíveis
- **Radix UI** - Primitivos de interface
- **date-fns** - Manipulação de datas

### Backend
- **Next.js API Routes** - Endpoints serverless
- **SQLite** - Banco de dados local
- **better-sqlite3** - Driver SQLite otimizado

### Componentes UI
- **Calendário** - Seleção de datas
- **Formulários** - React Hook Form
- **Tabelas** - Visualização de dados
- **Diálogos** - Modais interativos
- **Cards** - Layout de conteúdo

## 📁 Estrutura do Projeto

```
src/
├── app/
│   ├── page.tsx                    # Página inicial
│   ├── layout.tsx                  # Layout principal
│   ├── agendamento/
│   │   └── page.tsx               # Sistema de agendamento
│   ├── chatbot/
│   │   └── page.tsx               # Interface do chatbot
│   ├── admin/
│   │   └── page.tsx               # Painel administrativo
│   └── api/
│       ├── agendamentos/
│       │   └── route.ts           # API de agendamentos
│       ├── pontos-atendimento/
│       │   ├── route.ts           # API de pontos
│       │   └── [id]/route.ts      # CRUD individual
│       └── whatsapp/
│           └── route.ts           # Simulação WhatsApp
├── components/
│   └── ui/                        # Componentes shadcn/ui
├── hooks/                         # Hooks customizados
└── lib/
    └── utils.ts                   # Utilitários
```

## 🗄️ Banco de Dados

### Tabelas Principais

#### `pontos_atendimento`
```sql
CREATE TABLE pontos_atendimento (
    id TEXT PRIMARY KEY,
    nome TEXT NOT NULL,
    endereco TEXT NOT NULL,
    cidade TEXT NOT NULL,
    horarios TEXT NOT NULL,        -- JSON array
    capacidade_por_horario INTEGER DEFAULT 1,
    status TEXT DEFAULT 'ativo',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

#### `agendamentos`
```sql
CREATE TABLE agendamentos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    telefone TEXT NOT NULL,
    email TEXT,
    cidade TEXT,
    ponto_atendimento_id TEXT NOT NULL,
    data_agendamento TEXT NOT NULL,
    horario TEXT NOT NULL,
    status TEXT DEFAULT 'agendado',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

#### `whatsapp_logs`
```sql
CREATE TABLE whatsapp_logs (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    telefone TEXT NOT NULL,
    mensagem TEXT NOT NULL,
    tipo TEXT NOT NULL,            -- 'enviada' ou 'recebida'
    status TEXT DEFAULT 'enviada',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

## 🚀 Como Executar

### Pré-requisitos
- Node.js 18+
- npm, yarn, pnpm ou bun

### Instalação
```bash
# Clonar o repositório
git clone <url-do-repositorio>
cd bioresonancia-agendamento

# Instalar dependências
npm install

# Executar em desenvolvimento
npm run dev
```

### Acesso
- **Aplicação**: http://localhost:3000
- **Página Inicial**: /
- **Agendamento**: /agendamento
- **Chatbot**: /chatbot
- **Admin**: /admin

## 📡 APIs Disponíveis

### Agendamentos
- `GET /api/agendamentos` - Listar agendamentos
- `POST /api/agendamentos` - Criar agendamento

### Pontos de Atendimento
- `GET /api/pontos-atendimento` - Listar pontos
- `POST /api/pontos-atendimento` - Criar ponto
- `GET /api/pontos-atendimento/[id]` - Buscar ponto específico
- `PUT /api/pontos-atendimento/[id]` - Atualizar ponto
- `DELETE /api/pontos-atendimento/[id]` - Excluir ponto

### WhatsApp (Simulado)
- `POST /api/whatsapp` - Processar mensagem
- `GET /api/whatsapp` - Buscar logs
- `PUT /api/whatsapp` - Enviar confirmação

## 🎯 Fluxo do Sistema

### 1. Agendamento Online
```
Cliente acessa /agendamento
↓
Preenche dados pessoais
↓
Seleciona ponto de atendimento
↓
Escolhe data e horário
↓
Confirma agendamento
↓
Recebe confirmação via WhatsApp
```

### 2. Chatbot
```
Cliente acessa /chatbot
↓
Interage com Dr. Silva (Naturopata)
↓
Recebe informações sobre biorressonância
↓
É direcionado para agendamento
```

### 3. Administração
```
Admin acessa /admin
↓
Visualiza dashboard
↓
Gerencia pontos de atendimento
↓
Monitora agendamentos
```

## 🤖 Persona do Chatbot

### Dr. Silva - Naturopata Sênior
- **Experiência**: 20+ anos em medicina integrativa
- **Especialidade**: Biorressonância e nanotecnologia
- **Tom**: Acolhedor, técnico quando necessário
- **Objetivo**: Educar e direcionar para agendamento

### Respostas Inteligentes
- Explicações sobre biorressonância
- Benefícios da nanotecnologia
- Orientações de preparo
- Direcionamento para agendamento
- Esclarecimento de dúvidas

## 🔧 Configurações de Deploy

### Replit
1. Importar projeto no Replit
2. Instalar dependências: `npm install`
3. Executar: `npm run dev`
4. Configurar porta 3000

### Vercel
```bash
# Deploy automático
vercel --prod

# Ou configurar no dashboard Vercel
```

### Variáveis de Ambiente (Futuras)
```env
# Para integração real com WhatsApp
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886

# Para email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password

# Para banco de dados em produção
DATABASE_URL=your_database_url
```

## 🎨 Design System

### Cores Principais
- **Azul**: `#2563eb` - Primária
- **Verde**: `#16a34a` - Saúde/Natureza
- **Roxo**: `#9333ea` - Admin
- **Cinza**: `#6b7280` - Texto secundário

### Tipografia
- **Font**: Inter (Google Fonts)
- **Tamanhos**: text-sm, text-base, text-lg, text-xl, text-2xl, text-3xl

### Componentes
- Cards com sombra sutil
- Botões com hover states
- Inputs com focus rings
- Tabelas responsivas
- Modais acessíveis

## 🧪 Testes

### Testes Manuais Recomendados
1. **Agendamento Completo**
   - Preencher formulário
   - Selecionar data/horário
   - Verificar confirmação

2. **Chatbot**
   - Testar diferentes perguntas
   - Verificar respostas contextuais
   - Testar direcionamento

3. **Admin**
   - Criar/editar/excluir pontos
   - Visualizar agendamentos
   - Testar filtros

4. **Responsividade**
   - Mobile (320px+)
   - Tablet (768px+)
   - Desktop (1024px+)

## 🔮 Próximas Funcionalidades

### Integrações Reais
- [ ] WhatsApp Business API (Twilio/Z-API)
- [ ] Envio de emails (SendGrid/Nodemailer)
- [ ] Google Maps para localização
- [ ] Pagamentos online

### Funcionalidades Avançadas
- [ ] Sistema de lembretes
- [ ] Histórico de exames
- [ ] Relatórios administrativos
- [ ] Multi-idiomas
- [ ] PWA (Progressive Web App)
- [ ] Notificações push

### Melhorias Técnicas
- [ ] Testes automatizados
- [ ] Cache Redis
- [ ] CDN para assets
- [ ] Monitoramento de performance
- [ ] Logs estruturados

## 📞 Suporte

Para dúvidas ou suporte:
- **Email**: suporte@bioresonancia.com
- **WhatsApp**: (11) 99999-9999
- **Documentação**: Este README

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

---

**Desenvolvido com ❤️ para revolucionar o agendamento de exames de biorressonância**
