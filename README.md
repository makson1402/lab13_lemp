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
docker compose up -d

### Zatrzymanie i usunięcie kontenerów
docker compose down

### Sprawdzenie statusu i portów działających kontenerów
docker compose ps

wynik:
PS C:\Users\1\Desktop\lab13> docker compose ps
time="2026-06-04T12:48:51+03:00" level=warning msg="C:\\Users\\1\\Desktop\\lab13\\docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion"
NAME              IMAGE                COMMAND                  SERVICE      CREATED          STATUS          PORTS
lemp-mysql        mysql:8.0            "docker-entrypoint.s…"   mysql        15 minutes ago   Up 15 minutes   3306/tcp, 33060/tcp
lemp-nginx        nginx:1.25-alpine    "/docker-entrypoint.…"   webserver    15 minutes ago   Up 15 minutes   0.0.0.0:4001->80/tcp, [::]:4001->80/tcp
lemp-php          php:8.2-fpm-alpine   "docker-php-entrypoi…"   php          15 minutes ago   Up 15 minutes   9000/tcp
lemp-phpmyadmin   phpmyadmin:5.2       "/docker-entrypoint.…"   phpmyadmin   15 minutes ago   Up 15 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp

### Weryfikacja i wyświetlenie listy sieci utworzonych przez Docker
docker network ls

Wynik:
PS C:\Users\1\Desktop\lab13> docker network ls
NETWORK ID     NAME             DRIVER    SCOPE
9c0637f30689   bridge           bridge    local
4edcf9155320   host             host      local
ea9fa6bfb14f   lab12net         bridge    local
70395ecdb630   lab13_backend    bridge    local
603831cc77a9   lab13_frontend   bridge    local
f3dc66007574   mybridge         bridge    local
631f3714262d   none             null      local
4c9394d51ab8   skynet           bridge    local
