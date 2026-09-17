# Manuales de localización Odoo 19

Sitio estático (MkDocs Material) con guías de usuario de las localizaciones **Uruguay (CFE/DGI)** y **Paraguay (SIFEN/DNIT)**.

Sin datos de clientes. Sin RUT/RUC reales, certificados, CSC, CAE ni capturas de compañías vivas.

Repo inicial en cuenta personal. Más adelante se puede transferir a la org de Felipe (`LFer`).

## Local

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Abrir <http://127.0.0.1:8000>.

## GitHub

Crear el remoto (si aún no existe) **sin** `--push` desde el agente; el push lo hace el dueño del repo:

```bash
gh auth login
gh repo create localization-docs --public --source=. --remote=origin -d "Manuales de localización Odoo 19 (UY CFE / PY SIFEN)"
git push -u origin main
```

## Netlify

1. [app.netlify.com](https://app.netlify.com) → Add new site → Import an existing project → GitHub.
2. Elegir `localization-docs`.
3. Netlify lee `netlify.toml` (build `mkdocs build`, publish `site`).
4. Cada push a `main` republica el sitio.

Dominio por defecto: `https://<nombre-sitio>.netlify.app`. Se puede cambiar en Site settings.

## Transferir a LFer

En GitHub: Settings → Transfer repository → org `LFer`. En Netlify, reconectar el repo. El contenido no se reescribe.
