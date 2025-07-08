# 📘 Documentação do Fluxo — Typebot + OpenAI

Este documento descreve o fluxo conversacional funcional implementado com **Typebot** integrado à **API da OpenAI**, utilizado no assistente comercial da Synk.

---

## 🔧 Visão Técnica Geral

O fluxo foi desenvolvido diretamente no construtor visual do Typebot, utilizando:

- **Blocos interativos** para coletar dados (Nome, Empresa, Produto)
- **Webhook HTTP** para enviar os dados coletados à API da OpenAI
- **Blocos de resposta dinâmica** para exibir o retorno da IA
- **Fallbacks** para possíveis erros de requisição

---

## 🧩 Estrutura dos Blocos no Typebot

1. **Start**
   - Boas-vindas com tom acolhedor e emojis
   - Introdução ao assistente comercial da Synk

2. **Perguntas ao usuário**
   - `Nome` → Input de texto livre
   - `Empresa` → Input de texto livre
   - `Produto ou serviço de interesse` → Input de texto livre

3. **Webhook HTTP**
   - URL configurada apontando para endpoint externo (simulado localmente com serviços como n8n ou Make, ou um endpoint simples hospedado)
   - Método: POST
   - Payload contendo nome, empresa e produto do usuário

4. **Resposta da IA**
   - Bloco de texto dinâmico que apresenta a resposta gerada pela OpenAI
   - Mensagem inclui tom profissional, personalizado e uma call-to-action

5. **Encerramento**
   - Agradecimento e orientação sobre próximos passos

---

## 📥 Exemplo de Payload Enviado para OpenAI
```json
{
  "nome": "João",
  "empresa": "TechBR",
  "produto": "Plataforma de automação"
}
```

### Prompt enviado via backend:
```js
const prompt = `
Você é um assistente comercial da Synk, empresa focada em automação e IA.
Empresa cliente: TechBR
Produto interesse: Plataforma de automação
Crie uma resposta comercial profissional, acolhedora e personalizada.`
```

---

## 💬 Exemplo de Resposta Gerada

> Olá, João! Obrigado por entrar em contato com a Synk. Agradecemos o seu interesse na nossa plataforma de automação! Ela foi desenvolvida para simplificar fluxos e potencializar resultados com eficiência e inteligência artificial. Posso te encaminhar um material mais detalhado ou agendar um atendimento personalizado. Como prefere seguir?

---

## ✅ Fallbacks e Respostas Alternativas
- Caso ocorra falha no webhook:
  - Mensagem amigável: "Tivemos um problema técnico ao gerar sua resposta, mas já estamos verificando! Você pode tentar novamente em instantes."

---

## 📎 Importação
O fluxo completo pode ser importado no Typebot através do arquivo:

📁 `config/fluxo-typebot.json`

---

## 🌿 Observação Final
Este foi meu **primeiro contato com o Typebot**, explorando seus recursos com foco em criar uma experiência útil, agradável e alinhada com as diretrizes do teste. A documentação foi elaborada com o mesmo cuidado, garantindo transparência, organização e reusabilidade do fluxo.

Feito com 💚 por Lídi — com atenção a cada detalhe.
