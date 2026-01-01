# TODO

## Główne zadania

### 1. Uruchomić model GPT 2 wystawiając api RESTowe
- [x] Zainstalować wymagane biblioteki (transformers, torch, fastapi, uvicorn)
- [x] Załadować model GPT-2 i tokenizer
- [x] Utworzyć endpoint REST API z FastAPI (`/generate`)
- [x] Uruchomić serwer uvicorn

### 2. Mając zadany zestaw tokenów i kontekstów odpowiedzieć na pytania:

#### 2.1. Jak wygląda macierz embeding dla każdego z tych słów (bazowej - nie tej po transformacjach)
- [x] Zdefiniować zestaw słów do analizy
- [x] Tokenizować słowa
- [x] Pobrać macierz embeddingów bazowych (`model.transformer.wte.weight`)
- [x] Wyświetlić embeddingi dla każdego tokenu

#### 2.2. Z jakim prawdopodobieństwem jakie tokeny - 100 pierwszych tokenów wypisać i z jakim prawdopodobieństwem dany model chciałby uznać następny token za następne możliwe słowo
- [x] Przygotować prompt/kontekst
- [x] Wykonać forward pass modelu (bez generacji)
- [x] Pobrać logity dla ostatniego tokena
- [x] Zastosować softmax do obliczenia prawdopodobieństw
- [x] Wybrać top 100 najbardziej prawdopodobnych tokenów
- [x] Wyświetlić tokeny z ich prawdopodobieństwami
- [x] Utworzyć wizualizację (wykres słupkowy)

#### 2.3. Jak wygląda funkcja softmax
- [ ] Pokazać szczegółowo jak działa funkcja softmax
- [ ] Zilustrować transformację logitów → prawdopodobieństwa
- [ ] Pokazać właściwości softmax (suma = 1, wartości w zakresie [0,1])

#### 2.4. Jak wygląda funkcja prawdopodobieństwa dla tych rzeczy
- [ ] Pokazać szczegółowo funkcję prawdopodobieństwa
- [ ] Zilustrować rozkład prawdopodobieństw dla tokenów
- [ ] Pokazać jak prawdopodobieństwa są obliczane z logitów

