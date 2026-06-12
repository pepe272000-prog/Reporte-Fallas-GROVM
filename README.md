# Sistema de Gestión de Fallas PMX/TIS — III Servicios

## 📋 Descripción General

Sistema web completo para reportar, validar, asignar y cerrar fallas de la flota de autotanques (PMX y TIS) de III Servicios, con integración a Google Sheets y notificaciones en tiempo real.

**5 módulos operativos:**
- 👷 Supervisor: Captura de fallas en cascada (Grupo → Categoría → Descripción)
- 🏢 Subgerente: Validación y definición de estatus operativo
- 🔧 Coordinador: Asignación de proveedor y ticket SISCO, cierre del día
- 📊 Gerencias: Dashboard con filtros, KPIs y exportación
- ✓ Cierre de turno: Evidencia fotográfica obligatoria, arrastre automático

## 🚀 Inicio Rápido

### Requisitos
- Cuenta Google (personal o corporativa)
- Google Sheets
- Google Apps Script
- Navegador moderno (Chrome, Edge, Firefox)

### Instalación en 5 pasos

#### 1️⃣ Crear la Google Sheet
1. Abre [Google Drive](https://drive.google.com)
2. Nueva → Google Sheets
3. Nómbrala: `III-Servicios-Fallas-DB`
4. **Copia el ID** de la URL (la parte larga entre `/d/` y `/edit`)

#### 2️⃣ Publicar el Apps Script
1. Abre [script.google.com](https://script.google.com)
2. Proyecto nuevo
3. Pega el contenido de `backend/AppScript_III_Servicios.gs`
4. En la línea 9, reemplaza:
   ```javascript
   var SHEET_ID = "TU_GOOGLE_SHEET_ID_AQUI";
   ```
   Con tu ID real (ej: `1a2b3c4d5e6f7g8h9i0j`)
5. **Guardar** → Implementar → Nueva implementación → App web
   - Ejecutar como: Tu cuenta
   - Acceso: Cualquier usuario
6. **Copia la URL** que genera (será algo como `https://script.google.com/macros/s/AKfycbx.../exec`)

#### 3️⃣ Conectar el HTML al backend
1. Abre `index.html` en un editor
2. Línea 1000 (busca `var WEBHOOK`):
   ```javascript
   var WEBHOOK = "https://script.google.com/macros/s/TU_WEBHOOK_URL_AQUI/exec";
   ```
3. Reemplaza `TU_WEBHOOK_URL_AQUI` con la URL del paso anterior
4. Guarda el archivo

#### 4️⃣ Publicar en GitHub Pages
1. Sube los archivos a tu repo `/docs` o raíz
2. En Settings → Pages → Deploy from branch: `main` (o la rama que uses)
3. El sitio estará disponible en `https://usuario.github.io/Reporte-Fallas-GROVM/`

#### 5️⃣ Probar
1. Abre el sitio en el navegador
2. Activa **MODO DEMO: ON** (botón esquina superior derecha)
3. Completa un flujo supervisor → subgerente → coordinador

---

## 📊 Catálogo de Fallas

**18 Grupos de Fallas** con **143 categorías** (subgrupos):

| Grupo | Categorías | Nota |
|-------|-----------|------|
| Aire Acondicionado | 6 | Incluye "Otro" |
| Cabina | 9 | Espejos, botonera, iluminación, cámara reversa |
| Carrocería | 12 | Defensas, escalera, rombos, tonel, siniestro |
| Dirección | 4 | Dura, fuga, pernos |
| Eje y Tren de Rodaje | 6 | Maza, cruceta, diferencial, quinta rueda |
| Embrague | 4 | Pedal, disco, ruido |
| Escape | 6 | Matachispas, tolva, tubo, fuga gases |
| Frenos | 6 | Balatas, matracas, ABS, sistema neumático |
| Llantas | 4 | Ponchadura, desgaste, reemplazo |
| Motor | 10 | Aceite, refrigeración, combustible, turbo, postratamiento, UREA, códigos |
| Sistema de Aire | 6 | Compresor, secador, manguera, freno estacionamiento |
| Sistema de Llenado por el Fondo | 14 | Sello, válvulas, caja, manómetros, manguera, sensor |
| Sistema Cuenta Litros | 7 | Pantalla TCS, válvula Betts, sonda, medidor directo |
| Sistema Eléctrico | 7 | Baterías, ABS, iluminación, velocímetro, acelerador |
| Suspensión | 7 | Bolsas aire, amortiguadores, muelles, pernos, válvula niveladora |
| Telemetría y Video | 6 | Cámara reversa, DMAS, botón emergencia, comunicación |
| Tonel / Compartimentos | 6 | Poro, soldadura, oxidación, calibración |
| Transmisión | 4 | Ruido, neutralización, cardan, palanca |

Cada grupo tiene opción **"Otro"** para fallas no catalogadas.

---

## 🔄 Flujo de Datos

```
SUPERVISOR captura falla
    ↓
SUBGERENTE valida + define estatus operativo
    ↓
COORDINADOR asigna proveedor + ticket SISCO
    ↓
GERENCIAS ven en dashboard en tiempo real
    ↓
SUPERVISOR cierra turno (con foto obligatoria)
    ↓
Órdenes abiertas se arrastran automáticamente al día siguiente
```

---

## 📁 Estructura del Repo

```
Reporte-Fallas-GROVM/
├── index.html                          # Sistema completo (desplegable en GH Pages)
├── backend/
│   └── AppScript_III_Servicios.gs      # Google Apps Script backend
├── docs/
│   ├── Catalogo_Fallas.xlsx            # Referencia de grupos/categorías
│   ├── Cronograma_GoLive.xlsx          # Plan de implementación
│   └── README.md                       # Este archivo
└── .gitignore                          # Excluir archivos locales
```

---

## 🧪 Modo Demo

El sistema incluye **Modo Demo** activable sin backend. Útil para:
- Entrenar supervisores sin conectar a Sheets
- Demostrar flujo a stakeholders
- Pruebas rápidas

Botón en esquina superior derecha: **MODO DEMO: ON/OFF**

---

## 🔌 Conectar WhatsApp (Siguiente Paso)

Aún no implementado. Cuando esté listo:
- WhatsApp Business API (Meta)
- Notificaciones en tiempo real al Subgerente, Coordinador, Gerencias
- Link directo al panel desde el mensaje

---

## 🛠️ Próximos Pasos

### Inmediato (Este Chat ✅)
- ✅ Catálogo FUO limpio (18 grupos, 143 categorías)
- ✅ Formulario supervisor con flujo 3-niveles
- ✅ 5 módulos operativos (supervisor, subgerente, coordinador, gerencias, cierre)
- ✅ Backend Apps Script completo
- ✅ Modo demo funcional
- ✅ Publicado en GitHub Pages

### Siguiente Chat 📱
1. **WhatsApp Business API — Notificaciones reales**
   - Integración Meta Cloud API
   - Mensajes a Subgerente, Coordinador, Gerencias
   - Links directos al panel
   - Templates de notificación

2. **Roles y Acceso**
   - Login simple o links por rol
   - Cada supervisor solo ve sus fallas
   - Subgerentes ven su terminal/grupo
   - Coordinadores y gerencias acceso completo

3. **Dashboard Gerencias Avanzado**
   - Gráficas: top 10 fallas, reincidencias
   - Tendencias mensuales por proveedor
   - SLA de cierre por turno
   - Reportes PDF automáticos

4. **PWA / App Móvil**
   - Instalable como app nativa
   - Funciona offline (sync cuando hay conexión)
   - Cámara integrada para evidencia fotográfica

---

## 📞 Soporte

- **Bugs o mejoras**: Abre un issue en GitHub
- **Preguntas técnicas**: Revisa la documentación en `/docs`
- **Para cambiar el catálogo**: Edita `Catalogo_Fallas.xlsx` y carga nuevamente

---

## 📄 Licencia

Uso interno III Servicios. No distribuir sin autorización.

---

**Versión**: 1.0  
**Última actualización**: Junio 2026  
**Estado**: Listo para producción (pendiente WhatsApp y roles)
