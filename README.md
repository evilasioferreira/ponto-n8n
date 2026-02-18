# ⏱️ Auditoria Automática de Ponto Eletrônico (n8n + Tangerino)

Automação desenvolvida em **n8n** para auditar registros de ponto eletrônico, identificar **omissões**, **horas extras excessivas** e **intervalos intrajornada irregulares**, com **disparo automático de e-mails** para colaboradores e gestores.

Projeto criado para reduzir trabalho manual do DHO e garantir **conformidade com a CLT**, sem precisar virar fiscal 24/7.

---

## 🎯 Objetivo

Automatizar a análise diária do ponto eletrônico para:

- Identificar **falta de registro de ponto**
- Detectar **extrapolação de horas extras**
- Verificar **intervalo intrajornada inferior a 60 minutos**
- Diferenciar regras para:
  - Jornada **8h (Seg–Sex)**
  - Jornada **12x36 (Plantão)**
- Notificar automaticamente:
  - Colaborador
  - Gestor imediato
  - DHO (cópia e auditoria)

---

## 🧠 Visão Geral da Automação

A automação executa em horários programados e segue o fluxo abaixo:

1. **Cron (Agendamento)**
2. **Consulta à API da Tangerino**
3. **Tratamento e normalização dos dados**
4. **Regras de validação**
5. **Identificação de desvios**
6. **Disparo de e-mails automáticos**
7. **Controle de envio com `Wait` e `Split In Batches`**

Tudo pensado para escalar sem virar gargalo.

---

## 🔄 Regras Implementadas

### 📌 Omissão de Registro
- Entrada, almoço, retorno ou saída ausente
- Disparo automático para o colaborador
- Cópia para DHO

---

### ⏰ Horas Extras
- Jornada **8h** → alerta acima de **2h extras**
- Jornada **12h** → cálculo ajustado
- Alerta educativo + respaldo legal (Art. 59 CLT)

---

### 🍽️ Intervalo Intrajornada
- Intervalo inferior a **60 minutos**
- Alerta com base no **Art. 71 da CLT**
- Disparo automático

---

## 🗂️ Estrutura do Workflow

### Bases Tratadas Separadamente
- **Base 8h (Seg–Sex)**
- **Base 12h (Plantão)**

### Principais Nodes
- `Cron`
- `HTTP Request` (API Tangerino)
- `Code` (tratamento e regras)
- `IF` (validações)
- `Split Out / Split In Batches`
- `Wait`
- `Microsoft Outlook`

---

## 🔐 Integrações Utilizadas

- **Tangerino API**
- **Microsoft Outlook (OAuth2)**
- **Microsoft Excel Online**
  - Base de colaboradores
  - Associação colaborador → gestor

---

## 🕘 Agendamentos

- Execução principal: **Quarta a Domingo**
- Análise retroativa:
  - Ex: Dia 07 → analisa registros do dia 05
- Fluxo separado para **Plantonistas**

Timezone configurado:  
`America/Sao_Paulo`

---

## 📧 Comunicação

Os e-mails são:
- Educativos
- Baseados em legislação
- Com linguagem profissional e clara
- Enviados automaticamente com controle de volume

---

## ⚠️ Observações Importantes

- Credenciais sensíveis **não devem ser versionadas**
- Recomenda-se uso de variáveis de ambiente no n8n
- Workflow pode ser facilmente adaptado para:
  - WhatsApp
  - Teams
  - Slack
  - Webhooks externos

---

## 🚀 Próximos Passos (Roadmap)

- [ ] Intervalo **interjornada**
- [ ] Resumo diário para gestores
- [ ] Disparo via **Microsoft Teams**
- [ ] Dashboard de indicadores (SLI / SLO de jornada)

---

## 🧩 Tags

`n8n` `automação` `rh` `dho` `ponto-eletrônico` `tangerino` `compliance` `clt`

---

## 👨‍💻 Autor

**Evilásio Ferreira**  
Automação • n8n • APIs • IA  
*"Automatizar o chato para sobrar tempo pro estratégico."*
