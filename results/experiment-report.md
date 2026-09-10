# Context Engineering Experiment
## Hypothesis
Se tiene al idea de que la calidad del código generado por un agente de inteligencia artificial depende del contexto proporcionado en el prompt. Se espera que un contexto más detallado y específico conduzca a resultados de mayor calidad en comparación con un contexto mínimo o genérico.
## Experimental Setup
Se realizará una serie de pruebas utilizando un agente de inteligencia artificial para generar código en respuesta a prompts con diferentes niveles de contexto.
Los 3 experimentos parten de la misma linea base
## A — Minimal Context
**Prompt:** Implement the customer email update functionality.
Inspect the repository first. Implement the necessary changes and run the tests.

**Results:** Los resultados se encuentran en la la rama Experimento_A.

**Human intervention:** No se realizaron cambios al codigo dado que nada genero error.

**Score:** : 8
**Observations:** Fue el resultado con mayor tiempo de espera, además de ser el único que generó más pruebas de pytest.
Además se observó que el agente en lugar de editar el archivo lo reescribió por completo aunque no haya editado parte reescritas.

## B — Repository Context
**Prompt:**
Implement the customer email update functionality.
Before making changes:
1. Inspect the repository.
2. Read README.md.
3. Inspect all relevant source files.
4. Inspect the tests.
5. Infer expected behavior from the code and tests.
6. Run tests before changing code.
7. Make the smallest necessary implementation.
8. Run tests again.
9. Explain which repository information influenced the implementation.

**Results:** Se encuentra en la rama Experimento_B
**Human intervention:** No se realizaron cambios al codigo dado que nada genero error.

**Score:**: 8.5

**Observations:** Fue el resultado con menor código innecesario.

## C — Engineered Context
**Prompt:** Implement the customer email update functionality.
Follow SPEC.md and AGENTS.md.
Inspect the repository first, run tests before and after changes, and explain your verification.

**Results:** Se encuentra en la rama Experimento_C

**Human intervention:** No se realizaron cambios al codigo dado que nada genero error.

**Score:** 8

**Observations:** Se esperaba que fuera el de mejor resultado, pero en este experimento el agente decidió revisar los commits anteriores,
usar varias veces git diff y decidió reescribir el archivo en lugar de editarlo.

## Comparative Results
Al realizar la comparativa de resultados se observó que el experimento B generó el código más limpio y con menos código innecesario, mientras que el experimento A generó más pruebas de pytest y el experimento C generó más lecturas por todo el repositorio.
## Error Analysis
En esta ocasión no se presentaron errores en el código generado por el agente.
Sin embargo, se observó que menos contexto generó más pruebas de pytest, lo que podría indicar que el agente no estaba seguro de la implementación y generó más pruebas para verificar su funcionamiento.
## Context Quality Analysis
Se observó que la falta de contexto hizo que el agente generara más código inncesario.
En un experimento a pequeña escala como este, esto no es un problema, pero en un proyecto más grande podría generar problemas de mantenimiento y aumentar la probabilidad de introducir errores o defectos.

## Conclusions

### Preguntas de Análisis.
1. ¿Cuál fue tu hipótesis?

    *Se tiene al idea de que la calidad del código generado por un agente de inteligencia artificial depende del contexto proporcionado en el prompt. Se espera que un contexto más detallado y específico conduzca a resultados de mayor calidad en comparación con un contexto mínimo o genérico. Se esperaba que el experimento C presentara mejores resultados.*
2. ¿Cuál experimento produjo el mejor resultado y por qué?

   *El experimento B, dado que generó el código más limpio además de que utilizó menos lecturas al repositorio.*

3. ¿Qué errores aparecieron en A y no en C?

    *No se detectaron errores, sin embargo si se detectó que el A generó más pruebas pytest*

5. ¿Qué aportó SPEC.md?

    *Especificaciones claras para que el agente sepa qué requisitos debe cumplir*

6. ¿Qué función tuvo AGENTS.md?

    *Proporcionar instrucciones detalladas de comportamiento sin tener que introducirlas en el prompt*

7. ¿Más contexto significa necesariamente mejor contexto?
    *No necesariamente, más contexto puede ser de menor calidad y ocasionar contradicciones o lectura innecesaria*
8. ¿Qué información fue redundante?
    
    *Tener que leer el repositorio*

9. ¿Qué intervención humana fue necesaria?
    
    *Otorgar permisos y validacion*

10. ¿Qué cambiarías en SPEC.md y AGENTS.md?
    
    *En Agents agregaría instrucciones para evitar la lectura innecesaria.*

11. ¿Qué aprendiste sobre la responsabilidad del desarrollador al usar agentes?

    *La responsabilidad de la calidad del código generado por un agente de inteligencia artificial recae en el desarrollador, quien debe proporcionar contexto de calidad y definir metas claras para obtener resultados óptimos. La falta de contexto o contexto de mala calidad puede llevar a decisiones incorrectas por parte del agente, introduciendo defectos o vulnerabilidades en el código.*
### Pregunta Final
El contexto proporcionado a los agentes hace la diferencia entre el uso optimizado de los recursos y la generación de código innecesario.
Al dar contexto de mala calidad o poco contexto permitimos que el agente tenga más "libertad" en hacer cambios deliverados y no solicitados.
Esto puede causar cosas como lecturas innecesarias o reescrituras completas de archivos.

Definir metas claras y proporcionar contexto de calidad es fundamental para obtener resultados de mayor calidad generados por agentes de inteligencia artificial.
La falta de contexto puede causar que el agente decida tomar decisiones que pueden introducir defectos o incluso vulnerabilidades.
Por otro lado, contexto de mala calidad puede hacer contradecir al agente y hacer que necesite más loops de corrección o que tenga que suponer más.
### Comparativa de Métricas

| Métrica | A | B | C |
| :--- | :--- | :--- | :--- |
| **Test Passing** | 8 | 4 | 4 |
| **Test Failing** | 0 | 0 | 0 |
| **Requisitos cumplidos** | Todos | Todos | Todos |
| **Cambios innecesarios** | Reescritura completa del código | Ninguno | Reescritura completa de repository.py |
| **Iteraciones** | 5 | 2 | 1 |
| **Intervenciones humanas** | En validación al final y otorgar permisos | En validación al final y otorgar permisos | En validación al final y otorgar permisos |
| **Problemas introducidos** | Código extra no solicitado y reescritura de código innecesaria. | No se identificaron problemas | Código extra no solicitado y reescritura de código innecesaria. |
| **Tiempo** | 4 minutos | 2 minutos | 1:50 minutos |
| **Score/10** | 8 | 10 | 8.5 |
## What I Would Change
No permitiría que el agente revisara los commits anteriores. Esto puede causar que el agente decida 
reescribir todo el archivo con el contenido de los commits anteriores, lo que puede generar código innecesario y aumentar el tiempo de espera.