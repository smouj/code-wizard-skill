name: Code Wizard
description: Magically transforms code into efficient, bug-free solutions
tags: code, magic, transform, efficiency
version: 1.0.0
author: Kilo
dependencies:
  - Node.js >= 14.0.0 (for JavaScript/TypeScript projects)
  - Python >= 3.8 (for Python projects)
  - Git >= 2.25.0
  - ESLint (for JavaScript/TypeScript linting)
  - Ruff (for Python linting)
environment_variables:
  - CODE_WIZARD_API_KEY: Optional API key for advanced transformations (contact support for access)
  - CODE_WIZARD_LOG_LEVEL: Set to 'debug' for verbose logging, 'info' for standard (default)
---

# Habilidad Code Wizard

## Propósito

La habilidad Code Wizard transforma mágicamente el código en soluciones eficientes y libres de errores aplicando técnicas avanzadas de refactorización, optimización y corrección de bugs. Entiende patrones de código en múltiples lenguajes y frameworks, asegurando codebases mantenibles, performantes y seguras.

### Casos de Uso Reales
- **Refactorización de Código Legacy**: Convertir código spaghetti en una función JavaScript de 10 años en patrones modernos async/await con manejo adecuado de errores.
- **Optimización de Rendimiento**: Transformar un script de procesamiento de datos en Python que toma 30 minutos en ejecutarse en una implementación vectorizada con NumPy que se completa en menos de 5 segundos.
- **Corrección de Bugs**: Detectar y corregir automáticamente excepciones de puntero nulo en código Java agregando verificaciones de nulo y usando wrappers Optional.
- **Implementación de Características**: Generar operaciones CRUD para una nueva entidad en una API de Django REST framework, completa con serializadores, vistas y configuraciones de URL.
- **Fortalecimiento de Seguridad**: Escanear y parchear vulnerabilidades de inyección SQL en código PHP implementando declaraciones preparadas y validación de entrada.

## Alcance

Code Wizard opera en comandos específicos que apuntan a desafíos comunes de codificación. Funciona con archivos en el workspace actual y soporta cambios incrementales con verificación integrada.

### Comandos Específicos
- `/code-wizard refactor <file_path> [--language <lang>] [--style <style>]`: Refactorizar código para legibilidad y mantenibilidad
- `/code-wizard optimize <file_path> [--metric <perf|memory|cpu>]`: Optimizar código para métricas de rendimiento específicas
- `/code-wizard fix-bug <file_path> <bug_description>`: Identificar y corregir bugs basados en descripción
- `/code-wizard implement <feature_description> [--language <lang>] [--framework <fw>]`: Generar código de nueva característica
- `/code-wizard audit <file_path> [--security|--performance|--best-practices]`: Auditar código por problemas
- `/code-wizard migrate <file_path> --from <old_version> --to <new_version>`: Migrar código entre versiones

### Lenguajes Soportados
- JavaScript/TypeScript (ES6+, React, Node.js)
- Python (3.8+, Django, Flask)
- Java (8+, Spring)
- C# (.NET Core 3.1+)
- Go (1.16+)
- PHP (7.4+, Laravel)

## Proceso de Trabajo Detallado

Code Wizard sigue un proceso sistemático de 7 pasos para asegurar transformaciones mágicas:

1. **Análisis de Código**: Analizar el(los) archivo(s) objetivo usando AST (Abstract Syntax Tree) para entender estructura, dependencias y patrones.
2. **Detección de Problemas**: Ejecutar herramientas de análisis estático (ESLint para JS, Ruff para Python) para identificar bugs, ineficiencias y violaciones.
3. **Planificación de Transformación**: Generar un plan detallado de cambios, incluyendo diffs antes/después y evaluación de impacto.
4. **Aplicación Segura**: Aplicar cambios incrementalmente con staging de git, permitiendo fácil rollback.
5. **Pruebas Automatizadas**: Ejecutar suites de pruebas relevantes (Jest para JS, pytest para Python) para verificar funcionalidad.
6. **Linting y Formateo**: Aplicar estilo de código consistente usando Prettier o Black.
7. **Verificación Final**: Realizar pruebas de integración y escaneos de seguridad antes de marcar como completo.

### Configuración de Entorno
Antes de usar Code Wizard, asegúrate:
- Repositorio Git inicializado en el workspace
- Dependencias instaladas (ejecutar `npm install` o `pip install -r requirements.txt`)
- Framework de pruebas configurado (ej. `jest.config.js` o `pytest.ini`)

## Reglas de Oro

1. **Siempre Hacer Backup Primero**: Code Wizard crea commits automáticos de git antes de cambios. Nunca ejecutar en trabajo no commiteado.
2. **Cambios Incrementales**: Grandes refactors se dividen en commits pequeños y testeables para minimizar riesgo.
3. **Seguridad de Tipos**: Para lenguajes tipados, asegurar que las transformaciones preserven o mejoren anotaciones de tipo.
4. **Seguridad Primero**: Cualquier generación de código incluye validación de entrada y patrones de seguridad comunes.
5. **Verificación de Rendimiento**: Todas las optimizaciones incluyen benchmarks antes/después usando profiling integrado.
6. **Compatibilidad de Framework**: Las transformaciones respetan convenciones de framework (ej. React hooks, Django models).
7. **Actualizaciones de Documentación**: Code Wizard actualiza comentarios y docstrings para reflejar cambios.

