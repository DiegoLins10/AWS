## 🌐 WebSocket no API Gateway (DVA-C02)

👉 **WebSocket API** no API Gateway permite comunicação **bidirecional em tempo real** entre cliente e servidor.

---

## 🧠 Conceito rápido

👉 Diferente do HTTP:

* HTTP = request → response (curto, stateless)
* WebSocket = conexão **persistente (aberta)**

📌 Ou seja:

* Cliente conecta uma vez
* Depois **ambos podem enviar mensagens a qualquer momento**

---

## ⚙️ Como funciona no AWS

### 🔌 Conexão

1. Cliente conecta via WebSocket
2. API Gateway cria um **connectionId**
3. Essa conexão fica ativa

---

### 🧩 Rotas (Routes)

Você define rotas baseadas em eventos:

* `$connect` → quando conecta
* `$disconnect` → quando desconecta
* `$default` → fallback
* Rotas custom (ex: `sendMessage`)

---

### 🔗 Integração

Normalmente com:

* **Lambda** (mais comum)
* DynamoDB (guardar conexões)
* Outros serviços AWS

---

## 🔥 Exemplo de fluxo

1. Cliente conecta (`$connect`)
2. Salva `connectionId` no DynamoDB
3. Cliente envia mensagem
4. Lambda processa
5. Lambda responde usando:

   ```
   @connections API
   ```

---

## 📡 Enviar mensagem de volta

👉 Usa endpoint especial do API Gateway:

```
POST /@connections/{connectionId}
```

---

## 🧠 Casos de uso (cai na prova)

* Chat em tempo real 💬
* Notificações instantâneas 🔔
* Jogos online 🎮
* Dashboards live 📊

---

## ⚠️ Diferença HTTP vs WebSocket (DECORAR)

| Feature     | HTTP API         | WebSocket API           |
| ----------- | ---------------- | ----------------------- |
| Comunicação | Request/Response | Bidirecional            |
| Conexão     | Curta            | Persistente             |
| Tempo real  | ❌                | ✅                       |
| Estado      | Stateless        | Stateful (connectionId) |

---

## ⚠️ Pegadinhas de prova

* 🔥 WebSocket mantém conexão aberta
* 🔥 Usa `connectionId`
* 🔥 Pode enviar mensagem **sem novo request do cliente**
* 🔥 Precisa gerenciar conexões (ex: DynamoDB)

---

## 🚀 Resumo final

👉 WebSocket API = **tempo real + conexão persistente**

* Conecta → ganha `connectionId`
* Rotas: `$connect`, `$disconnect`, `$default`
* Backend (Lambda) pode enviar mensagens de volta

---

Se quiser, posso te mandar:
👉 3 questões estilo prova só sobre WebSocket (esse tema às vezes aparece como pegadinha)
