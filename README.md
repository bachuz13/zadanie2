# Zadanie 2 – Programowanie Aplikacji w Chmurze

## Opis
Ten projekt demonstruje pipeline CI/CD w GitHub Actions, który:
- Buduje obraz kontenera na podstawie kodu z zadania 1.
- Wspiera platformy `linux/amd64` oraz `linux/arm64`.
- Używa cache z DockerHub.
- Skanuje obraz za pomocą Trivy i publikuje go tylko jeśli nie zawiera CVE o wysokim lub krytycznym poziomie.

## Skaner CVE
Użyto [Trivy](https://github.com/aquasecurity/trivy-action), ponieważ:
- Łatwo integruje się z GitHub Actions.
- Jest darmowy i dobrze udokumentowany.
- Umożliwia blokowanie procesu przy wykryciu luk.

## Tagowanie obrazów
Obrazy tagowane są jako `latest`, ponieważ:
- Upraszcza to automatyzację.
- Brak potrzeby ręcznego wersjonowania w środowisku testowym.

## Publikacja
Obrazy trafiają do:
- `ghcr.io/bachuz13/zadanie1-app`
