
# Chaos Engineering with Observability in Kubernetes (Project Type 1)

## Project Description
Celem projektu jest stworzenie zaawansowanego środowiska testowego dla aplikacji działających w Kubernetes, które umożliwia przeprowadzanie kontrolowanych eksperymentów awarii (Chaos Engineering) oraz ich dogłębną analizę przy użyciu narzędzi obserwowalności.

Projekt skupia się na symulowaniu realistycznych scenariuszy awarii, takich jak utrata nodów, restarty podów czy degradacja sieci, a następnie analizie ich wpływu na wydajność, dostępność i stabilność systemu. Dzięki integracji z OpenTelemetry oraz Grafana możliwe jest uzyskanie pełnego obrazu zachowania systemu w czasie rzeczywistym.

Częścią projektu jest integracje LLM przez serwer MCP do symulacji ruchu sieciowego w aplikacji, która będzie poddawana rónym scenariuszom testowym wygenerowanych przez Chaos-K.


---


## Project Goals

- Testowanie odporności systemu na awarie infrastruktury
- Identyfikacja wąskich gardeł i problemów wydajnościowych
- Integracja Chaos Engineering z Observability
- Integracja Chaos-K z LLM + MCP Server

---

## Podstawy teoretyczne
Chaos-K (Krkn) jest narzędziem do chaos engineering w Kubernetes, którego celem jest świadome wprowadzanie awarii w systemie w celu oceny jego odporności, identyfikacji wąskich gardeł oraz poprawy stabilności i wydajności. Narzędzie pozwala na wstrzykiwanie różnych typów awarii, takich jak restart podów, przeciążenie CPU lub pamięci, awarie sieci czy niedostępność węzłów, w kontrolowanym zakresie wybranych namespace’ów, deploymentów lub węzłów. Proces testowy obejmuje definicję scenariusza chaos, wykonanie wstrzyknięcia awarii w Kubernetes za pomocą API, obserwację reakcji systemu poprzez narzędzia monitorujące (np. OpenTelemetry, Prometheus) oraz wizualizację danych w Grafanie, a następnie analizę wyników w celu wyciągnięcia wniosków i iteracyjnego doskonalenia odporności systemu. Chaos-K działa zgodnie z podstawowymi zasadami chaos engineering: zaczynanie od małego wpływu, używanie rzeczywistych metryk systemowych, kontrolowanie zakresu testów i stopniowe rozszerzanie testów w oparciu o zdobyte doświadczenie.

---


## High-Level Architecture

System składa się z czterech głównych warstw:

### 1. LLM + MCP
Symuluje ruch sieciowy (generuje scenariusze Haosu)
- strzela na endpointy z różną częstotliwością

### 2. Chaos Layer
Narzędzie Kraken odpowiada za wstrzykiwanie awarii do klastra Kubernetes:
- usuwanie nodów
- restart podów
- symulacja problemów sieciowych

### 3. Observability Layer
- OpenTelemetry zbiera metryki, logi i trace’y
- Loki/ELK przechowuje logi

### 4. Visualization Layer
- Grafana prezentuje dane w czasie rzeczywistym
- Dashboardy pokazują wpływ awarii na system

<img width="789" height="377" alt="schemat-u" src="https://github.com/user-attachments/assets/d559b5b6-9a6d-4ffd-840a-e2323bc9bf36" />




---

## Case Study: Odporność aplikacji Bookinfo na trudne warunki sieciowe i awarie infrastruktury

Celem eksperymentu było przetestowanie odporności aplikacji Bookinfo (https://istio.io/latest/docs/examples/bookinfo/) działającej w Kubernetes (k3d) na trudne warunki sieciowe i awarie infrastruktury przy użyciu narzędzi Chaos Engineering (Kraken) oraz obserwowalności (OpenTelemetry + Grafana).


### Scenariusz
- Usunięcie poda z klastra
- Restart kluczowych podów
- Dodanie opóźnienia sieciowego
- Zabranie większości zasobów CPU

---

## Technology Stack

| Technology | Zastosowanie |
|------------|--------------|
| Kubernetes (k3d) | Uruchamianie i zarządzanie klastrem aplikacji. |
| Kraken (Chaos Engineering) | Wstrzykiwanie awarii i testowanie odporności systemu. |
| OpenTelemetry | Zbieranie metryk, logów i trace’ów dla obserwowalności. |
| Grafana | Wizualizacja metryk i tworzenie dashboardów w czasie rzeczywistym. |
| MCP | Symulacja ruchu sieciowego i generowanie scenariuszy testowych. |
| REST API | Komunikacja i automatyzacja testów między komponentami. |
| LLM (OpenAPI) | Generowanie dynamicznych scenariuszy i analiza wyników. |


