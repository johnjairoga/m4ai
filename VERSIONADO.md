# Sistema de Versionado de Archivos

## Política de Versionado Sincronizado con GitHub

**REGLA FUNDAMENTAL:** El número de versión en el nombre del archivo DEBE coincidir EXACTAMENTE con el tag/release en GitHub.

---

## Proceso Obligatorio para cada Cambio

Cada vez que se realice un cambio en un archivo conforme a los requerimientos del dueño:

### 1️⃣ Actualizar el archivo original
- **Achei meu Apple:** editar `Achei meu apple/achei meu Apple.md`
- **Vetor Imports:** editar `Vetor Imports/Vetor Imports.md`
- **iBest:** editar `ibest/iBest.md`
- **T2H:** editar `T2H/T2H.md`

### 2️⃣ Crear copia versionada (sincronizada con GitHub)
- **Achei meu Apple:** crear `achei meu Apple_v{X.Y.Z}.md`
- **Vetor Imports:** crear `Vetor Imports_v{X.Y.Z}.md`
- **iBest:** crear `iBest_v{X.Y.Z}.md`
- **T2H:** crear `T2H_v{X.Y.Z}.md`
- El número DEBE coincidir con el tag en GitHub
- Ejemplo: Si vamos a crear `v1.0.0` en GitHub → crear `Vetor Imports_v1.0.0.md`

### 3️⃣ Hacer commit en git
```bash
git add .
git commit -m "Descripción del cambio"
```

### 4️⃣ Crear tag en GitHub (MISMO NÚMERO)
```bash
git tag -a v1.0.0 -m "Version 1.0.0: Descripción"
git push origin main
git push origin v1.0.0
```

### 5️⃣ Verificar sincronización
- ✅ GitHub muestra el tag v1.0.0
- ✅ Repositorio tiene archivo `achei meu Apple_v1.0.0.md`
- ✅ Todo sincronizado

---

## Ejemplo de Flujo Sincronizado:

```
=== ACHEI MEU APPLE ===

VERSIÓN 1.0.0 (Inicial):
├─ GitHub tag: v1.0.0 ✅
├─ Archivo original: achei meu Apple.md
└─ Copia versionada: achei meu Apple_v1.0.0.md

VERSIÓN 1.1.0 → 1.1.2 (Mudanças do cliente):
├─ GitHub tags: v1.1.0, v1.1.1, v1.1.2 ✅
├─ Archivo original: achei meu Apple.md (actualizado)
└─ Copias versionadas: achei meu Apple_v1.1.0/1/2.md

=== VETOR IMPORTS ===

VERSIÓN 1.0.0 (Inicial - 02/06/2026):
├─ GitHub tag: vetor-v1.0.0 ✅
├─ Archivo original: Vetor Imports.md
└─ Copia versionada: Vetor Imports_v1.0.0.md

=== IBEST ===

VERSIÓN 1.0.0 (Inicial - 02/06/2026):
├─ GitHub tag: ibest-v1.0.0
├─ Archivo original: iBest.md
└─ Copia versionada: iBest_v1.0.0.md (a crear após primeiro prompt)

=== T2H ===

VERSIÓN 1.0.0 (Inicial - 02/06/2026):
├─ GitHub tag: t2h-v1.0.0
├─ Archivo original: T2H.md
└─ Copia versionada: T2H_v1.0.0.md (a crear após primeiro prompt)
```

---

## Convención de Versionado (Semver)

- **v1.0.0** → Versión inicial / cambios mayores
- **v1.0.1** → Correcciones de errores
- **v1.1.0** → Nuevas características / secciones
- **v2.0.0** → Cambios mayores que rompen versiones anteriores

---

## Verificación de Sincronización

Después de cada cambio, confirmar:

- [ ] ¿Existe el tag en GitHub? (https://github.com/johnjairoga/m4ai/releases)
- [ ] ¿Existe el archivo versionado en el repositorio?
- [ ] ¿El número en el archivo coincide con el número del tag?
- [ ] ¿Los cambios están en la rama `main`?

---

## Ventajas

- ✅ Historial completo y sincronizado
- ✅ Fácil comparar versiones entre GitHub y archivos locales
- ✅ Trazabilidad clara de cambios
- ✅ Acceso a cualquier versión anterior
- ✅ Releases visibles en GitHub
