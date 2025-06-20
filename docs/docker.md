### ⚙️ Parametry wejściowe (`inputs`)

| Nazwa                | Typ    | Domyślna wartość | Opis                                                         |
| -------------------- | ------ | ---------------- | ------------------------------------------------------------ |
| `docker_image`       | string | `docker:24`      | Obraz Dockera wykorzystywany do uruchomienia joba            |
| `docker_host`        | string | `""`             | Wartość zmiennej `DOCKER_HOST`, np. `tcp://localhost:2375`   |
| `docker_tls_certdir` | string | `""`             | Ścieżka TLS cert dir dla Dockera (pusta wartość wyłącza TLS) |
| `container_version`  | string | `latest`         | Wersja obrazu kontenera (używana jako tag w `docker build`)  |

---
### 🧬 Zmienne środowiskowe

| Nazwa zmiennej           | Wartość                            |
| ------------------------ | ---------------------------------- |
| `CONTAINER_IMAGE_DOCKER` | `$[[ inputs.docker_image ]]`       |
| `DOCKER_HOST`            | `$[[ inputs.docker_host ]]`        |
| `DOCKER_TLS_CERTDIR`     | `$[[ inputs.docker_tls_certdir ]]` |
| `CONTAINER_VERSION`      | `$[[ inputs.container_version ]]`  |

---
### 🧱 Zależności

* **Pliki lokalne**:

  * `/source/logo.yml` – wyświetla logo komponentu
  * `/source/input_variables_docker.yml` – przypisuje zmienne wejściowe do środowiska

* **Usługi**:

  * `docker:24-dind` – uruchamiany jako serwis `docker`

* Wymagany plik `Dockerfile` w katalogu głównym repozytorium

---
### 🚀 Job: `build docker image`

* Buduje obraz Dockera z katalogu projektu
* Używa wersji (`container_version`) jako taga
* Gotowy do rozszerzenia o dodatkowe tagi, push lub metadane

#### 📜 Skrypt
```bash
docker build \
  --build-arg CONTAINER_VERSION=$CONTAINER_VERSION \
  -t $CI_REGISTRY_IMAGE:$CONTAINER_VERSION .
```

---
### 🧪 Przykład użycia

```yaml
include:
  component: registry.gitlab.com/your-group/gitlab-components/docker-build
  inputs:
    container_version: "v1.3.0"
```
