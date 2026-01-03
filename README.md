# 🤖 Python Voice Assistant (JARVIS-like)

Простой план и дорожная карта, чтобы **с нуля** собрать голосового ассистента на Python, который принимает команды, отвечает голосом и выполняет действия.

> Проект рассчитан на **нулевые знания**. Идём по шагам.

---

## 🎯 Цель проекта

Сделать ассистента, который:

* слушает голосовые команды
* понимает текст команды
* отвечает голосом
* выполняет действия (открыть сайт, сказать время, запустить программу и т.д.)
* легко расширяется

---

## 🧠 Что в итоге получится

* Ассистент в стиле **JARVIS** (без ИИ сначала, потом добавим)
* Запуск одной командой
* Модульная структура (легко добавлять новые команды)

---

## 🧱 Технологии

* Python 3.10+
* SpeechRecognition — распознавание речи
* pyttsx3 — синтез речи (offline)
* pyaudio — микрофон
* os / webbrowser — системные команды
* (позже) OpenAI API / LLM

---

## 📁 Структура проекта

```
jarvis-assistant/
│
├─ README.md          # этот файл
├─ main.py            # точка входа
├─ requirements.txt   # зависимости
│
├─ core/
│   ├─ listener.py    # слушает микрофон
│   ├─ speaker.py     # говорит
│   ├─ commands.py    # логика команд
│   └─ config.py      # настройки
│
└─ skills/
    ├─ time_skill.py
    ├─ browser_skill.py
    └─ system_skill.py
```

---

## 🛣️ Путь обучения (ШАГИ)

### ШАГ 0. Установка

1. Установи Python: [https://www.python.org](https://www.python.org)
2. Проверь:

```
python --version
```

---

### ШАГ 1. Создание проекта

```
mkdir jarvis-assistant
cd jarvis-assistant
```

Создай виртуальное окружение:

```
python -m venv venv
```

Активируй:

* Windows:

```
venv\Scripts\activate
```

* Mac/Linux:

```
source venv/bin/activate
```

---

### ШАГ 2. Установка библиотек

```
pip install SpeechRecognition pyttsx3 pyaudio
```

Если pyaudio не ставится — **это нормально**, будем фиксить отдельно.

`requirements.txt`

```
SpeechRecognition
pyttsx3
pyaudio
```

---

### ШАГ 3. Ассистент говорит

`core/speaker.py`

```python
import pyttsx3

engine = pyttsx3.init()

def say(text):
    engine.say(text)
    engine.runAndWait()
```

---

### ШАГ 4. Ассистент слушает

`core/listener.py`

```python
import speech_recognition as sr

r = sr.Recognizer()

def listen():
    with sr.Microphone() as source:
        print("Слушаю...")
        audio = r.listen(source)
    try:
        return r.recognize_google(audio, language="ru-RU").lower()
    except:
        return ""
```

---

### ШАГ 5. Команды

`core/commands.py`

```python
import webbrowser
from datetime import datetime


def handle(command):
    if "время" in command:
        return f"Сейчас {datetime.now().strftime('%H:%M')}"

    if "ютуб" in command:
        webbrowser.open("https://youtube.com")
        return "Открываю YouTube"

    return "Я не понял команду"
```

---

### ШАГ 6. Главный файл

`main.py`

```python
from core.listener import listen
from core.speaker import say
from core.commands import handle

say("Ассистент запущен")

while True:
    command = listen()
    if command:
        response = handle(command)
        say(response)
```

---

## 🚀 Запуск

```
python main.py
```

---

## 🔮 Что добавлять дальше

* активация по слову ("Джарвис")
* ИИ (GPT)
* управление файлами
* управление ПК
* GUI
* автозапуск

---

## 🧠 Принцип

> Ассистент = **слушает → думает → действует → говорит**

---

## ⚠️ Важно

* Не пугайся ошибок — это нормально
* Делай по шагам
* Ассистент растёт вместе с тобой

---

## 🏁 Итог

Если хочешь — дальше могу:

* объяснять **каждую строку кода**
* помочь установить pyaudio
* превратить это в реального JARVIS 😎

Скажи, с какого шага начинаем.
