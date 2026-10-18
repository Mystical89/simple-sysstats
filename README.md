**English** | [Русский](#russian)

# Simple sysstats for Omarchy

CPU, GPU, RAM and disk usage (with CPU/GPU temperatures) for the Omarchy bar.

![Simple sysstats in the Omarchy bar](preview.png)

Hover any stat for details:

| CPU | GPU |
|---|---|
| ![CPU tooltip](screenshots/tooltip-cpu.png) | ![GPU tooltip](screenshots/tooltip-gpu.png) |
| **RAM** | **Disk** |
| ![RAM tooltip](screenshots/tooltip-ram.png) | ![Disk tooltip](screenshots/tooltip-disk.png) |

- **Lightweight.** CPU, RAM, temperatures and AMD GPU figures are read straight from `/proc` and `/sys` inside the shell, with no scripts or subprocesses on each refresh. Only disk usage (`df`) and NVIDIA GPUs (`nvidia-smi`) run a command.
- **Hardware detection.** CPU temperature from `k10temp`/`zenpower` (AMD), `coretemp` (Intel), `x86_pkg_temp`, `cpu_thermal` (ARM) or `acpitz`. GPU from AMD sysfs or `nvidia-smi`; the discrete GPU is picked automatically.
- **Three views.** Left-click cycles between all values, first value only and icon only. The choice is shared across monitors and kept across restarts.
- **Warnings.** The widget turns the theme's urgent colour at 90% usage or 85 °C (configurable).
- Hover for details (load average, swap, VRAM, free space). Right-click opens `btop`.

## Install

```bash
omarchy plugin add https://github.com/Mystical89/simple-sysstats.git --enable
```

This is a fork of [AlexMedela/simple-sysstats](https://github.com/AlexMedela/simple-sysstats)
— see [This fork](#this-fork) for what it changes. It keeps the upstream plugin
id `amedela.simple-sysstats`, so installing it replaces an upstream copy and
your existing bar entries keep working.

The widget is added once, showing CPU. Add it again for each stat you want and set its `stat` in the bar settings panel or in `~/.config/omarchy/shell.json`:

```json
"right": [
  { "id": "amedela.simple-sysstats", "stat": "CPU" },
  { "id": "amedela.simple-sysstats", "stat": "GPU" },
  { "id": "amedela.simple-sysstats", "stat": "RAM" },
  { "id": "amedela.simple-sysstats", "stat": "Disk", "mount": "/" }
]
```

## Settings

| Key | Default | Description |
|---|---|---|
| `stat` | `CPU` | `CPU`, `GPU`, `RAM` or `Disk` |
| `interval` | `3` (`30` for disk) | Refresh interval in seconds |
| `showTemperature` | `true` | Show CPU/GPU temperature |
| `mount` | `/` | Disk only: filesystem to report |
| `gpuCard` | auto | GPU only: pin a DRM card, e.g. `card1` |
| `usageThreshold` | `90` | Usage (%) that triggers the warning colour |
| `temperatureThreshold` | `85` | Temperature (°C) that triggers the warning colour |
| `onRightClick` | `omarchy-launch-or-focus-tui btop` | Command on right-click |
| `onMiddleClick` | — | Command on middle-click |
| `icon`, `iconSize`, `fontSize` | auto | Override the Nerd Font glyph and sizes |
| `viewMode` | `0` | Starting view: `0` all values, `1` first value, `2` icon only |
| `padding` | `9` | Space around the pill; it is the only gap between two sysstats widgets |

## Hardware support

| | Usage | Temperature |
|---|---|---|
| AMD CPU | ✅ | ✅ `k10temp` / `zenpower` |
| Intel CPU | ✅ | ✅ `coretemp` |
| AMD GPU (amdgpu) | ✅ | ✅ |
| NVIDIA GPU | ✅ needs `nvidia-smi` (proprietary driver) | ✅ |
| Intel GPU | ❌ not exposed by the driver (shows N/A) | — |

## Uninstall

```bash
omarchy plugin remove amedela.simple-sysstats
```

That unloads the widget from the shell and deletes the plugin folder; the bar
entries stay in `shell.json`, so a later `omarchy plugin add` brings the same
widgets back. Remove them by hand if you don't want that.

## This fork

Fork of [AlexMedela/simple-sysstats](https://github.com/AlexMedela/simple-sysstats)
that matches the stock Omarchy bar typography out of the box:

- values use `Style.font.body` (12) instead of `body + 2`;
- the icon is drawn with `OpticalGlyph` in a `Style.bar.iconCanvas` (16) box at
  `Style.bar.iconFont` (13) instead of a plain 15 px `Text`, so the glyph is
  optically centred like every other bar icon;
- icon-to-text spacing and the pill padding come from `Style.space(...)`
  (3 and 17), so they scale with the bar's font size.

Nothing else changes: same settings, same behaviour, `fontSize` / `iconSize`
still override the new defaults.

## License

MIT

---

<a id="russian"></a>

## Русский

[↑ English](#simple-sysstats-for-omarchy)

Форк [AlexMedela/simple-sysstats](https://github.com/AlexMedela/simple-sysstats):
загрузка CPU, GPU, RAM и диска (с температурами CPU/GPU) для бара Omarchy,
приведённая к типографике штатного бара.

![Simple sysstats в баре Omarchy](preview.png)

Наведение на показатель показывает подробности:

| CPU | GPU |
|---|---|
| ![Подсказка CPU](screenshots/tooltip-cpu.png) | ![Подсказка GPU](screenshots/tooltip-gpu.png) |
| **RAM** | **Disk** |
| ![Подсказка RAM](screenshots/tooltip-ram.png) | ![Подсказка Disk](screenshots/tooltip-disk.png) |

- **Лёгкий.** CPU, RAM, температуры и показатели AMD GPU читаются прямо из
  `/proc` и `/sys` внутри shell — без скриптов и подпроцессов на каждое
  обновление. Команды запускаются только для диска (`df`) и NVIDIA GPU
  (`nvidia-smi`).
- **Определение железа.** Температура CPU: `k10temp`/`zenpower` (AMD),
  `coretemp` (Intel), `x86_pkg_temp`, `cpu_thermal` (ARM) или `acpitz`.
  GPU — через sysfs AMD или `nvidia-smi`; дискретная карта выбирается
  автоматически.
- **Три режима просмотра.** Левый клик циклит «все значения → первое значение →
  только иконка». Выбор общий для всех мониторов и сохраняется между
  перезапусками.
- **Предупреждения.** При 90 % загрузки или 85 °C виджет красится в urgent-цвет
  темы (пороги настраиваются).
- Наведение — подробности (load average, swap, VRAM, свободное место). Правый
  клик открывает `btop`.

### Установка

```bash
omarchy plugin add https://github.com/Mystical89/simple-sysstats.git --enable
```

Это форк [AlexMedela/simple-sysstats](https://github.com/AlexMedela/simple-sysstats)
(отличия — в разделе «Этот форк» ниже). ID плагина оставлен апстримным
(`amedela.simple-sysstats`), поэтому установка заменяет апстримную копию, а
записи виджетов в баре продолжают работать.

Виджет добавляется один раз, с показателем CPU. Чтобы добавить ещё показатели,
вставьте его повторно и задайте `stat` в панели настроек бара или в
`~/.config/omarchy/shell.json`:

```json
"right": [
  { "id": "amedela.simple-sysstats", "stat": "CPU" },
  { "id": "amedela.simple-sysstats", "stat": "GPU" },
  { "id": "amedela.simple-sysstats", "stat": "RAM" },
  { "id": "amedela.simple-sysstats", "stat": "Disk", "mount": "/" }
]
```

### Настройки

| Ключ | По умолчанию | Описание |
|---|---|---|
| `stat` | `CPU` | `CPU`, `GPU`, `RAM` или `Disk` |
| `interval` | `3` (`30` для диска) | Интервал обновления, секунды |
| `showTemperature` | `true` | Показывать температуру CPU/GPU |
| `mount` | `/` | Только для диска: какой файловой системой считать |
| `gpuCard` | авто | Только для GPU: закрепить DRM-карту, например `card1` |
| `usageThreshold` | `90` | Загрузка (%), при которой включается цвет предупреждения |
| `temperatureThreshold` | `85` | Температура (°C), при которой включается цвет предупреждения |
| `onRightClick` | `omarchy-launch-or-focus-tui btop` | Команда по правому клику |
| `onMiddleClick` | — | Команда по среднему клику |
| `icon`, `iconSize`, `fontSize` | авто | Переопределить глиф Nerd Font и размеры |
| `viewMode` | `0` | Стартовый режим: `0` все значения, `1` первое, `2` только иконка |
| `padding` | `9` | Отступ вокруг плашки; он же единственный зазор между двумя виджетами sysstats |

### Поддержка железа

| | Загрузка | Температура |
|---|---|---|
| AMD CPU | ✅ | ✅ `k10temp` / `zenpower` |
| Intel CPU | ✅ | ✅ `coretemp` |
| AMD GPU (amdgpu) | ✅ | ✅ |
| NVIDIA GPU | ✅ нужен `nvidia-smi` (проприетарный драйвер) | ✅ |
| Intel GPU | ❌ драйвер не отдаёт загрузку (показывает N/A) | — |

### Удаление

```bash
omarchy plugin remove amedela.simple-sysstats
```

Команда выгружает виджет из shell и удаляет каталог плагина; записи в
`shell.json` остаются, поэтому повторный `omarchy plugin add` вернёт те же
виджеты. Если это не нужно — удалите записи вручную.

### Этот форк

Форк [AlexMedela/simple-sysstats](https://github.com/AlexMedela/simple-sysstats),
который сразу выглядит как штатный бар Omarchy:

- значения набраны `Style.font.body` (12) вместо `body + 2`;
- иконка рисуется `OpticalGlyph` в канве `Style.bar.iconCanvas` (16) размером
  `Style.bar.iconFont` (13) вместо обычного `Text` на 15 px — глиф
  оптически центрируется, как у остальных иконок бара;
- отступ иконка↔текст и поля пилюли берутся из `Style.space(...)` (3 и 17),
  поэтому масштабируются вместе с размером шрифта бара.

Больше ничего не меняется: те же настройки, то же поведение, `fontSize` /
`iconSize` по-прежнему переопределяют новые значения по умолчанию.

### Лицензия

MIT
