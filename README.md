[README (2).md](https://github.com/user-attachments/files/25461584/README.2.md)
# 🤖 APIs de IA Gratuitas — Guia Completo

> Repositório de referência para o vídeo **"Como usar APIs de IA Multimodal GRATUITAMENTE"**  
> Todas as ferramentas, links diretos, limites e exemplos de uso em um só lugar.

---

## 📌 Índice

- [🧠 Processamento de Texto (LLMs)](#-processamento-de-texto-llms)
- [🖼️ Geração de Imagens](#️-geração-de-imagens)
- [🎙️ Síntese e Clonagem de Voz](#️-síntese-e-clonagem-de-voz)
- [🎬 Geração de Vídeo com Avatares](#-geração-de-vídeo-com-avatares)
- [🔐 Boas Práticas de Segurança com Chaves](#-boas-práticas-de-segurança-com-chaves)
- [🔗 Todos os Links em um Lugar Só](#-todos-os-links-em-um-lugar-só)

---

## 🧠 Processamento de Texto (LLMs)

### 1. NVIDIA Build
**O que é:** Plataforma da NVIDIA que hospeda modelos open-source de ponta (Llama, Mistral, DeepSeek e mais) com inferência na nuvem.

**🔗 Link:** [https://build.nvidia.com](https://build.nvidia.com)

**Como obter a chave:**
1. Acesse o site e clique em **"Explorar"**
2. Escolha um modelo (ex: Llama 3.1 405B, DeepSeek R1)
3. Clique em **"Ver Código"** → **"Gerar Chave de API"**
4. Copie a chave imediatamente (não é exibida novamente)

**Limite gratuito:** ~4.000 créditos renováveis | Dezenas de requisições/minuto

**Exemplo de uso (Python):**
```python
from openai import OpenAI

client = OpenAI(
    base_url="https://integrate.api.nvidia.com/v1",
    api_key="SUA_CHAVE_NVIDIA_AQUI"
)

response = client.chat.completions.create(
    model="meta/llama-3.1-70b-instruct",
    messages=[{"role": "user", "content": "Analise este contrato..."}]
)
print(response.choices[0].message.content)
```

---

### 2. Ollama Cloud
**O que é:** Famoso por rodar modelos localmente, agora oferece acesso a modelos via API na nuvem, inclusive o poderoso GLM-4.

**🔗 Link:** [https://ollama.com](https://ollama.com)

**Como obter a chave:**
1. Crie uma conta no site
2. Vá em **Configurações → API Access (Cloud)**
3. Clique em **"Criar Chave"** e dê um nome descritivo
4. Na página de modelos, filtre pelos que têm a tag **"cloud"**

**Limite gratuito:** Uso gratuito com reset a **cada 2 horas** — ideal para lotes de processamento

**Exemplo de uso (terminal):**
```bash
ollama run glm4:cloud --api-key SUA_CHAVE_AQUI "Resuma este texto..."
```

---

### 3. Groq — Velocidade Extrema
**O que é:** Hardware proprietário (LPU) focado em inferência ultrarrápida. Resposta quase instantânea, essencial para assistentes de voz e atendimento telefônico.

**🔗 Link:** [https://console.groq.com](https://console.groq.com)

**Como obter a chave:**
1. Acesse o console e crie uma conta
2. No painel, clique em **"API Keys → Create Key"**
3. Defina nome e **data de expiração** (recomendado para segurança)
4. Complete a verificação e copie a chave

**Limite gratuito:** 30 requisições/minuto → milhares de chamadas/dia

**Compatibilidade:** 100% compatível com o padrão da OpenAI — só troque a `base_url`:
```python
from openai import OpenAI

client = OpenAI(
    base_url="https://api.groq.com/openai/v1",
    api_key="SUA_CHAVE_GROQ_AQUI"
)
```

---

### 4. GitHub Models (OpenAI, Microsoft e +)
**O que é:** Marketplace da Microsoft/GitHub com acesso gratuito a modelos como GPT-4o, Llama, Mistral e outros para desenvolvedores.

**🔗 Link:** [https://github.com/marketplace/models](https://github.com/marketplace/models)

**Como obter o token:**
1. Acesse o marketplace e escolha um modelo
2. Clique em **"Use this model"**
3. Crie um **Personal Access Token (PAT)**:
   - Confirme identidade (e-mail/2FA)
   - Defina nome e permissão **somente leitura** → apenas **"Models"**
4. O token começa com `github_pat_...`

**Limite gratuito:** 50–150 requisições/dia (varia por modelo)

**Exemplo de uso:**
```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://models.inference.ai.azure.com",
    api_key=os.environ["GITHUB_TOKEN"]
)
```

---

### 5. Google AI Studio (Gemini) — Rei do Volume
**O que é:** Interface e API gratuita do Google para os modelos Gemini. Maior cota gratuita disponível no mercado.

**🔗 Link:** [https://aistudio.google.com](https://aistudio.google.com)

**Como obter a chave:**
1. Acesse o site com sua conta Google
2. No menu esquerdo, clique em **"Get API Key"**
3. Vincule a um projeto Google Cloud (pode criar um novo ali mesmo)
4. A chave é gerada instantaneamente

**Limite gratuito:** 🔥 **1.000.000 tokens/dia** com Gemini Flash — ideal para processar documentos, contratos e bases de conhecimento inteiras

**Exemplo de uso:**
```python
import google.generativeai as genai

genai.configure(api_key="SUA_CHAVE_GEMINI_AQUI")
model = genai.GenerativeModel("gemini-1.5-flash")
response = model.generate_content("Responda baseado no manual anexo...")
```

---

### 6. OpenRouter — Agregador Universal
**O que é:** API única que dá acesso a quase todos os modelos do mundo. Evite dependência de fornecedor único — troque de modelo mudando apenas uma linha de código.

**🔗 Link:** [https://openrouter.ai](https://openrouter.ai)

**Como obter a chave:**
1. Crie uma conta
2. Clique em **"Get API Key"**
3. **Importante:** defina o limite de crédito como `$0` para usar apenas modelos gratuitos sem risco de cobrança acidental

**Modelos gratuitos:** Na página de modelos, filtre por **Price: $0/M tokens** — dezenas de opções disponíveis

**Exemplo de uso:**
```python
from openai import OpenAI

client = OpenAI(
    base_url="https://openrouter.ai/api/v1",
    api_key="SUA_CHAVE_OPENROUTER_AQUI"
)

response = client.chat.completions.create(
    model="mistralai/mistral-7b-instruct:free",  # Modelo gratuito
    messages=[{"role": "user", "content": "Sua mensagem aqui"}]
)
```

---

## 🖼️ Geração de Imagens

### 7. Cloudflare Workers AI
**O que é:** Rede global da Cloudflare com GPUs espalhadas pelo mundo. Rode Stable Diffusion via API sem servidor próprio.

**🔗 Link:** [https://dash.cloudflare.com](https://dash.cloudflare.com)

**Como configurar:**
1. Acesse o dashboard → **Computação e IA → Workers & Pages**
2. Crie um novo Worker (`api-geradora-imagens`)
3. Em **Configurações → Variáveis e Segredos**: adicione `API_KEY` com uma senha forte
4. Em **Bindings**: adicione um binding de Workers AI com a variável `AI`
5. Cole o script de geração de imagem no editor de código

**Worker script (exemplo):**
```javascript
export default {
  async fetch(request, env) {
    const authKey = request.headers.get("X-API-Key");
    if (authKey !== env.API_KEY) {
      return new Response("Unauthorized", { status: 401 });
    }
    
    const { prompt } = await request.json();
    const response = await env.AI.run(
      "@cf/stabilityai/stable-diffusion-xl-base-1.0",
      { prompt }
    );
    
    return new Response(response, {
      headers: { "Content-Type": "image/jpeg" }
    });
  }
};
```

**Limite gratuito:** Cota diária baseada em **neurônios computacionais** — dezenas de imagens/dia

---

### 8. Google Cloud Vertex AI (Imagen 3 + Veo)
**O que é:** Plataforma corporativa do Google com acesso ao Imagen 3 (fotos hiper-realistas) e Veo (geração de vídeos curtos).

**🔗 Link:** [https://console.cloud.google.com](https://console.cloud.google.com)

**Como configurar:**
1. Ative o **teste gratuito** (R$300 em créditos por 90 dias — cartão necessário, sem cobrança automática)
2. Crie um projeto e ative a **API do Vertex AI**
3. Vá em **APIs e Serviços → Credenciais → Criar Conta de Serviço**
4. Atribua o papel **"Usuário do Vertex AI"**
5. Gere e baixe a chave em formato **JSON**

**Exemplo de uso (Python):**
```python
import vertexai
from vertexai.vision_models import ImageGenerationModel

vertexai.init(project="SEU_PROJETO", location="us-central1")
model = ImageGenerationModel.from_pretrained("imagegeneration@006")

images = model.generate_images(
    prompt="Foto profissional de produto, xícara de café artesanal, fundo branco limpo",
    number_of_images=1
)
images[0].save(location="produto.png")
```

**Crédito gratuito:** $300 USD nos primeiros 90 dias → centenas de gerações de imagem e vídeo

---

## 🎙️ Síntese e Clonagem de Voz

### 9. LMNT
**O que é:** API de Text-to-Speech com vozes ultra-realistas e suporte a **clonagem de voz** a partir de apenas 30 segundos de áudio.

**🔗 Link:** [https://docs.lmnt.com](https://docs.lmnt.com) | [https://lmnt.com](https://lmnt.com)

**Como obter a chave:**
1. Crie uma conta em lmnt.com
2. Acesse **Dashboard → API Keys → Gerar Token**
3. Ao cadastrar, você recebe cota gratuita de caracteres imediatamente

**Síntese de voz (uso básico):**
```python
import requests

response = requests.post(
    "https://api.lmnt.com/v1/ai/speech",
    headers={"X-API-Key": "SUA_CHAVE_LMNT"},
    json={
        "text": "Bem-vindo à nossa empresa! Como posso te ajudar hoje?",
        "voice": "voice_id_do_catalogo",
        "format": "mp3"
    }
)

with open("audio.mp3", "wb") as f:
    f.write(response.content)
```

**Clonagem de voz (create-voice):**
```python
import requests

# Envie ~30s de áudio limpo para clonar uma voz
with open("voz_referencia.mp3", "rb") as audio_file:
    response = requests.post(
        "https://api.lmnt.com/v1/ai/voice",
        headers={"X-API-Key": "SUA_CHAVE_LMNT"},
        files={"file": audio_file},
        data={"name": "voz-ceo-empresa"}
    )

voice_id = response.json()["voice"]["id"]
print(f"Voice ID gerado: {voice_id}")
# Guarde este ID para usar em todas as sínteses futuras
```

**Casos de uso:**
- Atendimento telefônico automatizado com voz humana
- Podcasts e narração de artigos em escala
- Treinamentos em áudio com voz do especialista da equipe
- Mensagens personalizadas com voz do CEO

---

## 🎬 Geração de Vídeo com Avatares

### 10. HeyGen
**O que é:** Plataforma líder em geração de vídeos com avatares humanos digitais. Apresentador virtual, sincronia labial perfeita e movimentos naturais — tudo via API.

**🔗 Link:** [https://heygen.com](https://heygen.com) | [Docs API](https://docs.heygen.com)

**Como obter a chave:**
1. Crie uma conta (créditos gratuitos de teste incluídos)
2. Vá em **Configurações de Perfil → API / Desenvolvedores**
3. Clique em **"Gerar Token de Acesso"** e salve

**Fluxo de uso via API (2 etapas):**

**Etapa 1 — Listar avatares e vozes disponíveis:**
```python
import requests

headers = {"X-Api-Key": "SUA_CHAVE_HEYGEN"}

# Listar avatares
avatares = requests.get("https://api.heygen.com/v2/avatars", headers=headers).json()
avatar_id = avatares["data"]["avatars"][0]["avatar_id"]

# Listar vozes
vozes = requests.get("https://api.heygen.com/v2/voices", headers=headers).json()
voice_id = vozes["data"]["voices"][0]["voice_id"]
```

**Etapa 2 — Gerar o vídeo:**
```python
# Gerar vídeo com o roteiro
payload = {
    "video_inputs": [{
        "character": {
            "type": "avatar",
            "avatar_id": avatar_id,
            "avatar_style": "normal"
        },
        "voice": {
            "type": "text",
            "input_text": "Olá João! Seja bem-vindo à nossa plataforma. Vi que você atua no setor de saúde...",
            "voice_id": voice_id
        }
    }],
    "dimension": {"width": 1280, "height": 720}
}

response = requests.post(
    "https://api.heygen.com/v2/video/generate",
    headers={**headers, "Content-Type": "application/json"},
    json=payload
).json()

video_id = response["data"]["video_id"]
print(f"Vídeo em processamento: {video_id}")

# Consultar status (após alguns minutos)
status = requests.get(
    f"https://api.heygen.com/v1/video_status.get?video_id={video_id}",
    headers=headers
).json()

video_url = status["data"]["video_url"]
print(f"Vídeo pronto: {video_url}")
```

**Caso de uso avançado — Pipeline completo:**
> CRM recebe novo lead → Groq/Gemini escreve roteiro personalizado → HeyGen gera vídeo com avatar → E-mail automático com vídeo é enviado ao lead

---

## 🔐 Boas Práticas de Segurança com Chaves

```
⚠️  NUNCA commite chaves de API no GitHub
⚠️  Use sempre variáveis de ambiente (.env)
⚠️  Defina data de expiração nas chaves quando possível
⚠️  Use permissões mínimas necessárias (princípio do menor privilégio)
⚠️  Monitore o uso no dashboard de cada plataforma
```

**Configuração recomendada (.env):**
```bash
# .env — NUNCA suba este arquivo para o GitHub
NVIDIA_API_KEY=sua_chave_aqui
GROQ_API_KEY=sua_chave_aqui
GEMINI_API_KEY=sua_chave_aqui
OPENROUTER_API_KEY=sua_chave_aqui
GITHUB_TOKEN=sua_chave_aqui
LMNT_API_KEY=sua_chave_aqui
HEYGEN_API_KEY=sua_chave_aqui
```

**Carregar no Python:**
```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("GROQ_API_KEY")
```

**Instalar dotenv:**
```bash
pip install python-dotenv
```

---

## 🔗 Todos os Links em um Lugar Só

| Ferramenta | Categoria | Link | Limite Gratuito |
|---|---|---|---|
| NVIDIA Build | LLM (Texto) | [build.nvidia.com](https://build.nvidia.com) | ~4.000 créditos renováveis |
| Ollama Cloud | LLM (Texto) | [ollama.com](https://ollama.com) | Reset a cada 2 horas |
| Groq | LLM (Ultra-rápido) | [console.groq.com](https://console.groq.com) | 30 req/min |
| GitHub Models | LLM (OpenAI, etc) | [github.com/marketplace/models](https://github.com/marketplace/models) | 50–150 req/dia |
| Google AI Studio | LLM (Volume) | [aistudio.google.com](https://aistudio.google.com) | 1M tokens/dia |
| OpenRouter | LLM (Agregador) | [openrouter.ai](https://openrouter.ai) | Modelos gratuitos disponíveis |
| Cloudflare Workers AI | Imagem | [dash.cloudflare.com](https://dash.cloudflare.com) | Cota diária de neurônios |
| Google Vertex AI | Imagem + Vídeo | [console.cloud.google.com](https://console.cloud.google.com) | $300 em créditos (90 dias) |
| LMNT | Áudio / Voz | [lmnt.com](https://lmnt.com) | Cota gratuita de caracteres |
| HeyGen | Vídeo com Avatar | [heygen.com](https://heygen.com) | Créditos de teste incluídos |
| Tavus | Vídeo com Avatar | [tavus.io](https://www.tavus.io) | Créditos de teste incluídos |
                                           
---

## 💡 Pipeline Completo Sugerido

```
[Novo Lead no CRM]
       ↓
[Google AI Studio / Groq]
  Analisa dados e escreve roteiro personalizado
       ↓
[LMNT] → Sintetiza áudio com voz clonada
       ↓
[HeyGen] → Gera vídeo com avatar + roteiro + voz
       ↓
[E-mail automático] → Lead recebe vídeo personalizado
```

---

## 📺 Sobre este Repositório

Este repositório foi criado como material complementar para o vídeo sobre como usar APIs de IA multimodal gratuitamente.

Se este conteúdo te ajudou, considera:
- ⭐ Deixar uma estrela no repositório
- 🔔 Se inscrever no canal para mais conteúdos sobre IA e automação

---

*Última atualização: Fevereiro 2026*
