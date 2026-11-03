# 🐍 PyOS — mini system operacyjny w przeglądarce

Jeden plik HTML, który udaje mały system operacyjny działający w przeglądarce.

🌍 **Wersja online (GitHub Pages):** https://v4786669-sudo.github.io/pyos/

## Co jest w środku

- 🖥️ **Pulpit** z ikonami, przeciąganymi oknami (zmiana rozmiaru, minimalizacja, maksymalizacja), paskiem zadań, menu Start, tapetami i ekranem wyłączania/restartu
- 🐍 **Terminal, którego głównym językiem jest Python 3** — pełny interpreter CPython (Pyodide/WebAssembly) działa w przeglądarce, bez serwera
- 🌐 **Przeglądarka** stron (iframe) z paskiem adresu, historią i szybkimi linkami
- 📁 **Menedżer plików** — trwały dysk wirtualny (localStorage): przeglądanie, tworzenie, usuwanie, import z dysku, pobieranie
- 📝 **Edytor** tekstu i kodu z zapisem na wirtualny dysk
- 🔌 **Python steruje systemem**: `open_url()`, `search()`, `notify()`, `wallpaper()`, `shutdown()`, `reboot()`, `files()`, `editor()`, `ls()`, `cat()`, `rm()`… (pełna lista w `help()`)

## Uruchomienie

1. **Najprościej:** otwórz `index.html` w przeglądarce (klik dwukrotnie), **albo**
2. Serwer lokalny (zalecane — działa wtedy przerwanie Ctrl+C dla zapętlonych programów):

```bash
cd pyos
python3 -m http.server 8123
# wejdź na http://localhost:8123
```

## Przykłady do wpisania w terminalu

```python
>>> for i in range(3): print('PyOS', i)
>>> open_url('https://pl.wikipedia.org')
>>> notify('Cześć!')
>>> wallpaper('matrix')
>>> exec(open('hello.py').read())
```

## Uwagi i ograniczenia

- **Pierwsze uruchomienie wymaga internetu** — Pyodide (~10 MB) pobiera się z CDN, potem działa z pamięci podręcznej przeglądarki.
- **Google/YouTube nie otworzą się** w wewnętrznej przeglądarce (nagłówek `X-Frame-Options`). Działają np. Wikipedia, OpenStreetMap, DuckDuckGo Lite.
- Długa pętla Pythona może na chwilę zamrozić kartę — interpreter działa w tym samym wątku co interfejs (mini-VM w jednym wątku). Ctrl+C działa w przerwie między programami (anuluje wpisywaną linię); przerwanie *działającego* programu wymagałoby nagłówków cross-origin isolation, które zepsułyby wbudowaną przeglądarkę — kod próbuje to ustawić, jeśli środowisko na to pozwala.
- Dysk wirtualny ma limit localStorage (~5 MB).
