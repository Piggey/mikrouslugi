### Jaka jest różnica między obrazem a kontenerem?

**Obraz (Image)**:
- Jest szablonem niezbędnym do uruchomienia kontenera.
- Zawiera wszystkie potrzebne elementy, takie jak kod aplikacji, biblioteki, zależności, środowisko uruchomieniowe, a także konfiguracje.
- Obraz jest statycznym plikiem, który może być przechowywany i dystrybuowany.

**Kontener (Container)**:
- Jest uruchomionym egzemplarzem obrazu.
- Działa jako izolowane środowisko wykonawcze, które zawiera wszystkie elementy z obrazu oraz dodatkowe ustawienia związane z jego uruchomieniem (takie jak sieć, zasoby CPU, pamięć).
- Kontener jest dynamiczny, co oznacza, że może być uruchamiany, zatrzymywany, usuwany i ponownie uruchamiany.

### Jak sprawdzić liczbę uruchomionych kontenerów Dockera?

```sh
docker ps
```

### Jak sprawdzić, jakie obrazy są dostępne?

Aby sprawdzić, jakie obrazy są dostępne na Twoim systemie, można użyć komendy:
```sh
docker images
```

### Jak uruchomić kontener na podstawie obrazu?

Aby uruchomić kontener na podstawie obrazu, użyj komendy:
```sh
docker run <nazwa-obrazu>
```

### Co się stanie, jeśli spróbujemy uruchomić kontener, którego obraz nie znajduje się na naszym komputerze (np. obraz busybox)?

Jeśli spróbujesz uruchomić kontener z obrazu, który nie jest dostępny lokalnie, Docker automatycznie spróbuje pobrać ten obraz z rejestru Docker Hub (domyślny publiczny rejestr obrazów). Na przykład, komenda:

W ten sposób Docker zapewnia, że zawsze możesz uruchomić kontener na podstawie dostępnych publicznie obrazów, nawet jeśli nie masz ich jeszcze na swoim komputerze.
