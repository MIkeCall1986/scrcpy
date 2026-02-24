**This GitHub repo (<https://github.com/Genymobile/scrcpy>) is the only official
source for the project. Do not download releases from random websites, even if
their name contains `scrcpy`.**

# scrcpy (v3.3.4)

<img src="app/data/icon.svg" width="128" height="128" alt="scrcpy" align="right" />

_pronounced "**scr**een **c**o**py**"_

This application mirrors Android devices (video and audio) connected via USB or
[TCP/IP](doc/connection.md#tcpip-wireless) and allows control using the
computer's keyboard and mouse. It does not require _root_ access or an app
installed on the device. It works on _Linux_, _Windows_, and _macOS_.

![screenshot](assets/screenshot-debian-600.jpg)

It focuses on:

 - **lightness**: native, displays only the device screen
 - **performance**: 30~120fps, depending on the device
 - **quality**: 1920×1080 or above
 - **low latency**: [35~70ms][lowlatency]
 - **low startup time**: ~1 second to display the first image
 - **non-intrusiveness**: nothing is left installed on the Android device
 - **user benefits**: no account, no ads, no internet required
 - **freedom**: free and open source software

[lowlatency]: https://github.com/Genymobile/scrcpy/pull/646

Its features include:
 - [audio forwarding](doc/audio.md) (Android 11+)
 - [recording](doc/recording.md)
 - [virtual display](doc/virtual_display.md)
 - mirroring with [Android device screen off](doc/device.md#turn-screen-off)
 - [copy-paste](doc/control.md#copy-paste) in both directions
 - [configurable quality](doc/video.md)
 - [camera mirroring](doc/camera.md) (Android 12+)
 - [mirroring as a webcam (V4L2)](doc/v4l2.md) (Linux-only)
 - physical [keyboard][hid-keyboard] and [mouse][hid-mouse] simulation (HID)
 - [gamepad](doc/gamepad.md) support
 - [OTG mode](doc/otg.md)
 - and more…

[hid-keyboard]: doc/keyboard.md#physical-keyboard-simulation
[hid-mouse]: doc/mouse.md#physical-mouse-simulation

## Prerequisites

The Android device requires at least API 21 (Android 5.0).

[Audio forwarding](doc/audio.md) is supported for API >= 30 (Android 11+).

Make sure you [enabled USB debugging][enable-adb] on your device(s).

[enable-adb]: https://developer.android.com/studio/debug/dev-options#enable

On some devices (especially Xiaomi), you might get the following error:

```
Injecting input events requires the caller (or the source of the instrumentation, if any) to have the INJECT_EVENTS permission.
```

In that case, you need to enable [an additional option][control] `USB debugging
(Security Settings)` (this is an item different from `USB debugging`) to control
it using a keyboard and mouse. Rebooting the device is necessary once this
option is set.

[control]: https://github.com/Genymobile/scrcpy/issues/70#issuecomment-373286323

Note that USB debugging is not required to run scrcpy in [OTG mode](doc/otg.md).


## Get the app

 - [Linux](doc/linux.md)
 - [Windows](doc/windows.md) (read [how to run](doc/windows.md#run))
 - [macOS](doc/macos.md)


## Must-know tips

 - [Reducing resolution](doc/video.md#size) may greatly improve performance
   (`scrcpy -m1024`)
 - [_Right-click_](doc/mouse.md#mouse-bindings) triggers `BACK`
 - [_Middle-click_](doc/mouse.md#mouse-bindings) triggers `HOME`
 - <kbd>Alt</kbd>+<kbd>f</kbd> toggles [fullscreen](doc/window.md#fullscreen)
 - There are many other [shortcuts](doc/shortcuts.md)


## Usage examples

There are a lot of options, [documented](#user-documentation) in separate pages.
Here are just some common examples.

 - Capture the screen in H.265 (better quality), limit the size to 1920, limit
   the frame rate to 60fps, disable audio, and control the device by simulating
   a physical keyboard:

    ```bash
    scrcpy --video-codec=h265 --max-size=1920 --max-fps=60 --no-audio --keyboard=uhid
    scrcpy --video-codec=h265 -m1920 --max-fps=60 --no-audio -K  # short version
    ```

 - Start VLC in a new virtual display (separate from the device display):

    ```bash
    scrcpy --new-display=1920x1080 --start-app=org.videolan.vlc
    ```

 - Record the device camera in H.265 at 1920x1080 (and microphone) to an MP4
   file:

    ```bash
    scrcpy --video-source=camera --video-codec=h265 --camera-size=1920x1080 --record=file.mp4
    ```

 - Capture the device front camera and expose it as a webcam on the computer (on
   Linux):

    ```bash
    scrcpy --video-source=camera --camera-size=1920x1080 --camera-facing=front --v4l2-sink=/dev/video2 --no-playback
    ```

 - Control the device without mirroring by simulating a physical keyboard and
   mouse (USB debugging not required):

    ```bash
    scrcpy --otg
    ```

 - Control the device using gamepad controllers plugged into the computer:

    ```bash
    scrcpy --gamepad=uhid
    scrcpy -G  # short version
    ```

## User documentation

The application provides a lot of features and configuration options. They are
documented in the following pages:

 - [Connection](doc/connection.md)
 - [Video](doc/video.md)
 - [Audio](doc/audio.md)
 - [Control](doc/control.md)
 - [Keyboard](doc/keyboard.md)
 - [Mouse](doc/mouse.md)
 - [Gamepad](doc/gamepad.md)
 - [Device](doc/device.md)
 - [Window](doc/window.md)
 - [Recording](doc/recording.md)
 - [Virtual display](doc/virtual_display.md)
 - [Tunnels](doc/tunnels.md)
 - [OTG](doc/otg.md)
 - [Camera](doc/camera.md)
 - [Video4Linux](doc/v4l2.md)
 - [Shortcuts](doc/shortcuts.md)


## Resources

 - [FAQ](FAQ.md)
 - [Translations][wiki] (not necessarily up to date)
 - [Build instructions](doc/build.md)
 - [Developers](doc/develop.md)

[wiki]: https://github.com/Genymobile/scrcpy/wiki


## Articles

- [Introducing scrcpy][article-intro]
- [Scrcpy now works wirelessly][article-tcpip]
- [Scrcpy 2.0, with audio][article-scrcpy2]

[article-intro]: https://blog.rom1v.com/2018/03/introducing-scrcpy/
[article-tcpip]: https://www.genymotion.com/blog/open-source-project-scrcpy-now-works-wirelessly/
[article-scrcpy2]: https://blog.rom1v.com/2023/03/scrcpy-2-0-with-audio/

## Contact

You can open an [issue] for bug reports, feature requests or general questions.

For bug reports, please read the [FAQ](FAQ.md) first, you might find a solution
to your problem immediately.

[issue]: https://github.com/Genymobile/scrcpy/issues

You can also use:

 - Reddit: [`r/scrcpy`](https://www.reddit.com/r/scrcpy)
 - BlueSky: [`@scrcpy.bsky.social`](https://bsky.app/profile/scrcpy.bsky.social)
 - Twitter: [`@scrcpy_app`](https://twitter.com/scrcpy_app)


## Donate

I'm [@rom1v](https://github.com/rom1v), the author and maintainer of _scrcpy_.

If you appreciate this application, you can [support my open source
work][donate]:
 - [GitHub Sponsors](https://github.com/sponsors/rom1v)
 - [Liberapay](https://liberapay.com/rom1v/)
 - [PayPal](https://paypal.me/rom2v)

[donate]: https://blog.rom1v.com/about/#support-my-open-source-work

## License

    Copyright (C) 2018 Genymobile
    Copyright (C) 2018-2026 Romain Vimont

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

24.02.26 sync fork 
Ось результати аналізу та стратегія трансформації для проекту **scrcpy**, підготовлені у форматі для копіювання в Notion.

---

# 📑 Звіт AI-консультанта: Проект "scrcpy"

**scrcpy** (v3.3.4) — це високопродуктивний додаток з відкритим кодом, призначений для дзеркалювання екрана Android-пристроїв та керування ними з комп'ютера через USB або TCP/IP.

---

## 🧬 Частина 1: "ДНК" Проекту

Логіку коду проекту можна розбити на такі **атомарні функції**:

*   **Дзеркалювання відео та аудіо (Mirroring):** Трансляція екрана та звуку (для Android 11+) у реальному часі.
*   **Ін’єкція подій (Input Injection):** Симуляція фізичної клавіатури, миші та геймпада (HID) для дистанційного керування пристроєм.
*   **Медіа-обробка (Encoding/Decoding):** Кодування потоку (наприклад, H.265) для оптимізації якості та продуктивності.
*   **Синхронізація даних (Data Sync):** Двостороння передача тексту через буфер обміну та можливість запису екрана.
*   **Керування віртуальними дисплеями:** Створення окремих робочих областей, незалежних від основного екрана пристрою.
*   **Емуляція периферії:** Використання пристрою як веб-камери (V4L2) або робота в режимі OTG без USB-налагодження.

### 💎 Головна технічна цінність
Головна цінність проекту полягає в **екстремальній продуктивності та неінвазивності**. Він забезпечує мінімальну затримку (**35~70 мс**) та високу частоту кадрів (**30~120 fps**), не потребуючи *root*-прав або встановлення будь-якого ПЗ на Android-пристрій. Це робить його "золотим стандартом" для розробників та тестувальників.

---

## 🚀 Частина 2: "Трансформація" (Інтеграція з Gemini LLM)

Інтеграція з мультимодальною моделлю **Gemini** (через **GitHub Models**) перетворює scrcpy з інструмента віддаленого доступу на **автономного ШІ-оператора**.

### Як зміниться функціонал?
1.  **Візуальне розуміння контексту:** Gemini зможе аналізувати потік відео в реальному часі, розпізнаючи елементи інтерфейсу, текст та аномалії на екрані пристрою.
2.  **Семантичне керування:** Користувач зможе віддавати команди природною мовою (наприклад: *"Знайди в налаштуваннях додаток X і видали його"*), а Gemini через scrcpy самостійно виконає серію кліків.
3.  **Автоматизоване тестування (QA):** ШІ зможе самостійно проходити сценарії тестування, ідентифікуючи баги верстки або логічні помилки в реальних умовах Android-середовища.

### Сценарій сервісу "Remote AI Device Lab" (scrcpy + Gemini + ваші ID_{$})

Сценарій створення інтелектуальної ферми пристроїв на вашому сайті:
1.  **Запит клієнта:** Користувач завантажує APK-файл на ваш сайт для перевірки.
2.  **Запуск (ID_{$1}):** Ваш Python-скрипт **ID_{$1}** ініціалізує scrcpy з параметром запису (`--record=file.mp4`) та запускає встановлення додатка.
3.  **Аналіз (Gemini):** Відеопотік передається в Gemini. Модель аналізує поведінку додатка, шукає критичні помилки та фіксує продуктивність.
4.  **Дія (ID_{$2}):** Якщо Gemini помічає "зависання", скрипт **ID_{$2}** через CLI-команди scrcpy перезавантажує пристрій або очищує кеш.
5.  **Звіт:** Використовуючи **GitHub Spark**, ви розгортаєте дашборд для клієнта, де відображається відеозапис тестування з коментарями ШІ щодо кожної помилки.

---

## 📋 План дій для Notion
| Крок | Дія | Результат |
| :--- | :--- | :--- |
| **1** | Розгортання через `scrcpy --otg` для початкового налаштування | Доступ до пристрою без дебагу |
| **2** | Підключення Gemini API для аналізу скріншотів | Інтелектуальний моніторинг |
| **3** | Зв'язування з вашими скриптами `ID_{$}` | Автоматизація життєвого циклу пристрою |
| **4** | Створення інтерфейсу в **GitHub Spark** | Готовий клієнтський сервіс |

---

### 💡 Резюме

**Суть:** **Дзеркалювання та керування Android-пристроями**.

**AI-Роль:** **Створення інтелектуальних застосунків через Spark**.
