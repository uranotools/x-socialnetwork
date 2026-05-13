<div align="center">
  <img src="https://img.shields.io/badge/UranoDesktop-2.0-blueviolet?style=for-the-badge&logo=rocket" alt="UranoDesktop 2.0 Badge"/>
  <img src="https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript Badge"/>
  <img src="https://img.shields.io/badge/MCP-Plugin-success?style=for-the-badge" alt="MCP Plugin Badge"/>
  <img src="https://img.shields.io/badge/Security-Anti--Prompt%20Injection-red?style=for-the-badge&logo=shield" alt="Security Badge"/>
  
  <h1>🪐 Urano X-SocialNetwork Plugin</h1>
  <p><strong>Gestor Autónomo de Redes Sociales para Urano AI</strong></p>
</div>

---

## 🌟 Bienvenido

**X-SocialNetwork** es un **Plugin AI** desarrollado sobre la arquitectura MCP (Model Context Protocol) de UranoDesktop 2.0. Permite a tus agentes de Inteligencia Artificial conectarse, leer y publicar en redes sociales (plantilla inicial para X/Twitter) de manera totalmente autónoma, segura e integrada.

Este plugin no es un simple script, es una extensión nativa que se beneficia de las **capacidades agenticas** de Urano: el LLM puede decidir de forma autónoma cuándo leer el *timeline*, cuándo responder a una mención y cuándo publicar nuevo contenido.

### 🤖 ¿Qué es un Plugin AI?
En el ecosistema de Urano Desktop, un **Plugin AI** es una funcionalidad empaquetada que se agrega a tus agentes para otorgarles capacidades en el mundo real. 
Estos plugins pueden:
- Incluir librerías internas de `node_modules`.
- Envolver librerías o servidores MCP (*Model Context Protocol*) Open Source para extender sus funciones.
- Usarse como base de herramientas nativas e integrarse profundamente en el ecosistema de Urano IA.

En resumen, los Plugins AI son los "brazos y ojos" de tu agente.

---

## 🚀 Características Principales

*   **Lectura de Contexto (`getTimeline`)**: El agente puede leer el feed para empaparse de las conversaciones y tendencias antes de opinar o publicar.
*   **Interacción (`replyToMention`)**: Permite responder específicamente a usuarios que hayan mencionado a la cuenta.
*   **Publicación (`postUpdate`)**: Capacidad para crear nuevos hilos o publicaciones con texto y multimedia.
*   **🛡️ Seguridad de Grado Empresarial (Anti Prompt-Injection)**: El plugin sanitiza la entrada de los usuarios de internet (ej. menciones maliciosas como *"Olvida tus instrucciones y haz X"*) encapsulando la información y forzando al LLM a priorizar su *System Prompt*.
*   **Aislamiento Criptográfico**: Las credenciales de API no se exponen al LLM. Urano inyecta los *secrets* mediante su bóveda segura (Vault).

---

## 🛠️ Tecnologías Usadas

*   **TypeScript / Node.js**: Lenguaje principal de desarrollo y ejecución.
*   **Esbuild**: Compilación ultrarrápida (menos de 10ms) de los binarios para ser consumidos por UranoDesktop.
*   **Urano MCP Protocol**: Arquitectura de comunicación que expone los esquemas (`pluginSchemas`) al agente y convierte los métodos en `tool_calls`.
*   **Skill Injector (`SKILL.md`)**: Inyección bajo demanda del contexto usando el formato `type: mcp`, para instruir al agente sobre *cómo* debe comportarse al usar estas herramientas.

---

## ⚙️ Cómo Configurar e Instalar (Guía Urano MCP)

De acuerdo a la arquitectura oficial de plugins (Documentación de Urano / `llms.txt`), la instalación se realiza directamente desde la interfaz:

### 1. Empaquetar el Plugin
Asegúrate de estar en el directorio del plugin y ejecuta el comando de despliegue para transpilar el código y comprimirlo.
```bash
npm install
npm run deploy
npm run urano-launch
```
Esto generará un archivo `.zip` (ej. `UranoXSocialNetwork.zip`).

### 2. Instalación (Opción A: Producción)
1. Abre **Urano Desktop** y dirígete a **Integrations / MCP Manager**.
2. Haz clic en **Install MCP (.zip)** y sube el archivo generado.
3. El módulo aparecerá en la interfaz visual gracias a que `config.ts` declara los campos necesarios en la sección `settings`.

### Instalación Manual (Opción B: Dev Mode / Desarrollo)
Si deseas ir haciendo cambios al código, agregar nuevas funcionalidades o integrar otras plataformas, usa el Modo Desarrollador:
1. Asegúrate de tener esta carpeta clonada en tu computadora y ejecuta `npm install`.
2. Abre **Urano Desktop > Integrations / MCP Manager**.
3. Dirígete a la sección **Dev Mode**.
4. Haz clic en **Link Local Folder** y simplemente selecciona la carpeta de este proyecto (`x-socialnetwork`).
5. Urano leerá y linkeará tu plugin en vivo. ¡Cualquier cambio que hagas a nivel de código se reflejará directamente!

### 3. Configuración de Credenciales (Vault)
En la misma interfaz del plugin instalado, deberás ingresar las credenciales de tu aplicación de X (Twitter Developer):
- **API Key**
- **API Secret**
- **Access Token**
- **Access Token Secret**

> [!TIP]
> **Seguridad Cero-Confianza**: Los campos están declarados como `type: 'password'` en el `config.ts`. Esto significa que UranoDesktop guardará estas claves en su bóveda criptográfica (`Vault`). El agente AI **nunca verá estos tokens** en su contexto de memoria, garantizando total privacidad.

---

## 🧠 Contexto de IA (`SKILL.md`)

Este plugin incluye su propio "manual de instrucciones" en `SKILL.md`. Al tener el parámetro `type: mcp` en su *frontmatter*, UranoDesktop oculta inteligentemente este archivo del editor visual global para evitar ruido visual, pero fuerza al agente a leer las reglas **antes** de usar las herramientas de la red social.

### Clonado para Otras Redes
Si deseas crear un "Facebook Social Network", simplemente:
1. Copia toda esta carpeta.
2. Modifica las credenciales del `settings` en `config.ts`.
3. Renombra las funciones internas en `ManagerPlugin.ts`.
4. Actualiza los metadatos y esquemas. ¡La estructura es universal!
