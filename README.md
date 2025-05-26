# Zadanie 2 – Programowanie Aplikacji w Chmurze

## 📦 Obraz Docker
Budowany z `zadanie1/Dockerfile` i wysyłany do GitHub Container Registry (GHCR).

## 🧪 Skanowanie CVE
Wykorzystano [Trivy](https://github.com/aquasecurity/trivy-action) — obraz nie jest publikowany, jeśli zawiera luki o poziomie CRITICAL lub HIGH.

## 🏷️ Tagowanie
- `latest` – zawsze aktualny build
- `short-sha` – unikalny tag dla konkretnego commita
- Cache przechowywany w DockerHub jako publiczny obraz `zadanie1-buildcache`

## 🔐 Sekrety wymagane
Ustawione w repozytorium GitHub:
- `GHCR_USERNAME`
- `GHCR_TOKEN`
- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

## 🚀 Uruchomienie
Pipeline uruchamia się przy pushu do `main` lub ręcznie z GitHub UI.
