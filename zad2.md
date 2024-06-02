### Jaka jest różnica pomiędzy kontenerem a obrazem?

**Obraz (Image)**:
- Jest to statyczny, gotowy do uruchomienia szablon zawierający wszystkie potrzebne komponenty do działania aplikacji (kod źródłowy, biblioteki, pliki binarne, konfiguracje itp.).
- Obrazy są niezmienne i można je przechowywać oraz przenosić między różnymi systemami.
- Obraz można porównać do szablonu lub wzorca, który można uruchomić w postaci kontenera.

**Kontener (Container)**:
- Jest to działający instancja obrazu.
- Kontener jest uruchamiany na podstawie obrazu, ale działa jako oddzielne środowisko wykonawcze.
- Kontener może być dynamicznie uruchamiany, zatrzymywany, usuwany, wznawiany itp.
- Kontener to działający proces, który korzysta z zasobów systemu i zapewnia izolację od innych kontenerów oraz systemu hosta.

### Co to są warstwy obrazu?

Warstwy obrazu (Image Layers) to poszczególne kroki zapisane podczas budowania obrazu Docker. Każda warstwa jest wynikiem jednej instrukcji w pliku Dockerfile (takiej jak `RUN`, `COPY`, `ADD`). Oto kluczowe cechy warstw obrazu:

- Każda warstwa jest niezmienną warstwą plików.
- Warstwy są przechowywane w pamięci podręcznej, co pozwala na efektywne wykorzystanie zasobów i przyspieszenie budowania obrazów.
- Gdy zmienia się jedna warstwa, wszystkie warstwy budowane na jej podstawie muszą być ponownie zbudowane.
- Warstwy są wspólne i mogą być używane przez różne obrazy, co oszczędza miejsce na dysku.

### Jak uruchomić kontener w trybie interaktywnym?

Aby uruchomić kontener w trybie interaktywnym, można użyć opcji `-it` w komendzie `docker run`. Na przykład, aby uruchomić kontener z obrazu `ubuntu` w trybie interaktywnym, można użyć:

```sh
docker run -it ubuntu /bin/bash
```

Opcje `-it` oznaczają:
- `-i` (interactive) - pozwala na interakcję z kontenerem.
- `-t` (tty) - przydziela terminal.

### Jakie polecenia służą do zarządzania kontenerem?

Kilka podstawowych poleceń do zarządzania kontenerami to:

- `docker run` - uruchamia nowy kontener.
- `docker ps` - wyświetla uruchomione kontenery.
- `docker ps -a` - wyświetla wszystkie kontenery (zarówno uruchomione, jak i zatrzymane).
- `docker stop <kontener>` - zatrzymuje uruchomiony kontener.
- `docker start <kontener>` - uruchamia zatrzymany kontener.
- `docker restart <kontener>` - restartuje kontener.
- `docker rm <kontener>` - usuwa zatrzymany kontener.
- `docker exec -it <kontener> <polecenie>` - wykonuje polecenie wewnątrz uruchomionego kontenera w trybie interaktywnym.

### Jak zbudować kontener bez pliku Dockerfile?

Aby zbudować kontener bez pliku Dockerfile, można użyć polecenia `docker commit`, które tworzy nowy obraz na podstawie istniejącego kontenera. Proces wygląda następująco:

1. Uruchom kontener z dowolnego obrazu:
   ```sh
   docker run -it ubuntu /bin/bash
   ```

2. Dokonaj potrzebnych zmian wewnątrz kontenera (np. instalacja oprogramowania, konfiguracja systemu).

3. W nowym terminalu wykonaj:
   ```sh
   docker commit <container_id> my_new_image
   ```

### Podaj znaczenie poszczególnych elementów pliku Dockerfile

Plik Dockerfile zawiera instrukcje, które definiują sposób budowy obrazu Docker. Oto niektóre z podstawowych instrukcji:

- `FROM` - określa bazowy obraz, od którego zaczynamy budowę nowego obrazu.
- `RUN` - wykonuje polecenia w środowisku tworzenia obrazu i zapisuje wynik jako nową warstwę.
- `COPY` - kopiuje pliki lub katalogi z systemu hosta do systemu plików obrazu.
- `ADD` - podobne do `COPY`, ale również obsługuje pobieranie plików z URL oraz automatyczną dekompresję archiwów.
- `CMD` - określa domyślne polecenie, które ma być uruchomione po uruchomieniu kontenera.
- `ENTRYPOINT` - podobne do `CMD`, ale nie jest zastępowane przez dodatkowe argumenty w `docker run`.
- `WORKDIR` - ustawia bieżący katalog roboczy dla następnych instrukcji.
- `EXPOSE` - informuje o portach, które kontener będzie nasłuchiwał w czasie uruchomienia.
- `ENV` - ustawia zmienne środowiskowe.

### Jak zbudować obraz na podstawie pliku Dockerfile?

Aby zbudować obraz na podstawie pliku Dockerfile, można użyć komendy `docker build`. Na przykład, jeśli plik Dockerfile znajduje się w bieżącym katalogu, można wykonać:

```sh
docker build -t my_image .
```

- `-t my_image` - oznacza nazwę i opcjonalnie tag dla nowego obrazu.
- `.` - oznacza bieżący katalog jako kontekst budowy, w którym Dockerfile się znajduje.

Docker następnie przeanalizuje plik Dockerfile, wykona instrukcje w nim zawarte i zbuduje nowy obraz na tej podstawie.
