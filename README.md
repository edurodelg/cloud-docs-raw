<div align="center">

# 📚 AI Documentation Archive

### Documentación técnica de servicios cloud en formato Markdown

[![Actualizado](https://img.shields.io/badge/Actualizado-2026-02-06%2017:08%20UTC-blue)]()
[![Archivos](https://img.shields.io/badge/Archivos-542-green)]()
[![Fuentes](https://img.shields.io/badge/Fuentes-13-orange)]()

*Listo para usar con NotebookLM, RAG, LLMs y más*

</div>

---

## 🎯 ¿Qué es esto?

Este repositorio contiene **documentación técnica oficial** de servicios cloud (AWS, Google Cloud, Azure, etc.) convertida a **Markdown limpio**, lista para usar en:

| Caso de uso | Descripción |
|-------------|-------------|
| 🧠 **[NotebookLM](https://notebooklm.google.com)** | Sube carpetas como fuentes para crear notebooks inteligentes |
| 🔍 **Sistemas RAG** | Alimenta pipelines de Retrieval Augmented Generation |
| 🤖 **LLMs locales** | Usa como contexto para modelos de lenguaje |
| 📴 **Consulta offline** | Accede a la documentación sin conexión |
| 🎯 **Búsqueda semántica** | Indexa con embeddings para búsqueda avanzada |

---

## 📊 Fuentes disponibles

| Fuente | Archivos | Documentación Original |
|--------|:--------:|------------------------|
| [aws-dynamodb-guide](./aws-dynamodb-guide/) | 39 | [Docs](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| [aws-ec2-guide](./aws-ec2-guide/) | 39 | [Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) |
| [aws-lambda-guide](./aws-lambda-guide/) | 39 | [Docs](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| [aws-s3-guide](./aws-s3-guide/) | 39 | [Docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html) |
| [azure-ai-foundry](./azure-ai-foundry/) | 45 | [Docs](https://learn.microsoft.com/en-us/azure/ai-foundry/) |
| [azure-aks](./azure-aks/) | 46 | [Docs](https://learn.microsoft.com/en-us/azure/aks/) |
| [azure-functions](./azure-functions/) | 43 | [Docs](https://learn.microsoft.com/en-us/azure/azure-functions/) |
| [gcp-bigquery-python](./gcp-bigquery-python/) | 50 | [Docs](https://cloud.google.com/python/docs/reference/bigquery/latest) |
| [gcp-cloud-run-python](./gcp-cloud-run-python/) | 37 | [Docs](https://cloud.google.com/python/docs/reference/run/latest) |
| [gcp-storage-python](./gcp-storage-python/) | 48 | [Docs](https://cloud.google.com/python/docs/reference/storage/latest) |
| [gcp-vertex-ai-python](./gcp-vertex-ai-python/) | 42 | [Docs](https://cloud.google.com/python/docs/reference/aiplatform/latest) |
| [google-adk-docs](./google-adk-docs/) | 46 | [Docs](https://google.github.io/adk-docs/) |
| [google-styleguide-python](./google-styleguide-python/) | 29 | [Docs](https://google.github.io/styleguide/pyguide.html) |

> **Total:** 542 archivos Markdown

---

## 🔧 Configuración

Cada fuente se procesa automáticamente con:

| Parámetro | Valor | Descripción |
|-----------|:-----:|-------------|
| `flatten` | ✅ | Todos los archivos al mismo nivel (sin subcarpetas) |
| `max_files` | ~50 | Consolidación automática si hay más archivos |
| `format` | `.md` | HTML → Markdown limpio |
| `incremental` | ✅ | Solo descarga páginas modificadas |

---

## 📥 ¿Necesitas otra fuente?

¡Las contribuciones son bienvenidas! 

**Opción 1:** [Abre un issue](https://github.com/edurodelg/cloudocs-scraper-/issues/new) con:
- URL de la documentación
- Nombre corto para la carpeta
- (Opcional) Filtros de versión

**Opción 2:** Fork + PR añadiendo la fuente en `sources.yaml`

---

## ⚙️ Generación automática

<table>
<tr>
<td width="60%">

Este repositorio se actualiza automáticamente usando el scraper [cloudocs-scraper](https://github.com/edurodelg/cloudocs-scraper-).

**Características:**
- ✅ Respeta `robots.txt` y `Crawl-delay`
- ✅ Solo documentación pública
- ✅ HTML → Markdown limpio
- ✅ Elimina UI/navegación
- ✅ Consolida archivos relacionados
- ✅ Detección de cambios via sitemaps

</td>
<td width="40%">

```
edurodelg/cloud-docs-raw/
├── README.md
├── adk-docs/
│   ├── agents.md
│   ├── tools.md
│   └── ...
├── aws-bedrock/
├── azure-search/
└── ...
```

</td>
</tr>
</table>

---

## 📝 Licencia

> ⚠️ **El contenido pertenece a sus respectivos propietarios** (Google, AWS, Microsoft, etc.)
> 
> Este repositorio facilita el acceso a documentación pública en un formato conveniente para herramientas de IA.

---

<div align="center">

**Creado por [Eduardo Rodelgo](https://www.linkedin.com/in/eduardo-rodelgo/)**

Generado con [cloudocs-scraper](https://github.com/edurodelg/cloudocs-scraper-)

</div>
