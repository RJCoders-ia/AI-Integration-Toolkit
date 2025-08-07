# 🤖 AI Integration Toolkit

**Una colección completa de herramientas, scripts y templates para integrar IA en tus proyectos**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/Node.js-16+-green.svg)](https://nodejs.org/)
[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org/)
[![RJ Coders](https://img.shields.io/badge/Made%20by-RJ%20Coders-4A90E2.svg)](https://rjcoders.com)

## 🚀 ¿Qué incluye?

Este toolkit te proporciona todo lo necesario para comenzar a integrar IA en tus aplicaciones web de forma rápida y segura.

### 📦 Integraciones Disponibles

- **OpenAI GPT** - Generación de texto e imágenes
- **Anthropic Claude** - Conversaciones avanzadas y análisis
- **Google Gemini** - Multimodal AI y comprensión
- **Cohere** - Procesamiento de lenguaje natural
- **Stability AI** - Generación de imágenes

### 🛠️ Tecnologías

- **Node.js** - Integraciones backend
- **Python** - Scripts de procesamiento
- **React** - Componentes frontend
- **Express.js** - APIs RESTful

## 📁 Estructura del Proyecto

```
ai-integration-toolkit/
├── 📂 apis/
│   ├── openai/
│   ├── claude/
│   ├── gemini/
│   └── cohere/
├── 📂 components/
│   ├── chat-widget/
│   ├── image-generator/
│   └── text-analyzer/
├── 📂 templates/
│   ├── chatbot-template/
│   ├── content-generator/
│   └── document-analyzer/
├── 📂 scripts/
│   ├── batch-processing/
│   └── data-preparation/
└── 📂 examples/
    ├── simple-chat/
    ├── image-generation/
    └── document-qa/
```

## ⚡ Instalación Rápida

```bash
# Clonar el repositorio
git clone https://github.com/rjcoders/ai-integration-toolkit.git
cd ai-integration-toolkit

# Instalar dependencias Node.js
npm install

# Instalar dependencias Python
pip install -r requirements.txt

# Configurar variables de entorno
cp .env.example .env
# Edita .env con tus API keys
```

## 🔧 Configuración

### 1. Variables de Entorno

```bash
# .env
OPENAI_API_KEY=tu_openai_key
ANTHROPIC_API_KEY=tu_claude_key
GOOGLE_API_KEY=tu_gemini_key
COHERE_API_KEY=tu_cohere_key
STABILITY_API_KEY=tu_stability_key

# Configuración opcional
MAX_TOKENS=1000
TEMPERATURE=0.7
```

### 2. Configuración Básica

```javascript
// config/ai-config.js
const config = {
  openai: {
    model: 'gpt-4',
    maxTokens: 1000,
    temperature: 0.7
  },
  claude: {
    model: 'claude-3-sonnet-20240229',
    maxTokens: 1000,
    temperature: 0.7
  }
};

module.exports = config;
```

## 🎯 Casos de Uso

### 1. 💬 Chatbot Inteligente

```javascript
// examples/simple-chat/chatbot.js
const { OpenAIWrapper } = require('../../apis/openai');

const chatbot = new OpenAIWrapper();

async function processMessage(userMessage) {
  const response = await chatbot.chat([
    { role: 'system', content: 'Eres un asistente útil y amigable.' },
    { role: 'user', content: userMessage }
  ]);
  
  return response;
}

// Uso
processMessage('¿Cómo puedo integrar IA en mi web?')
  .then(response => console.log(response));
```

### 2. 🎨 Generador de Imágenes

```javascript
// examples/image-generation/generator.js
const { OpenAIWrapper } = require('../../apis/openai');

const imageGen = new OpenAIWrapper();

async function generateImage(prompt, style = 'realistic') {
  const enhancedPrompt = `${prompt}, ${style} style, high quality`;
  
  const image = await imageGen.generateImage({
    prompt: enhancedPrompt,
    size: '1024x1024',
    quality: 'hd'
  });
  
  return image.url;
}

// Uso
generateImage('Un logo moderno para una empresa tech')
  .then(imageUrl => console.log('Imagen generada:', imageUrl));
```

### 3. 📄 Analizador de Documentos

```python
# examples/document-qa/analyzer.py
from apis.claude.claude_wrapper import ClaudeWrapper

class DocumentAnalyzer:
    def __init__(self):
        self.claude = ClaudeWrapper()
    
    def analyze_document(self, document_text, questions):
        prompt = f"""
        Documento: {document_text}
        
        Preguntas:
        {chr(10).join(f"{i+1}. {q}" for i, q in enumerate(questions))}
        
        Proporciona respuestas detalladas basadas únicamente en el documento.
        """
        
        return self.claude.chat(prompt)

# Uso
analyzer = DocumentAnalyzer()
result = analyzer.analyze_document(
    "Tu documento aquí...",
    ["¿Cuáles son los puntos clave?", "¿Hay riesgos mencionados?"]
)
print(result)
```

## 🧩 Componentes React

### Chat Widget

```jsx
// components/chat-widget/ChatWidget.jsx
import React, { useState } from 'react';
import { useAI } from '../../hooks/useAI';

const ChatWidget = () => {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState('');
  const { sendMessage, loading } = useAI('openai');

  const handleSend = async () => {
    if (!input.trim()) return;
    
    const userMessage = { role: 'user', content: input };
    setMessages(prev => [...prev, userMessage]);
    setInput('');
    
    const response = await sendMessage(input);
    const aiMessage = { role: 'assistant', content: response };
    setMessages(prev => [...prev, aiMessage]);
  };

  return (
    <div className="chat-widget">
      <div className="messages">
        {messages.map((msg, idx) => (
          <div key={idx} className={`message ${msg.role}`}>
            {msg.content}
          </div>
        ))}
      </div>
      <div className="input-area">
        <input
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="Escribe tu mensaje..."
          onKeyPress={(e) => e.key === 'Enter' && handleSend()}
        />
        <button onClick={handleSend} disabled={loading}>
          {loading ? '...' : 'Enviar'}
        </button>
      </div>
    </div>
  );
};

export default ChatWidget;
```

## 📚 Templates de Prompts

```javascript
// templates/prompt-templates.js
const promptTemplates = {
  // Generación de contenido
  contentGeneration: {
    blog: `Escribe un artículo de blog sobre {topic} que incluya:
           - Introducción engaging
           - 3-5 puntos principales
           - Conclusión con call-to-action
           - Tono: {tone}
           - Audiencia: {audience}`,
    
    product: `Describe este producto: {product}
              - Beneficios clave
              - Características únicas
              - Por qué elegirlo
              - Llamada a la acción`
  },

  // Análisis de datos
  dataAnalysis: {
    summary: `Analiza estos datos y proporciona:
              - Resumen ejecutivo
              - Tendencias principales
              - Insights clave
              - Recomendaciones
              
              Datos: {data}`,
    
    comparison: `Compara {item1} vs {item2} en términos de:
                 - Ventajas y desventajas
                 - Casos de uso ideales
                 - Recomendación final`
  },

  // Desarrollo de software
  development: {
    codeReview: `Revisa este código y proporciona:
                 - Problemas de seguridad
                 - Optimizaciones posibles
                 - Mejores prácticas
                 - Sugerencias de refactoring
                 
                 Código: {code}`,
    
    documentation: `Genera documentación para esta función:
                    - Descripción clara
                    - Parámetros y tipos
                    - Ejemplos de uso
                    - Posibles errores
                    
                    Función: {function}`
  }
};

module.exports = promptTemplates;
```

## 🔒 Mejores Prácticas de Seguridad

### 1. Manejo Seguro de API Keys

```javascript
// utils/security.js
class SecurityManager {
  static validateApiKey(key) {
    if (!key || key.length < 20) {
      throw new Error('API key inválida');
    }
    return true;
  }

  static sanitizeInput(input) {
    // Limitar longitud
    if (input.length > 10000) {
      throw new Error('Input demasiado largo');
    }
    
    // Filtrar contenido peligroso
    const dangerousPatterns = [
      /system\s*:/i,
      /ignore\s+previous/i,
      /<script>/i
    ];
    
    for (const pattern of dangerousPatterns) {
      if (pattern.test(input)) {
        throw new Error('Input contiene contenido no permitido');
      }
    }
    
    return input.trim();
  }

  static rateLimit = new Map();
  
  static checkRateLimit(userId, maxRequests = 10, windowMs = 60000) {
    const now = Date.now();
    const userRequests = this.rateLimit.get(userId) || [];
    
    // Limpiar requests antiguos
    const validRequests = userRequests.filter(
      time => now - time < windowMs
    );
    
    if (validRequests.length >= maxRequests) {
      throw new Error('Rate limit excedido');
    }
    
    validRequests.push(now);
    this.rateLimit.set(userId, validRequests);
    
    return true;
  }
}

module.exports = SecurityManager;
```

### 2. Validación de Inputs

```javascript
// utils/validation.js
const Joi = require('joi');

const schemas = {
  chatMessage: Joi.object({
    message: Joi.string().min(1).max(1000).required(),
    model: Joi.string().valid('gpt-4', 'claude-3', 'gemini').required(),
    temperature: Joi.number().min(0).max(2).default(0.7),
    maxTokens: Joi.number().min(1).max(4000).default(1000)
  }),

  imageGeneration: Joi.object({
    prompt: Joi.string().min(1).max(500).required(),
    size: Joi.string().valid('512x512', '1024x1024').default('1024x1024'),
    style: Joi.string().valid('realistic', 'artistic', 'cartoon').default('realistic')
  })
};

function validateInput(data, schemaName) {
  const schema = schemas[schemaName];
  if (!schema) {
    throw new Error('Schema no encontrado');
  }
  
  const { error, value } = schema.validate(data);
  if (error) {
    throw new Error(`Validación fallida: ${error.details[0].message}`);
  }
  
  return value;
}

module.exports = { validateInput, schemas };
```

## 📊 Monitoreo y Analytics

```javascript
// utils/analytics.js
class AIAnalytics {
  constructor() {
    this.metrics = {
      requests: 0,
      errors: 0,
      totalTokens: 0,
      averageResponseTime: 0,
      modelUsage: new Map()
    };
  }

  logRequest(model, tokens, responseTime, success = true) {
    this.metrics.requests++;
    this.metrics.totalTokens += tokens;
    
    if (!success) {
      this.metrics.errors++;
    }
    
    // Actualizar tiempo promedio de respuesta
    this.metrics.averageResponseTime = 
      (this.metrics.averageResponseTime * (this.metrics.requests - 1) + responseTime) 
      / this.metrics.requests;
    
    // Registrar uso por modelo
    const currentUsage = this.metrics.modelUsage.get(model) || 0;
    this.metrics.modelUsage.set(model, currentUsage + 1);
  }

  getStats() {
    return {
      ...this.metrics,
      errorRate: (this.metrics.errors / this.metrics.requests * 100).toFixed(2) + '%',
      averageTokensPerRequest: Math.round(this.metrics.totalTokens / this.metrics.requests),
      modelUsage: Object.fromEntries(this.metrics.modelUsage)
    };
  }

  exportStats() {
    const stats = this.getStats();
    const report = `
# Reporte de Uso de IA

- **Total de requests:** ${stats.requests}
- **Tasa de error:** ${stats.errorRate}
- **Tokens promedio por request:** ${stats.averageTokensPerRequest}
- **Tiempo de respuesta promedio:** ${stats.averageResponseTime.toFixed(2)}ms

## Uso por modelo:
${Object.entries(stats.modelUsage).map(([model, count]) => 
  `- ${model}: ${count} requests`).join('\n')}

Generado el: ${new Date().toISOString()}
    `;
    
    return report;
  }
}

module.exports = AIAnalytics;
```

## 🚀 Deployment

### Docker

```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

# Copiar package files
COPY package*.json ./
RUN npm ci --only=production

# Copiar código fuente
COPY . .

# Crear usuario no-root
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nextjs -u 1001
USER nextjs

EXPOSE 3000

CMD ["npm", "start"]
```

### Docker Compose

```yaml
# docker-compose.yml
version: '3.8'

services:
  ai-toolkit:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - OPENAI_API_KEY=${OPENAI_API_KEY}
      - ANTHROPIC_API_KEY=${ANTHROPIC_API_KEY}
    volumes:
      - ./logs:/app/logs
    restart: unless-stopped

  redis:
    image: redis:alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    restart: unless-stopped

volumes:
  redis_data:
```

## 📖 Documentación de APIs

### Endpoints Disponibles

```javascript
// Documentación de la API REST

/**
 * POST /api/chat
 * Envía un mensaje al modelo de IA seleccionado
 */
{
  "message": "string (required)",
  "model": "openai|claude|gemini (required)",
  "temperature": "number (0-2, optional)",
  "maxTokens": "number (1-4000, optional)"
}

/**
 * POST /api/images/generate
 * Genera una imagen basada en un prompt
 */
{
  "prompt": "string (required)",
  "size": "512x512|1024x1024 (optional)",
  "style": "realistic|artistic|cartoon (optional)"
}

/**
 * POST /api/analyze/document
 * Analiza un documento y responde preguntas
 */
{
  "document": "string (required)",
  "questions": "array of strings (required)",
  "model": "claude|gemini (optional)"
}

/**
 * GET /api/stats
 * Obtiene estadísticas de uso
 */
// Response: objeto con métricas de uso
```

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Por favor:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/amazing-feature`)
3. Commit tus cambios (`git commit -m 'Add amazing feature'`)
4. Push a la rama (`git push origin feature/amazing-feature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver `LICENSE` para más detalles.

## 🙏 Agradecimientos

- [OpenAI](https://openai.com/) - API de GPT y DALL-E
- [Anthropic](https://anthropic.com/) - API de Claude
- [Google](https://ai.google/) - API de Gemini
- [Cohere](https://cohere.ai/) - API de procesamiento de lenguaje

## 📞 Soporte

¿Necesitas ayuda? Contáctanos:

- 🌐 **Website:** [rjcoders.com](https://rjcoders.com)
- 📧 **Email:** hola@rjcoders.com
- 💼 **LinkedIn:** [RJ Coders](https://linkedin.com/company/rjcoders)

---

<div align="center">

**Hecho con ❤️ por [RJ Coders](https://rjcoders.com)**

*Transformamos ideas en soluciones digitales*

</div>
