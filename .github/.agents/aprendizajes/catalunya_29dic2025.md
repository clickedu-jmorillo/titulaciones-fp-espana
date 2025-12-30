# 📊 Aprendizajes del Dr. Indiana Jones - Catalunya (29/12/2025)

## 🗺️ Portal de Catalunya - Triaeducativa

### ✅ Información Verificada

**URL Principal**: `https://triaeducativa.gencat.cat/ca/fp/`

**Estructura del Portal:**
- Página principal de FP: `/ca/fp/`
- Listado de familias: `/ca/fp/families-professionals/`
- URLs de familias: `/ca/fp/families-professionals/{slug}/`

**Formato de Slugs:**
- Patrón general: `nombre-de-familia` (palabras en minúscula separadas por guiones)
- Ejemplo: `informatica-comunicacions`, `administracio-gestio`
- **Excepción detectada**: `installacio-manteniment` (doble 'l')

### 📚 Total de Familias Profesionales

**IMPORTANTE**: Catalunya tiene **24 familias profesionales**, no 26 como se pensaba inicialmente.

**Lista completa:**
1. Activitats Físiques i Esportives
2. Administració i Gestió
3. Agrària
4. Arts Gràfiques
5. Comerç i Màrqueting
6. Edificació i Obra Civil
7. Electricitat i Electrònica
8. Energia i Aigua
9. Fabricació Mecànica
10. Fusta, Moble i Suro
11. Hoteleria i Turisme
12. Imatge i So
13. Imatge Personal
14. Indústries Alimentàries
15. **Indústries Extractives** ← Nueva familia detectada 29/12/2025
16. Informàtica i Comunicacions
17. Instal·lació i Manteniment
18. Marítim-Pesquera
19. Química
20. Sanitat
21. Seguretat i Medi Ambient
22. Serveis Socioculturals i a la Comunitat
23. Tèxtil, Confecció i Pell
24. Transport i Manteniment de Vehicles

**Familias NO existentes en portal:**
- ❌ Arts i Artesanies (no aparece en el listado oficial)
- ❌ Vidre i Ceràmica (no aparece en el listado oficial)

### 🔍 Selectores y Estructura HTML

**Para extraer listado de familias:**
```bash
curl -s "https://triaeducativa.gencat.cat/ca/fp/families-professionals/" | \
grep -oP 'href="/ca/fp/families-professionals/[^"]*"' | sort -u
```

**Características del sitio:**
- Idioma: Catalán (ca-ES)
- Encoding: UTF-8
- Navegación: Estructura estática, no requiere JavaScript
- Método recomendado: requests + BeautifulSoup4 (más rápido que Playwright)

### 📋 Niveles de Titulaciones

**Estructura de niveles en Catalunya:**
- **FP Básica** (Grau bàsic) - CFGB
- **Grado Medio** (Grau mitjà) - CFGM
- **Grado Superior** (Grau superior) - CFGS
- **Cursos d'especialització**
- **Programes de formació i inserció**

**Patrones en URLs:**
- `/grau-basic/cicles/` → FP Básica
- `/grau-mitja/cicles/` → Grado Medio (también `cfgm`)
- `/grau-superior/cicles/` → Grado Superior (también `cfgs`)

### ⚠️ Problemas Comunes y Soluciones

**1. Error 404 en algunas familias:**
- Causa: Slug incorrecto o familia no existente
- Solución: Consultar listado oficial en `/families-professionals/`

**2. Titulaciones duplicadas:**
- Causa: La página incluye enlaces de navegación entre familias
- Solución: Filtrar enlaces que son nombres de familias profesionales

**3. Enlaces de navegación mezclados:**
- Patrón detectado: "Accedeix a Cicles", nombres de familias
- Solución: Validar que el nombre no sea navegación antes de incluir

### 🧪 Testing de Extracción

**Script de prueba rápida:**
```python
import requests
from bs4 import BeautifulSoup

url = "https://triaeducativa.gencat.cat/ca/fp/families-professionals/informatica-comunicacions/"
response = requests.get(url)
response.encoding = 'utf-8'
soup = BeautifulSoup(response.content, 'html.parser', from_encoding='utf-8')

# Extraer todos los enlaces
enlaces = soup.find_all('a', href=True)
for enlace in enlaces:
    if 'cicles' in enlace.get('href', ''):
        print(enlace.get_text(strip=True))
```

### 📊 Estadísticas de Extracción (29/12/2025)

**Completitud:** 24/24 familias (100%)
**Titulaciones totales:** 433 titulaciones válidas tras limpieza
**Tasa de éxito:** 100% en familias existentes

**Distribución estimada por nivel:**
- FP Básica: ~78 titulaciones
- Grado Medio: ~117 titulaciones
- Grado Superior: ~104 titulaciones
- Otros: ~134 titulaciones

### 🔄 Recomendaciones para Futuras Extracciones

1. **Siempre verificar** el listado oficial en `/families-professionals/` antes de extraer
2. **No asumir** que las 26 familias estándar existen en todas las CCAA
3. **Validar encoding UTF-8** en cada petición: `response.encoding = 'utf-8'`
4. **Filtrar navegación** antes de contar titulaciones
5. **Usar requests + BeautifulSoup** para Catalunya (no requiere Playwright)

### 🗓️ Última Actualización
**Fecha:** 29 de diciembre de 2025
**Verificado por:** Dr. Indiana Jones (vía Dr. René Belloq)
**Estado:** Portal funcional y estable
