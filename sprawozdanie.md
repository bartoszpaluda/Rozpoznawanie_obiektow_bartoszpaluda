**Szablon sprawozdania laboratoryjnego**

**Przedmiot:** Uczenie głębokie do rozpoznawania obiektów
**Zajęcia nr / temat:** Zajęcia 1 - Obraz jako dane; pierwszy klasyfikator obrazów (MLP)
**Autor:** Bartosz Paluda
**Data:** 20.10.2026

**1. Cel ćwiczenia**
Ćwiczenie miało na celu wytrenowanie i zbadanie klasyfikatora obrazów opartego na perceptronie wielowarstwowym dla zbioru FashionMnist. Należało zaimplenetować model bazowy i przetestować wpływ różnych architektur na dokładność klasyfikacji 

**2. Metoda i implementacja**
Do realizacji zadania wykorzystano język Python oraz biblioteki PyTorch, torchvision, matplotlib, pandas i scikit-learn. Zbiór FashionMNIST został znormalizowany przy użyciu wartości `mean=0.2860` i `std=0.3530`.
Przetestowano pięć wariantów architektury MLP:
- Baza: warstwy (256, 128)
- Wariant 2: warstwa (128,)
- Wariant 3: warstwa (512,)
- Wariant 4: warstwy (512, 256, 128)
- Wariant 5: warstwy (1024, 512)

Modele trenowano przez 8 epok, wykorzystując optymalizator Adam (`lr=1e-3`) oraz funkcję straty CrossEntropyLoss. Rozmiar batcha wynosił 128 dla zbioru treningowego i 256 dla testowego.

**3. Wyniki**
Zestawienie przetestowanych architektur:

| Architektura | Liczba parametrów | Dokładność [%] |
| :--- | :--- | :--- |
| baza (256, 128) | 235146 | 88.62 |
| (128,) | 101770 | 88.03 |
| (512,) | 407050 | 88.25 |
| (512, 256, 128) | 567434 | 88.60 |
| (1024, 512) | 1333770 | 89.34 |

Najlepszy wynik (89.34%) osiągnął model o warstwach ukrytych (1024, 512).

<img width="573" height="453" alt="image" src="https://github.com/user-attachments/assets/d26b77d4-6a98-4e19-96be-dfd7090b126a" />


<img width="1197" height="443" alt="image" src="https://github.com/user-attachments/assets/d11c3ffc-f9f5-4e29-81c8-42d195f79caf" />


<img width="787" height="702" alt="image" src="https://github.com/user-attachments/assets/e289ff5d-f35d-4aaa-8631-e28c78815579" />


**4. Analiza i interpretacja**
Krzywe uczenia dla najlepszego modelu pokazują, że model prawidłowo uczy się wzorców, a strata testowa stabilizuje się. Analiza macierzy pomyłek wskazuje, że najtrudniejszą parą klas dla modelu jest Shirt i T-shirt/top oraz Coat i Pullover, w 125 przypadkach klasą była Shirt, a model uznał ją za Tshirt/top, odwrotnie stało się to 72 razy. W drugim przypadku model rozpoznał Coat jako Pullover 103 razy, a odwrotnie 70 razy.

**5. Wnioski**
Eksperyment potwierdził zwiększenie dokładności z 88,62% do 89,34%, jednak ilość parametrów zwiększyła się z 235k do 1333k. Problemy z rozróżnianiem podobnych elementów garderoby (jak koszule i koszulki) są naturalnym ograniczeniem modeli MLP, które traktują piksele niezależnie. Aby poprawić ten wynik, należałoby zastosować konwolucyjne sieci neuronowe (CNN).
