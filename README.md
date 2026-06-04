# Laboratorium 13 - Stack LEMP w Docker Compose
**Przedmiot:** Programowanie Aplikacji w Chmurze Obliczeniowej (PAwChO)

Repozytorium zawiera konfigurację wielokontenerowego środowiska **LEMP** (Nginx, PHP-FPM, MySQL) wraz z narzędziem **phpMyAdmin** uruchomionego przy użyciu Docker Compose zgodnie z wytycznymi projektu laboratoryjnego.

---

## 1. Konfiguracja sieci i kontenerów
Zgodnie z wymaganiami zadania, architektura została podzielona na dwie odseparowane sieci typu `bridge`:
* **frontend** – sieć dostępna dla świata zewnętrznego (Nginx, phpMyAdmin).
* **backend** – sieć wewnętrzna do komunikacji między usługami (Nginx, PHP-FPM, MySQL, phpMyAdmin).

**Uzasadnienie podłączenia phpMyAdmin:** Narzędzie phpMyAdmin zostało dołączone do sieci `frontend`, aby umożliwić dostęp do interfejsu graficznego z poziomu przeglądarki hosta, oraz do sieci `backend`, co pozwala na bezpieczną komunikację z bazą danych MySQL w wydzielonej sieci wewnętrznej.

Wszystkie użyte obrazy posiadają sztywne, zdefiniowane tagi wersji z DockerHub. Serwer Nginx wystawia aplikację na porcie zewnętrznym **4001**, a phpMyAdmin na porcie **6001**.

---

## 2. Użyte polecenia i wyniki ich działania

### Uruchomienie środowiska w tle:
```bash
docker compose up -d
