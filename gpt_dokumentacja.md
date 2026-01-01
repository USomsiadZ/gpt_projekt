# Dokumentacja - gpt.ipynb

## Opis projektu

Ten notebook zawiera implementację serwera FastAPI wykorzystującego model GPT-2 do generowania tekstu. Projekt demonstruje podstawowe operacje na modelu językowym, w tym tokenizację, embeddingi, predykcje prawdopodobieństw oraz wizualizację wyników.

## Wymagania

Projekt wymaga następujących bibliotek:
- `transformers` - biblioteka Hugging Face do pracy z modelami NLP
- `torch` - PyTorch do obliczeń tensorowych
- `fastapi` - framework do tworzenia REST API
- `uvicorn` - serwer ASGI do uruchamiania FastAPI
- `nest-asyncio` - umożliwia uruchamianie asynchronicznego kodu w Jupyterze
- `matplotlib` - do wizualizacji danych

## Struktura notebooka

### Cell 0: Instalacja i inicjalizacja modelu

**Funkcjonalność:**
- Instaluje wymagane pakiety
- Ładuje model GPT-2 i tokenizer z Hugging Face
- Przenosi model na urządzenie (GPU jeśli dostępne, w przeciwnym razie CPU)
- Ustawia model w trybie ewaluacji (`model.eval()`)

**Kluczowe komponenty:**
- `GPT2Tokenizer` - tokenizer konwertujący tekst na tokeny
- `GPT2LMHeadModel` - model GPT-2 do generowania tekstu
- Automatyczne wykrywanie urządzenia (CUDA/CPU)

### Cell 1: Serwer FastAPI

**Funkcjonalność:**
Tworzy REST API z endpointem `/generate` do generowania tekstu.

**Endpoint:**
- **URL:** `GET /generate`
- **Parametry:**
  - `prompt` (str, wymagany) - tekst początkowy do generacji
  - `max_length` (int, opcjonalny, domyślnie 50) - maksymalna długość wygenerowanego tekstu
- **Zwraca:** JSON z wygenerowanym tekstem
  ```json
  {
    "generated_text": "wygenerowany tekst..."
  }
  ```

**Przykład użycia:**
```
GET http://127.0.0.1:5000/generate?prompt=Hej&max_length=50
```

**Uwagi techniczne:**
- Używa `nest_asyncio.apply()` aby umożliwić działanie asynchronicznego kodu w Jupyterze
- Serwer nasłuchuje na `127.0.0.1:5000`
- Generowanie używa `do_sample=True` dla bardziej zróżnicowanych wyników

### Cell 2: Tokenizacja i embeddingi

**Funkcjonalność:**
Demonstruje proces tokenizacji polskich słów i wyświetla informacje o embeddingach.

**Proces:**
1. Tokenizuje listę polskich słów: `["sztuczna", "inteligencja", "przyszłość"]`
2. Wyświetla tokeny dla każdego słowa
3. Pobiera embeddingi z warstwy `transformer.wte` (word token embeddings)
4. Wyświetla kształt embeddingów dla każdego tokena

**Wyniki:**
- Pokazuje jak słowa są dzielone na tokeny (może być wiele tokenów na słowo)
- Embeddingi mają kształt zgodny z rozmiarem modelu GPT-2

### Cell 3: Forward pass i prawdopodobieństwa

**Funkcjonalność:**
Wykonuje forward pass przez model i analizuje prawdopodobieństwa następnych tokenów.

**Proces:**
1. Tokenizuje prompt: `"Sztuczna inteligencja"`
2. Wykonuje forward pass przez model (bez generacji)
3. Pobiera logity (surowe prawdopodobieństwa) z ostatniego tokena
4. Stosuje softmax do konwersji logitów na prawdopodobieństwa
5. Wyświetla 100 najbardziej prawdopodobnych następnych tokenów z ich prawdopodobieństwami

**Kluczowe koncepty:**
- `logits` - surowe wyniki z modelu przed softmax
- `softmax` - normalizuje logity do prawdopodobieństw (suma = 1)
- `top_k` - wybiera k najbardziej prawdopodobnych opcji

### Cell 4: Wizualizacja prawdopodobieństw

**Funkcjonalność:**
Tworzy wykres słupkowy przedstawiający prawdopodobieństwa top 100 tokenów.

**Wizualizacja:**
- Wykres słupkowy (bar chart)
- Oś X: indeksy tokenów (0-99)
- Oś Y: prawdopodobieństwa
- Tytuł: "Top 100 prawdopodobnych tokenów"

## Uruchomienie

1. Otwórz notebook w Jupyter
2. Uruchom wszystkie komórki sekwencyjnie
3. Serwer FastAPI będzie dostępny na `http://127.0.0.1:5000`
4. Użyj endpointu `/generate` do generowania tekstu

## Uwagi

- Model GPT-2 jest modelem anglojęzycznym, więc wyniki dla polskiego tekstu mogą być mniej precyzyjne
- Tokenizacja polskich słów może rozbijać je na wiele tokenów
- Serwer działa synchronicznie w kontekście Jupytera dzięki `nest_asyncio`
- Aby zatrzymać serwer, użyj przerwania jądra (Kernel Interrupt)

## Rozszerzenia możliwe

- Dodanie obsługi innych modeli językowych (np. polskich modeli)
- Implementacja dodatkowych endpointów (np. batch processing)
- Dodanie parametrów generowania (temperature, top_p, top_k)
- Implementacja logowania i monitoringu
- Dodanie obsługi CORS dla aplikacji webowych
- Optymalizacja wydajności (np. caching, batching)

