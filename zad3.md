### Jakie sieci bazowo obsługuje Docker Engine?

Docker Engine bazowo obsługuje trzy typy sieci:

1. **bridge**
2. **host**
3. **none**

### Czym się różnią sieci bridge, host i none?

**Bridge**:
- Domyślna sieć dla nowych kontenerów, jeśli nie zostanie określona inna sieć.
- Kontenery podłączone do sieci bridge mogą komunikować się ze sobą za pomocą nazw DNS lub adresów IP.
- Kontenery są izolowane od sieci hosta, co oznacza, że mają własne adresy IP i komunikują się przez mostek sieciowy.
- Umożliwia mapowanie portów z kontenera na hosta, aby umożliwić komunikację ze światem zewnętrznym.

**Host**:
- Kontenery uruchamiane w tej sieci współdzielą sieć hosta.
- Kontener nie ma własnego adresu IP i używa IP oraz stosu sieciowego hosta.
- Eliminuje warstwę sieciową pośredniczącą, co może poprawić wydajność sieci.
- Może powodować konflikty portów, ponieważ kontener i host używają tych samych portów.

**None**:
- Całkowicie odizolowany tryb sieciowy.
- Kontener nie ma dostępu do żadnej sieci (nie ma interfejsu sieciowego).
- Używany głównie w celach specjalnych, gdzie sieć nie jest potrzebna.

### Jak działają polecenia docker network inspect i docker inspect?

**docker network inspect**:
- Służy do uzyskiwania szczegółowych informacji na temat danej sieci Docker.
- Wyświetla konfigurację sieci, w tym informacje o kontenerach podłączonych do sieci, ustawieniach IP, opcjach sterownika i innych.

Przykład użycia:
```sh
docker network inspect bridge
```
Wyświetli szczegółowe informacje o sieci bridge.

**docker inspect**:
- Służy do uzyskiwania szczegółowych informacji o zasobach Docker, takich jak kontenery, obrazy, wolumeny, itp.
- Wyświetla pełne metadane dotyczące zasobu, w tym konfigurację, status, opcje sieciowe, punkty montowania i inne.

Przykład użycia:
```sh
docker inspect <container_id_or_name>
```
Wyświetli szczegółowe informacje o wskazanym kontenerze.

### Jak skonfigurować komunikację kontenera "ze światem" w sieciach host i bridge?

**W sieci bridge**:
1. **Mapowanie portów**:
   - Aby kontener mógł komunikować się ze światem zewnętrznym, należy zmapować porty kontenera na porty hosta.
   - Używamy opcji `-p` lub `--publish` podczas uruchamiania kontenera.
   
   Przykład:
   ```sh
   docker run -d -p 8080:80 my_image
   ```
   - Ten przykład mapuje port 80 kontenera na port 8080 hosta. Dostęp do aplikacji w kontenerze można uzyskać przez port 8080 na hoście.

2. **Ustawienia sieci**:
   - Możemy również ustawić różne opcje sieciowe, takie jak DNS, IP itp., podczas tworzenia kontenera.

**W sieci host**:
- Kontener używa sieci hosta bez pośrednictwa dodatkowej warstwy sieciowej.
- Kontener ma dostęp do wszystkich portów i adresów IP hosta.
  
Przykład:
```sh
docker run --network host my_image
```
- W tym przypadku wszystkie usługi w kontenerze są dostępne bezpośrednio na adresie IP hosta. Jeśli kontener uruchamia serwer na porcie 80, będzie on dostępny na porcie 80 hosta.

### Komunikacja kontenera "ze światem":

**Sieć bridge**:
- **Port Forwarding**: Mapowanie portów hosta na porty kontenera.
- **Domyślna izolacja**: Kontenery mają własne adresy IP i są izolowane od hosta, co poprawia bezpieczeństwo.

**Sieć host**:
- **Bezpośredni dostęp**: Kontenery używają sieci hosta, co może poprawić wydajność, ale może prowadzić do konfliktów portów.
- **Brak izolacji sieciowej**: Kontenery są mniej izolowane, co może zwiększać ryzyko problemów z bezpieczeństwem.

Przykładowe konfiguracje i komendy umożliwiające komunikację kontenerów w sieci bridge i host można dostosować do specyficznych potrzeb i wymagań środowiska, w którym są uruchamiane.
