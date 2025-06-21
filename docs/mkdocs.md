### ⚙️ Parametry wejściowe (`inputs`)

| Nazwa          | Typ    | Domyślna wartość                                             | Opis                                                   |
| -------------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------ |
| `docker_image` | string | `registry.gitlab.com/pl.rachuna-net/containers/mkdocs:1.0.0` | Obraz Dockera zawierający MkDocs i wymagane zależności |

---
### 🧬 Zmienne środowiskowe

| Nazwa zmiennej           | Wartość                      |
| ------------------------ | ---------------------------- |
| `CONTAINER_IMAGE_MKDOCS` | `$[[ inputs.docker_image ]]` |

---
### 🧱 Zależności

* **Pliki lokalne**:

  * `/source/logo.yml` – wyświetla logo komponentu
  * `/source/input_variables_mkdocs.yml` – ustawia dodatkowe zmienne środowiskowe, jeśli wymagane

* **Wymagany plik w repozytorium**:

  * `mkdocs.yml` – plik konfiguracyjny MkDocs
  * katalog `docs/` – zawierający dokumentację w formacie Markdown

---
### 🚀 Job: `build mkdocs project`

* Etap: `build`
* Buduje stronę dokumentacji MkDocs do katalogu `public/`
* Artefakty są zapisywane i mogą być wykorzystane np. w `pages:` lub `deploy:` jobach

#### 📜 Skrypt

```bash
mkdocs build --site-dir public
```

#### 📁 Artefakty

```yaml
artifacts:
  paths:
    - public
```
---
### 🧪 Przykład użycia

```yaml
include:
  component: registry.gitlab.com/your-group/gitlab-components/mkdocs-build
  inputs:
    docker_image: "registry.gitlab.com/your-group/containers/mkdocs:1.0.0"
```