<picture>
  <source media="(prefers-color-scheme: dark)" srcset="shots/banner-dark.webp">
  <img src="shots/banner-light.webp" alt="Navision — Ubuntu, которой управляет AI">
</picture>

**[Сайт Navision](https://snemesh.github.io/navision/)** · [Установка на Ubuntu](#установка-на-ubuntu) · [Remote Navision для Mac](#remote-navision-для-mac) · [Все сборки](https://github.com/snemesh/navision/releases)

Navision — рабочий стол для Ubuntu со своим компоновщиком Wayland. Помощник на вашей
подписке Claude Code или Codex пишет код и ведёт систему: «поставь Docker», «что грузит
сервер», «почини тест». Здесь лежат сайт и готовые сборки. Их публикует CI после каждого
изменения, которое прошло все проверки.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="shots/desk-dark.webp">
  <img src="shots/desk-light.webp" alt="Стол Navision: верхняя панель, Настройки с приветствием первого входа и Док внизу">
</picture>

## Установка на Ubuntu

Ubuntu Server или Desktop **26.04, x86_64**, видеокарта AMD, Intel или NVIDIA. Одна команда
в терминале:

```sh
curl -fsSL https://github.com/snemesh/navision/releases/download/latest-main/install.sh | sh
```

Команда спросит пароль `sudo`. Установщик сам посмотрит машину и поставит:

- недостающие пакеты Ubuntu (PipeWire, Xwayland, порталы, шрифты…);
- драйвер NVIDIA и `nvidia-drm.modeset=1`, если на машине NVIDIA (`--no-gpu-driver` — не трогать);
- саму систему в `/usr/lib/novaos` и её службы;
- вход: свой экран входа на Ubuntu Server или пункт в списке сеансов GDM/SDDM на Ubuntu Desktop;
- Google Chrome, Claude Desktop и Claude Code (`--no-extras` — без них).

В конце он скажет, что делать дальше: обычно перезагрузиться и войти. При первом входе
откроются Настройки → Аккаунты: там вы входите в Claude и вводите свои ключи. Повторный
запуск той же команды обновляет систему.

### Без интернета

Скачайте на другой машине [архив](https://github.com/snemesh/navision/releases/download/latest-main/novaos-x86_64.tar.gz)
и [install.sh](https://github.com/snemesh/navision/releases/download/latest-main/install.sh),
перенесите их и запустите `sh install.sh --file novaos-x86_64.tar.gz`. Пакеты Ubuntu всё равно
ставятся через apt.

### Удалить

С текстовой консоли (Ctrl+Alt+F2), не из самой системы:

```sh
sudo novaos-setup remove              # система, службы, вход
sudo novaos-setup remove --packages   # и пакеты, которые поставил установщик
```

## Remote Navision для Mac

**[Скачать RemoteNavision.dmg](https://github.com/snemesh/navision/releases/download/remote-navision-latest/RemoteNavision.dmg)**
(macOS, Apple Silicon, предварительная версия)

Navision на сервере Ubuntu без видеокарты, а весь интерфейс рисует ваш Mac: Док, окна, меню
и анимации отвечают сразу, даже через сеть.

1. Откройте dmg и перетащите Remote Navision в «Программы». Сборка не нотаризована, поэтому
   первый запуск — правой кнопкой и «Открыть». Если macOS всё равно не открывает:
   `xattr -dr com.apple.quarantine "/Applications/Remote Navision.app"`.
2. На сервере поставьте Navision той же командой, что [выше](#установка-на-ubuntu).
3. Вход на сервер — по ключу SSH без пароля (`ssh-copy-id user@server`), и на сервере открыты
   порты UDP 60100–60199.

## Что внутри

- **Помощник.** Claude Code в окне, а не в терминале: чат с проектами и историей. Работает
  официальный CLI вашего агента: Claude Code, Codex, OpenCode, Gemini CLI.
- **Агенты и root.** Команда агента от root проходит через окно пароля, где она видна целиком.
  Своя локальная LLM по адресу и ключу, дела по расписанию.
- **Голос.** Диктовка в любое поле, чтение ответов вслух и разговор с помощником.
- **Мониторинг, Терминал, Файлы, Редактор, Диски, Снимки и запись экрана.**
- **Плавно и экономно.** Кадр только при изменениях и по vblank, простой стол спит.
- **Программы и игры.** Chrome, Claude Desktop, Steam с игровым режимом, Wine.

<img src="shots/brain-light.webp" alt="Окно «Помощник»: проекты слева, ответ со ссылками на запись экрана">

Нашли ошибку — [напишите в issues](https://github.com/snemesh/navision/issues).
