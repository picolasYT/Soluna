# Soluna Cloud

Soluna Cloud runs the existing Soluna agent in a browser. The web app is part
of this repository and uses the same agent loop, tools, providers, and session
storage as the terminal app.

## Deploy to Render

1. Push this repository to GitHub and merge the cloud workspace changes.
2. In Render, create a **Blueprint** and connect this repository. Render reads
   the root `render.yaml` file to configure the service.
3. Create the service. The Blueprint generates `SOLUNA_WEB_TOKEN` for the
   sign-in screen. Open the service's **Environment** page to reveal or rotate
   the token, then sign in at the service URL.
4. The initial provider is OpenCode Zen. To use another provider, open the
   settings button, choose it, and save its API key.
5. Choose **Importar repositorio** and enter the HTTPS URL of a public GitHub
   repository. Soluna clones it into its persistent workspace and switches to
   that project.

The Blueprint attaches a persistent disk at `SOLUNA_HOME`, so imported
repositories, saved provider keys, configuration, and sessions survive a
redeploy. Render only supports persistent disks on paid services. To run
without a disk, remove the `disk` section and understand that saved data may be
lost when the service restarts.

## Access and execution

The web service requires `SOLUNA_WEB_TOKEN` and presents a sign-in page. Keep
the token private. Soluna's web mode intentionally keeps its existing unsafe
execution behavior: once signed in, the agent can run shell commands in the
active project without a second confirmation. Only deploy it to a workspace
you control.

The first cloud version imports public GitHub repositories over HTTPS. Private
repositories and pushing commits back to GitHub need separate GitHub
credentials and are not configured by this Blueprint.

## Deploy without the Blueprint

Use these Render service settings:

- Runtime: **Node**
- Build command: `npm ci`
- Start command: `node bin/soluna-web.js`
- `SOLUNA_WEB_HOST`: `0.0.0.0`
- `SOLUNA_WEB_TOKEN`: generate a private random value
- `SOLUNA_HOME`: path on a persistent disk, for example
  `/opt/render/project/src/.soluna`

Attach the disk at the same path as `SOLUNA_HOME`. Soluna reads Render's
`PORT` automatically.
