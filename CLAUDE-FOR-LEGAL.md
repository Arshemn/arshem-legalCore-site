# Arshem LegalCore vs. Claude for Legal

**Nota de alcance.** Este documento es una referencia de posicionamiento competitivo
para uso interno (ventas, borradores de marketing). No ha pasado revisión legal y
**no debe publicarse tal cual en la página pública** sin esa revisión — en particular
cualquier frase que nombre a Anthropic o a Claude directamente. Ver la sección final
antes de usar cualquier parte de esto en `index.html`.

Todo lo que se afirma aquí sobre Claude for Legal viene de cobertura periodística
pública (citada abajo), no de documentación oficial de Anthropic ni de una prueba
directa del producto. Todo lo que se afirma sobre Arshem LegalCore es verificable en
este mismo proyecto (backend, frontend, `AGENTS.md`).

## Qué es Claude for Legal, según cobertura pública

Lanzado el 14 de mayo de 2026 (ABA Journal, Artificial Lawyer, LawNext, Legal IT
Insider — ver fuentes):

- Es una **capa de asistente de IA de propósito general** (Claude) con extensiones
  legales — no un sistema de gestión documental o de casos propio.
- Se integra en Word, Outlook, y una plataforma de colaboración llamada "Cowork".
- 12 plugins por área de práctica (Comercial, Laboral, Privacidad, Producto,
  Corporativo, Gobernanza de IA), con plantillas y playbooks personalizables.
- Más de 20 conectores MCP hacia herramientas legales existentes: Harvey, Thomson
  Reuters (CoCounsel Legal, Westlaw, Practical Law), DocuSign, Ironclad, iManage,
  NetDocuments, LexisNexis, Box, Everlaw, LSuite, y herramientas de acceso a la
  justicia (Courtroom5, Descrybe, Free Law Project).
- Capacidades mencionadas: comprensión de documentos (rastrear términos definidos
  entre anexos), revisión de contratos, investigación, apoyo a eDiscovery y
  litigio (cronologías, preparación de contrainterrogatorios).
- La cobertura consultada **no describe** que incluya: bóveda documental propia,
  gestión nativa de matters/clientes, registro de auditoría, aprobaciones de flujo
  de trabajo, ni permisos nativos por matter — esas funciones quedan del lado de
  las plataformas socias a las que se conecta.

## Dónde Arshem LegalCore es, hoy, una herramienta distinta

Esto no es "mejor en todo" — es una diferencia de arquitectura real, verificable en
este mismo proyecto, no una comparación de calidad de modelo de IA:

1. **Un solo sistema, no una capa que depende de otros.**
   Claude for Legal es el asistente; el equipo sigue necesitando — y configurando,
   y pagando por separado — una plataforma distinta para bóveda, matters, permisos
   y auditoría. En Arshem LegalCore la IA vive dentro del mismo documento que ya
   está cifrado, organizado por matter y auditado: un solo login, un solo lugar.

2. **Cifrado por sobre, nativo, no una opción que configurar aparte.**
   Cada documento se cifra con su propia llave (AES-256), envuelta por una llave
   maestra que nunca se guarda junto a los datos — por diseño del backend, no como
   un nivel empresarial que haya que activar.

3. **Registro de auditoría append-only, no una integración con otro sistema.**
   Cada acceso, cambio y borrado queda escrito en una tabla que ni un administrador
   puede alterar — es parte del propio backend (ver `AGENTS.md`: "Every access
   decision — allowed or denied — writes to AuditLog"), no algo que dependa de qué
   herramienta de terceros se conectó.

4. **Entorno de carga aislado, de fábrica.**
   Todo PDF o Word nuevo pasa por un contenedor sin acceso a red antes de llegar a
   la bóveda — escaneo de malware, bloqueo de macros, OCR. Es parte del flujo de
   subida del producto, no una integración con un escáner externo.

5. **La sugerencia de la IA vive en el documento, no en una ventana de chat aparte.**
   Insertar / tachar, visible en el mismo editor donde se redacta la cláusula — no
   una respuesta en un chat que luego hay que copiar y pegar al documento real.

## Lo que no podemos afirmar — y por qué no está aquí

- Nada sobre cifras de adopción, número de clientes, o comparaciones de calidad del
  modelo de IA — Arshem LegalCore no entrena ni opera un modelo propio; la revisión
  de IA depende del mismo tipo de modelos de lenguaje que cualquier producto del
  sector, no de un modelo exclusivo.
- Nada sobre privilegio legal, validez probatoria, ni certificaciones de
  cumplimiento (SOC2, ISO, etc.) — no hay evidencia de que Arshem las tenga, y no
  vamos a inventarlas.
- Nada sobre que Claude for Legal "falle" o sea "peor" — un artículo de terceros
  (gc.ai) hace afirmaciones fuertes sobre un caso judicial específico y riesgos de
  privilegio; se excluyó deliberadamente de este documento por no poder verificar
  esa cita de forma independiente y porque esa fuente compite en el mismo espacio
  (no es neutral). El punto de diferenciación real que sí sostenemos es
  arquitectónico — sistema integrado vs. capa de IA sobre herramientas de
  terceros — no de calidad del modelo ni de riesgo legal.

## Fuentes consultadas

- [ABA Journal — Anthropic launches Claude for Legal](https://www.abajournal.com/news/article/anthropic-launches-claude-for-legal-giving-lawyers-20-new-program-integrations-and-12-practice-area-plugins)
- [Artificial Lawyer — Claude For Legal Launches, May Reshape the Legal Tech World](https://www.artificiallawyer.com/2026/05/12/claude-for-legal-launches-may-reshape-the-legal-tech-world/)
- [LawNext — Anthropic Goes All-In on Legal](https://www.lawnext.com/2026/05/anthropic-goes-all-in-on-legal-releasing-more-than-20-connectors-and-12-practice-area-plugins-for-claude.html)
- [Legal IT Insider — Claude for Legal: What the industry needs to know](https://legaltechnology.com/claude-for-legal-what-the-industry-needs-to-know/)

## Si esto va a la página pública

No recomiendo nombrar "Claude" o "Anthropic" directamente en el copy público sin que
alguien con criterio legal lo revise antes. La publicidad comparativa veraz es
legal en la mayoría de jurisdicciones, pero eso no es lo mismo que "ya está listo
para publicar" — conviene revisión, no asumirlo.

Si se quiere algo para la web ya mismo, la versión más segura — y honestamente más
consistente con el tono que ya se definió para esta página tras las últimas
ediciones de copy — es describir lo que Arshem hace, sin nombrar a ningún
competidor: los cinco puntos de la sección anterior funcionan solos, sin la palabra
"Claude" en ninguna parte. Puedo preparar esa versión si quieres verla antes de
decidir si usamos la comparación nombrada o la versión sin nombrar.
