# M4IA - Sistema de Versionado Sincronizado

Repositorio del proyecto M4IA con sistema automático de versionado sincronizado entre archivos locales y GitHub.

---

## 📋 Tabla de Contenidos

1. [Descripción General](#descripción-general)
2. [Estructura del Proyecto](#estructura-del-proyecto)
3. [Sistema de Versionado](#sistema-de-versionado)
4. [Cómo Funciona](#cómo-funciona)
5. [Acceso a Versiones](#acceso-a-versiones)
6. [Flujo de Trabajo](#flujo-de-trabajo)

---

## 📖 Descripción General

**M4IA** es un proyecto que mantiene un control de versiones detallado de todos los cambios realizados. Cada modificación crea automáticamente:

- ✅ Una **copia versionada del archivo** con el número de versión en el nombre
- ✅ Un **commit en git** documentando el cambio
- ✅ Un **tag en GitHub** sincronizando versiones
- ✅ Un **release en GitHub** para fácil acceso

**Objetivo:** Mantener historial completo y sincronizado de todos los cambios del proyecto.

---

## 📁 Estructura del Proyecto

```
M4IA/
│
├── README.md                    ← Este archivo
├── VERSIONADO.md               ← Documentación del sistema de versionado
│
├── Achei meu apple/            ← Loja: Achei Meu Apple
│   ├── achei meu Apple.md      ← Arquivo de trabalho (sempre atualizado)
│   ├── achei meu Apple_v1.0.0.md
│   ├── achei meu Apple_v1.1.0.md
│   ├── achei meu Apple_v1.1.1.md
│   ├── achei meu Apple_v1.1.2.md
│   ├── Prompt Original.md
│   └── CAMBIOS_PROMPT.md
│
├── Vetor Imports/              ← Loja: Vetor Imports
│   ├── Vetor Imports.md        ← Arquivo de trabalho (sempre atualizado)
│   ├── Vetor Imports_v1.0.0.md ← Versão inicial
│   ├── Prompt Original.md
│   └── CAMBIOS_PROMPT.md
│
├── .git/                        ← Repositorio git local
└── .gitignore                   ← (Si existe) archivos ignorados

```

### Explicación de Archivos

| Archivo | Descripción |
|---------|------------|
| `achei meu Apple.md` | **Archivo original** - siempre contiene la versión más reciente |
| `achei meu Apple_vX.Y.Z.md` | **Copias versionadas** - historial de cada versión |
| `VERSIONADO.md` | Documentación del proceso de versionado |
| `README.md` | Este archivo - guía completa del proyecto |

---

## 🏷️ Sistema de Versionado

### Convención de Versiones (Semántica)

Utilizamos **Versionado Semántico (SemVer)**: `vX.Y.Z`

```
vX.Y.Z
 │ │ └─ Z: Correcciones de errores (v1.0.1, v1.0.2)
 │ └─── Y: Nuevas características (v1.1.0, v1.2.0)
 └───── X: Cambios mayores (v2.0.0, v3.0.0)
```

### Ejemplos de Versionado

| Versión | Tipo de Cambio | Archivo |
|---------|---|---|
| v1.0.0 | Versión inicial | `achei meu Apple_v1.0.0.md` |
| v1.0.1 | Corrección de typos | `achei meu Apple_v1.0.1.md` |
| v1.1.0 | Nueva sección agregada | `achei meu Apple_v1.1.0.md` |
| v2.0.0 | Reestructuración mayor | `achei meu Apple_v2.0.0.md` |

---

## ⚙️ Cómo Funciona

### Flujo de Cambio (Paso a Paso)

```
┌─────────────────────────────────────────────────────────────┐
│ 1. PETICIÓN DEL DUEÑO                                        │
│    "Agregar nueva sección a achei meu Apple.md"             │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. EDITAR ARCHIVO ORIGINAL                                   │
│    achei meu Apple.md (se actualiza con los cambios)        │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. CREAR COPIA VERSIONADA                                    │
│    achei meu Apple_v1.1.0.md (nueva copia histórica)        │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. GIT COMMIT + PUSH                                          │
│    git commit -m "Nueva sección agregada"                   │
│    git push origin main                                      │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. CREAR TAG EN GITHUB                                       │
│    git tag -a v1.1.0 -m "Version 1.1.0: Nueva sección"      │
│    git push origin v1.1.0                                    │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│ 6. VERIFICACIÓN DE SINCRONIZACIÓN ✅                         │
│    - Archivo versionado en carpeta local                    │
│    - Archivo versionado en GitHub                           │
│    - Tag v1.1.0 visible en GitHub releases                  │
│    - Historial completo disponible                          │
└─────────────────────────────────────────────────────────────┘
```

### Sincronización = PRIORIDAD ABSOLUTA

**Regla Fundamental:** 
- Número en archivo = Número en tag de GitHub
- Si no coinciden → ERROR de sincronización

Ejemplo correcto:
```
✅ Archivo: achei meu Apple_v1.1.0.md
✅ Tag: v1.1.0
✅ GitHub Release: v1.1.0
→ TODO SINCRONIZADO
```

---

## 📍 Acceso a Versiones

### En tu Computadora (Local)

```bash
# Ver versión actual
ls "Achei meu apple/"

# Salida esperada:
# achei meu Apple.md (versión más reciente)
# achei meu Apple_v1.0.0.md (historial)
# achei meu Apple_v1.0.1.md (historial)
# achei meu Apple_v1.1.0.md (historial)
```

### En GitHub

1. **Ir a Releases:**
   - https://github.com/johnjairoga/m4ai/releases

2. **Ver todas las versiones:**
   - Cada versión tiene su tag (v1.0.0, v1.0.1, v1.1.0, etc.)
   - Cada tag es un punto en el tiempo del proyecto

3. **Descargar una versión específica:**
   ```bash
   # Clonar repositorio en una versión específica
   git clone --branch v1.1.0 https://github.com/johnjairoga/m4ai.git
   ```

---

## 🔄 Flujo de Trabajo

### Para Peticiones del Dueño

#### Paso 1: Recibir Petición
```
"Agregar validaciones de datos en achei meu Apple.md"
```

#### Paso 2: Determinar Tipo de Cambio

| Cambio | Versión | Ejemplo |
|--------|---------|---------|
| Corrección pequeña | Bump Z | v1.0.0 → v1.0.1 |
| Nueva característica | Bump Y | v1.0.0 → v1.1.0 |
| Cambio mayor | Bump X | v1.0.0 → v2.0.0 |

En este caso: **Nueva sección/validación** → Bump Y → **v1.1.0**

#### Paso 3: Ejecutar Cambio

```bash
# 1. Editar archivo original
# achei meu Apple.md → agregar validaciones

# 2. Crear copia versionada
cp "achei meu Apple.md" "achei meu Apple_v1.1.0.md"

# 3. Commit + Push
git add .
git commit -m "feat: Add data validations"
git push origin main

# 4. Crear tag
git tag -a v1.1.0 -m "Version 1.1.0: Add data validations"
git push origin v1.1.0

# 5. Verificar en GitHub
# → https://github.com/johnjairoga/m4ai/releases
```

#### Paso 4: Documentar Cambio
- ✅ Cambio registrado en archivo local
- ✅ Copia versionada disponible
- ✅ Tag visible en GitHub
- ✅ Release documentado

---

## 📊 Ejemplo de Historial Completo

```
VERSIÓN 1.0.0 (Inicial)
├─ Fecha: 29/05/2026
├─ GitHub Tag: v1.0.0
├─ Archivo: achei meu Apple_v1.0.0.md
└─ Descripción: Initial release

VERSIÓN 1.0.1 (Corrección)
├─ Fecha: 29/05/2026
├─ GitHub Tag: v1.0.1
├─ Archivo: achei meu Apple_v1.0.1.md
└─ Descripción: Fix typos and formatting

VERSIÓN 1.1.0 (Nueva característica)
├─ Fecha: 29/05/2026
├─ GitHub Tag: v1.1.0
├─ Archivo: achei meu Apple_v1.1.0.md
└─ Descripción: Add data validations section

VERSIÓN 2.0.0 (Cambio mayor)
├─ Fecha: TBD
├─ GitHub Tag: v2.0.0
├─ Archivo: achei meu Apple_v2.0.0.md
└─ Descripción: Complete restructure
```

---

## ✅ Checklist de Sincronización

Después de cada cambio, verificar:

- [ ] ¿Se actualizó `achei meu Apple.md`?
- [ ] ¿Se creó copia versionada `achei meu Apple_vX.Y.Z.md`?
- [ ] ¿Se hizo commit en git?
- [ ] ¿Se creó tag con número correcto?
- [ ] ¿Se hizo push a GitHub?
- [ ] ¿Aparece el tag en GitHub releases?
- [ ] ¿El número en archivo = número en tag?

---

## 🔗 Enlaces Importantes

| Recurso | URL |
|---------|-----|
| Repositorio | https://github.com/johnjairoga/m4ai |
| Releases | https://github.com/johnjairoga/m4ai/releases |
| Commits | https://github.com/johnjairoga/m4ai/commits/main |
| Documentation | Ver `VERSIONADO.md` |

---

## 📝 Notas Importantes

1. **El archivo original siempre debe estar actualizado** - `achei meu Apple.md` contiene la versión más reciente

2. **Las copias versionadas son históricas** - `achei meu Apple_vX.Y.Z.md` son snapshots de cada versión

3. **GitHub es la fuente de verdad** - Si hay duda, verificar en https://github.com/johnjairoga/m4ai/releases

4. **Sincronización es crítica** - Archivo + Tag deben tener el MISMO número

5. **Commits descriptivos** - Describir QUÉ cambió y POR QUÉ

---

## 🚀 Próximos Pasos

Esperando peticiones del dueño para:
- ✅ v1.0.1 - Correcciones menores
- ✅ v1.1.0 - Nuevas características
- ✅ v2.0.0 - Cambios mayores

---

**Última actualización:** 29/05/2026  
**Sistema:** Sincronización GitHub + Local  
**Estado:** ✅ Operativo
