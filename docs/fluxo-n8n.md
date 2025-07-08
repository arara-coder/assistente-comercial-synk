# ⚙️ Documentação do Fluxo Experimental — Typebot + n8n + OpenAI

Este documento descreve o fluxo experimental criado utilizando **Typebot** conectado ao **n8n** e integrado à **API da OpenAI**. Embora este não tenha sido o fluxo final utilizado, ele foi documentado como parte do processo de aprendizado e exploração técnica.

---

## 🧭 Objetivo

- Testar a integração entre Typebot → Webhook (n8n) → OpenAI API
- Processar as informações recebidas do usuário e retornar uma resposta personalizada gerada por IA

---

## 🧩 Estrutura do Workflow no n8n

1. **Webhook Node**
   - Método: `POST`
   - Endpoint customizado para receber os dados do Typebot
   - Parâmetros: `nome`, `empresa`, `produto`

2. **Function Node**
   - Formata os dados recebidos para gerar o prompt para a IA
```js
return [{
  prompt: `Você é um assistente comercial da Synk, empresa focada em automação e IA.
Empresa cliente: ${$json["empresa"]}
Produto interesse: ${$json["produto"]}
Crie uma resposta comercial profissional, acolhedora e personalizada.`
}];
```

3. **OpenAI Node**
   - Modelo: `gpt-3.5-turbo`
   - Input: prompt gerado anteriormente
   - Retorno: resposta gerada pela IA

4. **Response Node**
   - Retorna o texto para o Typebot via Webhook Response

---

## 🔍 Desafios Identificados

- O retorno do OpenAI vinha encapsulado em objetos e metadados complexos
- Foi necessário usar o **Function Node** para estruturar o prompt corretamente
- Em alguns testes, o tempo de resposta excedia o limite do Typebot

---

## 💡 Aprendizados Técnicos

- Tratamento de dados JSON no n8n
- Estruturação de prompts dinâmicos com base em input do usuário
- Estratégias de fallback e uso do `Webhook Response` para devolver apenas o essencial

---

## 📎 Importação
O workflow completo pode ser importado no n8n com o seguinte arquivo:

📁 `config/n8n-workflow.json`

---

## 🧪 Observação Final
Este experimento foi essencial para compreender os limites e possibilidades da integração entre Typebot e n8n. Mesmo optando por seguir com uma abordagem mais direta (Typebot + OpenAI), decidi manter e documentar o fluxo n8n como referência técnica para futuros projetos.

Documentado com 💚 por Lídi — explorando possibilidades com curiosidade e propósito.
