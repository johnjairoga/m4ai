# Sistema de Versionado de Archivos

## Política de Versionado Sincronizado con GitHub

**REGLA FUNDAMENTAL:** El número de versión en el nombre del archivo DEBE coincidir EXACTAMENTE con el tag/release en GitHub.

---

## Proceso Obligatorio para cada Cambio

Cada vez que se realice un cambio en un archivo conforme a los requerimientos del dueño:

### 1️⃣ Actualizar el archivo original
- Editar: `achei meu Apple.md` con los cambios solicitados

### 2️⃣ Crear copia versionada (sincronizada con GitHub)
- Crear: `achei meu Apple_v{X.Y.Z}.md`
- El número DEBE coincidir con el tag en GitHub
- Ejemplo: Si vamos a crear `v1.0.0` en GitHub → crear `achei meu Apple_v1.0.0.md`

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
VERSIÓN 1.0.0 (Inicial):
├─ GitHub tag: v1.0.0 ✅
├─ Archivo original: achei meu Apple.md
└─ Copia versionada: achei meu Apple_v1.0.0.md

VERSIÓN 1.1.0 (Petición 1 - Nueva sección):
├─ GitHub tag: v1.1.0 ✅
├─ Archivo original: achei meu Apple.md (actualizado)
└─ Copia versionada: achei meu Apple_v1.1.0.md

VERSIÓN 2.0.0 (Petición 2 - Cambio mayor):
├─ GitHub tag: v2.0.0 ✅
├─ Archivo original: achei meu Apple.md (actualizado)
└─ Copia versionada: achei meu Apple_v2.0.0.md
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