## Ejemplos

### Ejemplo 1: Refactorización de JavaScript Legacy
**Entrada del Usuario:**
```
/code-wizard refactor src/utils.js --language javascript --style modern
```

**Código Actual:**
```javascript
function getUserData(userId) {
  return fetch('/api/users/' + userId)
    .then(response => response.json())
    .catch(error => console.error(error));
}
```

**Salida de Code Wizard:**
```javascript
/**
 * Fetches user data from the API
 * @param {string} userId - The user identifier
 * @returns {Promise<Object>} User data object
 */
async function getUserData(userId) {
  try {
    const response = await fetch(`/api/users/${userId}`);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error('Failed to fetch user data:', error);
    throw error;
  }
}
```

**Pasos de Verificación:**
- Ejecutar `npm test` para asegurar que las pruebas existentes pasen
- Verificar ESLint: `npx eslint src/utils.js`
- Rendimiento: No se espera cambio significativo para este refactor

### Ejemplo 2: Optimización de Rendimiento en Python
**Entrada del Usuario:**
```
/code-wizard optimize data_processor.py --metric perf
```

**Antes de Optimización:**
```python
def process_large_dataset(data):
    results = []
    for item in data:
        if item['value'] > 100:
            results.append(item['value'] * 2)
    return results
```

**Después de Optimización:**
```python
import numpy as np

def process_large_dataset(data):
    """
    Process large dataset using vectorized operations for performance
    @param data: List of dicts with 'value' key
    @return: List of processed values
    """
    values = np.array([item['value'] for item in data])
    return (values[values > 100] * 2).tolist()
```

**Impacto en Rendimiento:**
- Antes: 30.2 segundos para 1M items
- Después: 0.8 segundos para 1M items
- Verificación: `python -m pytest tests/test_data_processor.py -v`

### Ejemplo 3: Corrección de Bugs
**Entrada del Usuario:**
```
/code-wizard fix-bug api/routes.py "division by zero when quantity is 0"
```

**Código con Bug:**
```python
def calculate_total(price, quantity):
    return price * quantity / quantity  # Bug: divides by quantity
```

**Código Corregido:**
```python
def calculate_total(price: float, quantity: int) -> float:
    """
    Calculate total price for given quantity
    @param price: Unit price
    @param quantity: Number of units
    @return: Total price
    @raises ValueError: If quantity is zero or negative
    """
    if quantity <= 0:
        raise ValueError("Quantity must be positive")
    return price * quantity
```

## Comandos de Rollback

### Rollback Inmediato
- `git reset --hard HEAD~1`: Revertir el último commit hecho por Code Wizard
- `git checkout -- <file_path>`: Descartar cambios a un archivo específico

### Rollback Selectivo
- `git revert <commit_hash>`: Crear un nuevo commit que deshace cambios específicos
- `git reset --soft HEAD~1 && git reset HEAD <file_path>`: Deshacer staging de cambios manteniéndolos en directorio de trabajo

### Reset Completo del Proyecto
- `git reset --hard origin/main`: Resetear a rama remota main (usar con precaución)
- `git clean -fd`: Remover archivos y directorios no rastreados

### Verificación Después de Rollback
- Ejecutar pruebas: `npm test` o `python -m pytest`
- Verificar sintaxis: `node --check <file>` o `python -m py_compile <file>`
- Lint: `npx eslint .` o `ruff check .`

## Dependencias y Requisitos

- **Runtime**: Node.js 14+ o Python 3.8+
- **Herramientas**: Git, ESLint/Ruff, Prettier/Black
- **Frameworks**: Soporta frameworks principales con optimizaciones específicas
- **Almacenamiento**: Requiere ~100MB de espacio libre para archivos temporales

## Pasos de Verificación

1. **Pre-Transformación**: `git status && npm run lint && npm test`
2. **Post-Transformación**: `git diff --staged && npm run lint && npm test`
3. **Rendimiento**: Usar comando `time` o profiling integrado para benchmarks
4. **Seguridad**: Ejecutar `npm audit` o `safety check` para vulnerabilidades

## Solución de Problemas Comunes

### Problema: Code Wizard falla al parsear archivo
**Causa**: Sintaxis no soportada o código malformado
**Solución**: Ejecutar `node --check <file>` o `python -c "import ast; ast.parse(open('<file>').read())"` para validar sintaxis primero

### Problema: Transformaciones rompen pruebas
**Causa**: Cambios lógicos no contabilizados en pruebas
**Solución**: Revisar git diff, actualizar pruebas manualmente, luego re-ejecutar `/code-wizard implement "update tests for <feature>"`

### Problema: Optimización de rendimiento no mejora velocidad
**Causa**: Bottleneck en otro lugar (I/O, red)
**Solución**: Usar herramientas de profiling: `python -m cProfile <script>` o Chrome DevTools para JS

### Problema: Rollback falla
**Causa**: Cambios conflictivos o conflictos de merge
**Solución**: `git status`, resolver conflictos manualmente, luego `git reset --hard HEAD~1`

### Problema: Variables de entorno no reconocidas
**Causa**: No exportadas en shell
**Solución**: `export CODE_WIZARD_LOG_LEVEL=debug` antes de ejecutar comandos

Para soporte, contacta al equipo de desarrollo de OpenClaw o revisa logs en `~/.openclaw/logs/code-wizard.log`.