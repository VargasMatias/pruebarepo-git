#  Documentación del Microservicio: bdget

Este repositorio contiene la base de código del microservicio **bdget** , el cual ha sido estructurado y preparado bajo la cultura DevOps para optimizar y agilizar la entrega continua del software . El propósito principal de esta estructura es eliminar las barreras de comunicación y compatibilidad tecnológica entre los equipos de desarrollo y operaciones, asegurando un flujo de trabajo claro, automatizado y continuo desde el desarrollo hasta la producción .

La importancia de este documento radica en que:
- **Facilita la colaboración:** Permite que cualquier miembro del equipo de desarrollo entienda rápidamente el propósito y la estructura organizativa del proyecto .
- **Aumenta el mantenimiento:** Al contar con instrucciones y flujos claros, resulta más sencillo actualizar, escalar o corregir el código de la aplicación .
- **Ayuda a nuevos integrantes:** La curva de aprendizaje de nuevos desarrolladores disminuye notablemente al contar con este recurso técnico de referencia clara .
- **Proporciona claridad:** Detalla de manera concisa los objetivos, dependencias y pasos necesarios para trabajar diariamente con el proyecto .

---

##  Justificación del Modelo de Trabajo Seleccionadogit add README.md

Para la gestión de versiones del microservicio, el equipo ha seleccionado la metodología **Trunk-Based Development (TBD)** . A continuación, justificamos técnicamente esta elección comparándola con GitFlow bajo los estándares de clase:

- **Estructura de ramas simplificada:** Frente a las múltiples ramas de larga duración que utiliza GitFlow (`main`, `develop`, `feature`, `release`, `hotfix`) , TBD se organiza en torno a una **única rama principal (`main` o `trunk`)** asistida por ramas de funcionalidad pequeñas y de muy corta duración .
- **Frecuencia de lanzamientos rápida:** TBD promueve lanzamientos **continuos y frecuentes** (incluso varias veces al día) , lo cual es altamente compatible con enfoques de desarrollo ágil y DevOps , a diferencia de los lanzamientos planificados y espaciados de GitFlow.
- **Baja complejidad del flujo:** TBD favorece notablemente la **simplicidad y rapidez** en el desarrollo diario .
- **Riesgo mínimo de conflictos de fusión (*merge*):** En GitFlow el riesgo de conflictos es mayor debido al ciclo de vida prolongado de sus ramas . Con TBD, las integraciones frecuentes y el uso de ramas de corta duración reducen drásticamente los conflictos de fusión .
- **Control de calidad automatizado:** TBD aprovecha el uso de pruebas automatizadas y una sólida cultura de integración continua (CI/CD) para validar cambios rápidos , en contraste con las revisiones manuales exhaustivas previas a la fusión que caracterizan a GitFlow .

---

##  Convenciones del Repositorio

Para asegurar la trazabilidad del código y la calidad de la colaboración en el entorno DevOps , adoptamos los siguientes estándares técnicos:

### 1. Nomenclatura de Ramas 
Las ramas de desarrollo que se creen en el repositorio a partir de la rama principal deben seguir el siguiente formato estándar :
- **Nuevas características:** `feature/<nombre-desarrollador>-<descripcion-del-cambio>` (ej: `feature/mi-funcionalidad`) .
- **Correcciones de errores urgentes:** `hotfix/<nombre-desarrollador>-<descripcion-del-cambio>` (ej: `hotfix/correccion-urgente`) .

### 2. Estándar de Mensajes de Commits
Todos los commits que registren cambios locales en el historial del proyecto deben ser redactados con mensajes claros, descriptivos y en modo imperativo:
- `git commit -m "Implementa funcionalidad <X>"` 
- `git commit -m "Corrige bug urgente detectado en el microservicio"` 

### 3. Flujos de Integración  y Pull Requests
- Queda estrictamente prohibido realizar cambios directamente en la rama principal `main` sin validación previa 
- Todo desarrollo se realiza en ramas de corta duración .
- Al finalizar un cambio, se debe abrir un **Pull Request (PR)** en la plataforma web de GitHub para revisar, probar y validar de manera colaborativa las modificaciones antes de fusionarlas, asegurando la calidad y estabilidad del código en producción .

---

##  Comandos Sucesivos del Ciclo de Trabajo

La secuencia real de comandos Git ejecutados paso a paso para el desarrollo local y remoto de esta actividad es la siguiente:

### 1. Configuración de Identidad en la Computadora
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --list
(Grounded en 1.1.2 Git y modelos de trabajo.pdf - Diapositiva: Configuración inicial)
2. Inicialización y Primer Guardado del Proyecto
git init
git status
git add .
git commit -m "Primer commit iniciando el proyecto"
git branch -M main
(Grounded en 1.1.2 Git y modelos de trabajo.pdf - Diapositivas: Inicializar Git en un proyecto y Ejercicio Práctico)
3. Conexión Remota y Subida Inicial a GitHub
git remote add origin <URL-del-repositorio-creado>
git push -u origin main
(Grounded en 1.1.2 Git y modelos de trabajo.pdf - Diapositivas: Antes de comenzar a trabajar en TBD y Ejercicio Práctico)
4. Creación de la Estructura de Ramas en GitHub
git branch develop
git push origin develop

git branch feature/nueva-funcionalidad
git push origin feature/nueva-funcionalidad

git branch hotfix/correccion-urgente
git push origin hotfix/correccion-urgente
(Grounded en 1.1.2 Git y modelos de trabajo.pdf - Diapositivas: Creación y manejo de ramas y Realizando cambios en el proyecto)
5. Flujo de Desarrollo de Funcionalidad (Feature)
git checkout main
git pull origin main
git checkout -b feature/mi-primer-cambio
# [Se edita el archivo físico en el editor]
git add archivo.txt
git commit -m "Implementa primera funcionalidad"
git push origin feature/mi-primer-cambio
(Grounded en 1.1.2 Git y modelos de trabajo.pdf - Diapositiva: Comandos esenciales para TBD en GitHub)
6. Flujo de Desarrollo de Corrección (Hotfix)
git checkout main
git pull origin main
git checkout -b hotfix/solucion-error-critico
# [Se realiza la corrección del bug]
git add .
git commit -m "Corrige bug urgente detectado en el microservicio"
git push origin hotfix/solucion-error-critico
(Grounded en 1.1.2 Git y modelos de trabajo.pdf - Diapositivas: Comandos esenciales para TBD en GitHub y Realizando cambios en el proyecto)
Automatización con GitHub Actions (CI/CD)
Hemos configurado una canalización o flujo de trabajo automatizado (Workflow) en el directorio .github/workflows/ci-pipeline.yml del repositorio
.
Este pipeline automatiza las validaciones de integración utilizando máquinas virtuales Linux (ubuntu-latest) provistas de manera gratuita por GitHub
. El pipeline se activa automáticamente respondiendo a los siguientes desencadenadores de eventos (Triggers) de clase
:
push: Se ejecuta de forma automática con cada actualización subida a la rama develop
.
pull_request: Valida y prueba el código de manera previa cada vez que se abre un Pull Request con destino a la rama main
.
Código del Pipeline (.github/workflows/ci-pipeline.yml):
name: pipeline-evaluacion-devops

on:
  push:
    branches:
      - develop
  pull_request:
    branches:
      - main

jobs:
  compilar-y-validar:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout del codigo
        uses: actions/checkout@v4

      - name: Ejecutar validacion inicial
        run: echo "El pipeline se ha activado exitosamente."