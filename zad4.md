### Jakie są sposoby wymiany danych z kontenerem?

Wymiana danych z kontenerem Docker może odbywać się na kilka sposobów:

1. **Woluminy (Volumes)**:
   - Są to niezależne jednostki przechowywania, które istnieją poza cyklem życia kontenerów.
   - Woluminy są zarządzane przez Docker i przechowywane w specjalnym katalogu na hoście (np. `/var/lib/docker/volumes`).

2. **Bind mounts (Zamontowanie katalogów)**:
   - Umożliwiają bezpośrednie zamontowanie katalogu lub pliku z systemu plików hosta do systemu plików kontenera.
   - Dają pełną kontrolę nad lokalizacją danych na hoście.

3. **tmpfs mounts**:
   - Są to pamięci RAM używane jako system plików.
   - Są szybkie i nie przechowują danych na dysku hosta.

4. **Kopiowanie plików**:
   - Używanie komend `docker cp` do kopiowania plików między systemem hosta a kontenerem.

### Co to jest wolumin?

**Wolumin (Volume)**:
- Jest to mechanizm przechowywania danych w Dockerze, który umożliwia trwałe przechowywanie danych poza cyklem życia kontenera.
- Woluminy są zarządzane przez Docker i mogą być współdzielone między różnymi kontenerami.
- Umożliwiają łatwą migrację danych między kontenerami, bez zależności od lokalizacji na hoście.

### Jak obsługuje się woluminy?

Podstawowe operacje związane z woluminami w Dockerze:

1. **Tworzenie woluminu**:
   ```sh
   docker volume create my_volume
   ```

2. **Listowanie woluminów**:
   ```sh
   docker volume ls
   ```

3. **Inspekcja woluminu**:
   ```sh
   docker volume inspect my_volume
   ```

4. **Usuwanie woluminu**:
   ```sh
   docker volume rm my_volume
   ```

5. **Używanie woluminu podczas uruchamiania kontenera**:
   ```sh
   docker run -d -v my_volume:/path/in/container my_image
   ```

### Jak zadeklarować współdzielenie folderu hosta?

Aby współdzielić folder hosta z kontenerem, używamy bind mounts. Przykład:

```sh
docker run -d -v /path/on/host:/path/in/container my_image
```

W tej komendzie:
- `/path/on/host` to ścieżka na hoście.
- `/path/in/container` to ścieżka w kontenerze, gdzie będzie zamontowany folder z hosta.

### Jak kontener może udostępnić dane innemu kontenerowi?

Kontenery mogą udostępniać dane innym kontenerom poprzez współdzielone woluminy lub bind mounts. Przykład z użyciem woluminów:

1. **Tworzenie woluminu**:
   ```sh
   docker volume create shared_volume
   ```

2. **Uruchomienie pierwszego kontenera z woluminem**:
   ```sh
   docker run -d --name container1 -v shared_volume:/data my_image
   ```

3. **Uruchomienie drugiego kontenera z tym samym woluminem**:
   ```sh
   docker run -d --name container2 -v shared_volume:/data another_image
   ```

W obu kontenerach ścieżka `/data` będzie zamontowana na woluminie `shared_volume`, co pozwala im na współdzielenie danych.

### Przykład współdzielenia folderu hosta:

1. **Uruchomienie pierwszego kontenera z bind mount**:
   ```sh
   docker run -d --name container1 -v /path/on/host:/data my_image
   ```

2. **Uruchomienie drugiego kontenera z tym samym bind mount**:
   ```sh
   docker run -d --name container2 -v /path/on/host:/data another_image
   ```

W obu kontenerach ścieżka `/data` będzie zamontowana na folderze `/path/on/host`, co pozwala im na współdzielenie danych.

### Podsumowanie

Wymiana danych między kontenerami i hostem jest możliwa dzięki woluminom, bind mounts, tmpfs mounts oraz kopiowaniu plików. Woluminy zapewniają trwałość i niezależność danych, natomiast bind mounts umożliwiają bezpośrednie używanie plików i katalogów z hosta. Współdzielenie danych między kontenerami odbywa się poprzez wspólne używanie woluminów lub bind mounts.
