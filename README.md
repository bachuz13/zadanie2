# Zadanie 2 — GitHub Actions Pipeline

## 📌 Opis projektu
To repozytorium zawiera aplikację (zadanie 1) oraz pipeline GitHub Actions do budowania i publikowania obrazu kontenera w chmurze (GHCR). Pipeline:
✅ Buduje obraz multi-arch (amd64 i arm64)  
✅ Używa cache w DockerHub  
✅ Przeprowadza skanowanie CVE za pomocą Trivy  
✅ Publikuje obraz do GHCR tylko, jeśli nie wykryto krytycznych lub wysokich luk bezpieczeństwa

---

## 🚀 Uruchamianie pipeline
Pipeline uruchamia się automatycznie przy każdym **pushu** do gałęzi `main`.

### 🔥 Jak uruchomić pipeline ręcznie:
1. Przejdź do repozytorium na GitHub.
2. Kliknij zakładkę **Actions**.
3. Wybierz workflow `Build and Push Docker Image`.
4. Kliknij **Re-run all jobs** (lub wypchnij nowy commit).

---

## 🔐 Konfiguracja sekretów w GitHub Actions
Aby pipeline działał poprawnie, skonfiguruj sekrety w repozytorium:
1. Przejdź do: **Settings > Secrets and variables > Actions**
2. Dodaj:
   - `DOCKERHUB_USERNAME` — Twoja nazwa użytkownika DockerHub
   - `DOCKERHUB_TOKEN` — token dostępu DockerHub (Read & Write)

### Jak uzyskać token DockerHub:
- Zaloguj się do DockerHub.
- Przejdź do **Account Settings > Security > New Access Token**.
- Wybierz **Read & Write**, nadaj nazwę tokenowi i skopiuj go.
- Wklej token w GitHub w sekcji **Secrets**.

---

## 🛡️ Skanowanie CVE
Pipeline wykorzystuje **Trivy** do skanowania obrazu pod kątem podatności. Obraz zostanie wypchnięty do GHCR tylko wtedy, jeśli Trivy nie wykryje zagrożeń oznaczonych jako `CRITICAL` lub `HIGH`.

---

## 🏷️ Sposób tagowania
- `latest` — najnowszy stabilny obraz w GHCR.
- `zadanie2-cache:latest` — cache w DockerHub (używany do przyspieszenia buildów).

**Uzasadnienie**:  
Tag `latest` pozwala łatwo pobrać najnowszy obraz bez konieczności podawania konkretnego numeru wersji.  
Cache w trybie `max` w DockerHub umożliwia pełne wykorzystanie warstw (szybsze budowanie) — zgodnie z rekomendacją w [Docker Buildx documentation](https://docs.docker.com/build/cache/backends/registry/).

---

## 📦 Pobieranie obrazu
Obraz jest publikowany w GHCR:  
ghcr.io/bachuz13/zadanie2:latest
Aby pobrać obraz lokalnie:
```bash
docker pull ghcr.io/bachuz13/zadanie2:latest
``` 
## 🚀 Uruchamianie kontenera
Aby uruchomić aplikację lokalnie:
```bash
docker run -p 5000:5000 ghcr.io/bachuz13/zadanie2:latest
```
Aplikacja będzie dostępna pod adresem: http://localhost:5000.

