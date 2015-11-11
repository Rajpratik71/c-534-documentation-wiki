## 1. Welcome.
    C-534 jest aplikacja internetową, która służy do integracji z różnymi api. 

## 2. Basic Concepts.
1. **Mikro serwis**  jest to główna część oprogramowania, odpowiedzialna za całą integracje platformy c-534 z      systemami zewnętrznymi. Składa się z konektora wejściowego, transformacji i konektora wyjściowego.

2. **Transformacja** jest to konwersja formatu danych otrzymanych przez konektor wejściowy do formatu danych, które mają być przesłane przez konektor wyjściowy.

3. **Konektor wejściowy** jest to część mikro serwisu, odpowiedzialna za pobieranie, wysyłanie danych. Obsługuje tylko jeden format danych.

4. **Konektor wyjściowy** jest to część mikro serwisu, odpowiedzialna za wysyłanie danych. Obsługuje tylko jeden format danych.
    
5.  **Konektor aktywny** (webhook) jest to konektor, który jest uruchamiany ręcznie  przez użytkownika.

6. **Konektor pasywny** (trigger) jest to konektor, który może być uruchomiony automatycznie przez inny mikro serwis, zgodnie z harmonogramem.