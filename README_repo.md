# Dashboard de Operaciones · Cumplimiento de SLA

> Adiós a los dashboards aburridos: un tablero que **narra la historia de tu operación**, la defiende y la convierte en decisión.

Dashboard interactivo, en un solo archivo HTML, que monitorea el cumplimiento de SLA de un portafolio logístico B2B. No solo grafica: **interpreta** (Smart Narratives), **diagnostica**, **gobierna la decisión** (umbral · dueño · decisión) y permite **preguntar a los datos en lenguaje natural**.

Pieza demostrativa del ejercicio **“Métricas y eficiencia operativa”** — parte del método de [javierforero.co](https://javierforero.co).

**▶️ Demo en vivo:** `https://jaforero.github.io/dashboard-sla/`
_(disponible una vez publiques GitHub Pages — ver más abajo)_

---

## ✨ Qué incluye

- **8 pestañas navegables:** Resumen ejecutivo · Salud · Eficiencia · Riesgo · Predicción · **Diagnóstico** · **Gobernanza** · **Q&A · IA**.
- **Smart Narratives:** narrativa ejecutiva generada dinámicamente desde los datos (resumen, hallazgos, riesgos, recomendaciones).
- **Filtros globales:** región · tipo de cliente · rango de meses. Todo el tablero reacciona al instante.
- **Alertas automáticas:** 🔴 caída > 5 pp bajo la base de 12 meses · 🟡 brecha del trimestre negativa · 🟠 dato desactualizado (frescura).
- **Gobernanza editable:** umbral, dueño y decisión por indicador, con exportar/importar (JSON). Un KPI sin dueño no entra al tablero.
- **Diagnóstico del quiebre:** descompone el evento de Ene 2026 con hipótesis de causa y un veredicto que **bloquea el escalamiento** hasta cerrar la causa.
- **Q&A · IA conversacional:** preguntas en lenguaje natural con respuesta **anclada a los datos** (determinista, sin alucinación) y “soporte de datos” visible.
- **One-pager DATA → IDEA → DECISIÓN:** brief imprimible del filtro activo, habilitado tras la validación humana (Correctitud · Contexto · Consecuencias).
- **Marca Javier Forero:** tipografía IgraSans, paleta oficial, **tema claro/oscuro**.
- **Funciona offline:** versión con Plotly embebido (`dashboard-offline.html`), sin ninguna descarga externa.

---

## 🧠 Marco conceptual (POVs del autor)

Este tablero es una demostración viva de tres ideas de [javierforero.co](https://javierforero.co/category/2-analitica/):

| POV | Cómo se ve en el tablero |
|---|---|
| [Analítica de Datos en 5 Niveles](https://javierforero.co/2026/01/26/analitica-datos-5-niveles/) | Recorre los 5 niveles: **Salud** (descriptivo) → **Diagnóstico** (diagnóstico) → **Predicción** (predictivo) → **Gobernanza** (prescriptivo) → **Q&A** (cognitivo). |
| [¡Adiós a los dashboards aburridos! IA conversacional](https://javierforero.co/2024/02/02/ia-conversacional-revoluciona-dashboards-analitica/) | La pestaña **Q&A**: preguntar a los datos en lenguaje natural, con el dato bien preparado y el humano en control. |
| [PULSE: decidir mejor que tu competencia](https://javierforero.co/2026/06/30/pulse-decidir-mejor-con-datos/) | **Gobernanza** (umbral y dueño por decisión), **frescura** del dato (velocidad) y el **brief** de decisión. |

> “La analítica no falla por falta de modelos, falla por falta de criterio.” — Javier Forero

---

## 📁 Estructura del repositorio

```
dashboard-sla/
├── index.html                 # Dashboard (entrada de GitHub Pages). Plotly vía CDN.
├── dashboard-offline.html      # Versión 100% autónoma (Plotly embebido) para uso offline.
├── data/
│   ├── cumplimiento_sla_tidy.csv          # Dataset (formato tidy, 570 filas)
│   └── diccionario_datos_...csv           # Diccionario de datos
├── assets/fonts/IgraSans.otf   # Tipografía de marca (también va embebida en el HTML)
├── .nojekyll                   # Sirve los archivos tal cual en GitHub Pages
├── LICENSE                     # MIT (el código)
└── README.md
```

---

## 🚀 Publicar en GitHub Pages

### Opción A — desde la web (sin consola)
1. Crea un repositorio nuevo en tu cuenta: **`dashboard-sla`** (público).
2. En la página del repo → **Add file → Upload files** → arrastra **todo el contenido** de esta carpeta (no la carpeta, sino sus archivos/subcarpetas) → **Commit changes**.
3. Ve a **Settings → Pages**.
4. En **Build and deployment → Source**, elige **Deploy from a branch**.
5. En **Branch**, selecciona **`main`** y carpeta **`/ (root)`** → **Save**.
6. Espera ~1 minuto y recarga. Tu demo quedará en:
   **`https://jaforero.github.io/dashboard-sla/`**

### Opción B — desde consola (Git)
```bash
# dentro de esta carpeta
git init
git add .
git commit -m "Dashboard SLA interactivo — demo"
git branch -M main
git remote add origin https://github.com/jaforero/dashboard-sla.git
git push -u origin main
```
Luego repite los pasos 3–6 de la Opción A (Settings → Pages).

> El archivo `.nojekyll` ya está incluido para que GitHub Pages sirva el HTML sin procesarlo con Jekyll.

---

## 💻 Uso local
- **La forma simple:** abre `dashboard-offline.html` con doble clic. Funciona sin internet.
- **`index.html`** requiere conexión la primera vez (carga Plotly desde CDN, con respaldo multi-CDN).
- Para servirlo localmente igual que en producción:
  ```bash
  python3 -m http.server 8000
  # abre http://localhost:8000
  ```

---

## 📊 Sobre los datos
- **`cumplimiento_sla_tidy.csv`** — 570 filas (38 rutas × 15 meses, Ene 2025–Mar 2026), 8 regiones, 4 tipos de cliente, sin valores faltantes. Columnas: `ruta, mes, region, ciudad_origen, tipo_cliente, sla_objetivo_pct, cumplimiento_pct, brecha_pp`.
- Los datos están **embebidos** en el HTML (el CSV se incluye solo para transparencia y reproducibilidad).
- ⚠️ **Datos sintéticos / de ejemplo.** No representan operaciones ni clientes reales. Antes de publicar cualquier variante con datos propios, verifica que no sean confidenciales.

---

## 🛠️ Tecnología
- HTML + CSS (variables) + JavaScript **vanilla**, sin framework ni build.
- [Plotly.js](https://plotly.com/javascript/) 2.35.2 (MIT) para las gráficas.
- Q&A: motor local determinista de consulta en lenguaje natural (sin dependencias). El “upgrade” generativo opcional requiere backend/clave, por lo que **en GitHub Pages responde el motor local** (sin exponer credenciales).

---

## 👤 Autor
**Javier Forero** — Consultor en Analítica, IA y Transformación Digital.
🔗 [javierforero.co](https://javierforero.co) · [LinkedIn](https://www.linkedin.com/in/jforero/) · [GitHub](https://github.com/jaforero)

## 📄 Licencia
Código bajo **MIT** (ver `LICENSE`). La tipografía IgraSans es propiedad de su titular y no forma parte de la licencia del código.
