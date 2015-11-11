# Quick Start.
## 1.2. Welcome.
* C-534 jest aplikacja internetową, która służy do integracji z różnymi api. 

## 1.3. Basic Concepts.
* Mikro serwis  jest to główna część oprogramowania, odpowiedzialna za całą integracje platformy c-534 z systemami zewnętrznymi. Składa się z konektora wejściowego, transformacji i konektora wyjściowego.

* Transformacja jest to konwersja formatu danych otrzymanych przez konektor wejściowy do formatu danych, które mają być przesłane przez konektor wyjściowy.

* Konektor wejściowy jest to część mikro serwisu, odpowiedzialna za pobieranie, wysyłanie danych. Obsługuje tylko jeden format danych.

* Konektor wyjściowy jest to część mikro serwisu, odpowiedzialna za wysyłanie danych. Obsługuje tylko jeden format danych.

* Konektor aktywny (webhook) jest to konektor, który jest uruchamiany ręcznie  przez użytkownika.

* Konektor pasywny (trigger) jest to konektor, który może być uruchomiony automatycznie przez inny mikro serwis, zgodnie z harmonogramem.