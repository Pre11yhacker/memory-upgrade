<div align="center">

<img src="assets/memory-upgrade-banner.svg" alt="Memory Upgrade — persistent project context for AI agents" width="100%">

<p>
  <strong>Память проекта для AI-агентов</strong><br>
  Сохраняйте важный контекст между сессиями и продолжайте работу без повторного погружения.
</p>

<p>
  <a href="#возможности">Возможности</a> &nbsp;·&nbsp;
  <a href="#как-это-работает">Как работает</a> &nbsp;·&nbsp;
  <a href="#установка">Установка</a> &nbsp;·&nbsp;
  <a href="#безопасность">Безопасность</a> &nbsp;·&nbsp;
  <a href="#контакты">Контакты</a>
</p>

<a href="https://agentskills.io/specification"><img src="https://img.shields.io/badge/format-Agent%20Skills-8B5CF6?style=flat-square&labelColor=171020" alt="Agent Skills"></a>
<img src="https://img.shields.io/badge/workflow-restore%20%2F%20record%20%2F%20resume-6D28D9?style=flat-square&labelColor=171020" alt="Restore Record Resume">
<a href="https://github.com/Pre11yhacker/memory-upgrade"><img src="https://img.shields.io/github/stars/Pre11yhacker/memory-upgrade?style=flat-square&color=A78BFA&labelColor=171020" alt="GitHub stars"></a>

</div>

---

## О проекте

**Memory Upgrade** — переносимый навык в формате [Agent Skills](https://agentskills.io/specification), который помогает AI-агентам вести компактную рабочую память проекта в файле `SESSION_MEMORY.md`.

Вместо того чтобы полагаться только на историю чата, агент сохраняет то, что действительно понадобится дальше: текущее состояние проекта, важные решения, ограничения, результаты проверок и ближайший следующий шаг.

При запуске новой сессии память перечитывается и сверяется с реальным состоянием файлов. Это помогает продолжить работу с нужного места, а не восстанавливать контекст с нуля.

> **Идея:** не архивировать весь диалог, а сохранять рабочее состояние проекта — кратко, проверяемо и пригодно для продолжения.

## Возможности

<table>
  <tr>
    <td width="50%">
      <strong>Контекст между сессиями</strong><br>
      <sub>Сохраняет состояние проекта и помогает восстановить ход работы после перезапуска агента.</sub>
    </td>
    <td width="50%">
      <strong>Память по делу</strong><br>
      <sub>Фиксирует решения, ограничения, результаты и незавершённые задачи вместо стенограммы чата.</sub>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Сверка с проектом</strong><br>
      <sub>Заметки проверяются по актуальным файлам, чтобы устаревший контекст не становился источником истины.</sub>
    </td>
    <td>
      <strong>Понятная точка продолжения</strong><br>
      <sub>В памяти остаётся следующий практический шаг, а не только список уже сделанного.</sub>
    </td>
  </tr>
</table>

### Что попадает в память

| Блок | Что содержит |
|---|---|
| Состояние | Цель проекта, текущий статус и ближайший шаг |
| Контекст | Архитектура, требования, важные ограничения |
| Решения | Выбранные подходы и причины выбора |
| Прогресс | Выполненные действия и подтверждённые результаты |
| Открытые вопросы | Блокеры, риски и незавершённые задачи |

## Как это работает

<div align="center">
  <sub>Один файл памяти связывает последовательные рабочие сессии</sub>
</div>

```mermaid
flowchart TD
    A["Новая сессия"] --> B["Прочитать SESSION_MEMORY.md"]
    B --> C["Сверить заметки с файлами проекта"]
    C --> D["Продолжить текущую задачу"]
    D --> E["Зафиксировать решения и результаты"]
    E --> F["Обновить следующий шаг"]
    F --> B

    classDef step fill:#171020,stroke:#8B5CF6,color:#EDE9FE,stroke-width:1px
    class A,B,C,D,E,F step
```

| Этап | Действие агента |
|---|---|
| **01 · Restore** | Читает сохранённую память и проверяет её актуальность |
| **02 · Work** | Выполняет задачу, отмечая важные изменения и решения |
| **03 · Checkpoint** | Обновляет память по ходу работы и перед завершением сессии |
| **04 · Resume** | Следующая сессия начинает с проверенного состояния проекта |

## Установка

Memory Upgrade можно установить через официальный CLI экосистемы Agent Skills — `npx skills`. Команда скачает навык из GitHub и разместит его в каталоге, который использует выбранный агент.

**Требования:** Node.js 22.20.0 или новее и npm.

### OpenAI Codex

Выполните в терминале из корня проекта:

```bash
npx -y skills add Pre11yhacker/memory-upgrade --skill memory-upgrade -a codex
```

### Claude Code

```bash
npx -y skills add Pre11yhacker/memory-upgrade --skill memory-upgrade -a claude-code
```

### Cursor

```bash
npx -y skills add Pre11yhacker/memory-upgrade --skill memory-upgrade -a cursor
```

### GitHub Copilot

```bash
npx -y skills add Pre11yhacker/memory-upgrade --skill memory-upgrade -a github-copilot
```

### OpenCode

```bash
npx -y skills add Pre11yhacker/memory-upgrade --skill memory-upgrade -a opencode
```

### Установка для всех проектов

По умолчанию CLI устанавливает навык в текущий проект. Чтобы сделать его доступным во всех проектах пользователя, добавьте флаг `-g`:

```bash
npx -y skills add Pre11yhacker/memory-upgrade --skill memory-upgrade -a codex -g
```

Замените `codex` на нужный идентификатор агента из инструкций выше. Устанавливайте навык отдельно для каждой среды, которой пользуетесь.

### Установка по промту (без ручного ввода команд)

Если вы работаете с AI-агентом в терминале или IDE, можно просто отправить ему следующий промт. Агент должен определить свою среду, установить Memory Upgrade подходящим способом и проверить результат.

Скопируйте и отправьте агенту:

```text
Установи для себя навык Memory Upgrade из репозитория:
https://github.com/Pre11yhacker/memory-upgrade

Сначала определи, в какой среде ты работаешь (OpenAI Codex, Claude Code, Cursor, GitHub Copilot, OpenCode или другая), и используй официальный CLI Agent Skills:

npx -y skills add Pre11yhacker/memory-upgrade --skill memory-upgrade -a <agent-id>

Подставь вместо <agent-id> идентификатор моей среды:
- codex — OpenAI Codex
- claude-code — Claude Code
- cursor — Cursor
- github-copilot — GitHub Copilot
- opencode — OpenCode

Устанавливай навык в текущий проект, если я явно не попросил глобальную установку. Если CLI недоступен или моя среда не поддерживается, изучи README репозитория и установи навык вручную в правильный каталог этой среды.

После установки:
1. Проверь, что каталог memory-upgrade и файл SKILL.md действительно появились в нужном месте.
2. Убедись, что агентная среда сможет обнаружить навык; если требуется, сообщи, нужно ли перезапустить её.
3. Кратко объясни, что было установлено и где.
4. Не создавай SESSION_MEMORY.md заранее — дождись реальной работы над проектом или отдельной просьбы.
5. Не изменяй существующие инструкции проекта и другие файлы без необходимости.

Если установка не удалась, не утверждай обратное: покажи ошибку и предложи корректный способ установки.
```

### Проверка установки

Посмотреть установленные навыки можно командой:

```bash
npx skills list
```

После установки откройте или перезапустите агентную среду, если навык не появился сразу. Memory Upgrade рассчитан на автоматическое применение агентом при работе над проектом — отдельная команда для каждого запуска не нужна.

<details>
<summary><strong>Ручная установка и постоянные инструкции проекта</strong></summary>

Если вы не хотите использовать CLI, скопируйте каталог `skills/memory-upgrade` целиком в каталог навыков нужного агента:

| Агент | Каталог проекта | Каталог пользователя |
|---|---|---|
| Codex | `.agents/skills/memory-upgrade/` | `~/.agents/skills/memory-upgrade/` |
| Claude Code | `.claude/skills/memory-upgrade/` | `~/.claude/skills/memory-upgrade/` |
| Cursor | `.cursor/skills/memory-upgrade/` | `~/.cursor/skills/memory-upgrade/` |
| GitHub Copilot | `.github/skills/memory-upgrade/` | `~/.copilot/skills/memory-upgrade/` |
| OpenCode | `.opencode/skills/memory-upgrade/` | `~/.config/opencode/skills/memory-upgrade/` |

Для сред, которые загружают `AGENTS.md` как инструкции проекта, дополнительно скопируйте `skills/memory-upgrade/AGENTS.md` в корень проекта. Если `AGENTS.md` уже существует, объедините инструкции, не удаляя текущие правила.

Подробный сценарий работы находится в [`SKILL.md`](skills/memory-upgrade/SKILL.md).

</details>

## Совместимость

Memory Upgrade построен на открытом формате [Agent Skills](https://agentskills.io/specification). Установка и автоматический вызов зависят от возможностей конкретной среды и её конфигурации.

- [OpenAI Codex](https://developers.openai.com/codex/)
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Cursor](https://docs.cursor.com/)
- [GitHub Copilot](https://docs.github.com/en/copilot)
- [OpenCode](https://opencode.ai/docs/skills/)

## Безопасность и ограничения

- Не записывайте в память пароли, токены, приватные ключи и другие секреты.
- Разделяйте подтверждённые факты и предположения.
- Сверяйте старые заметки с текущим состоянием проекта.
- Не отмечайте проверки выполненными, если они фактически не запускались.
- Перед публикацией репозитория проверьте `SESSION_MEMORY.md`: в нём может оказаться внутренняя информация.

> [!IMPORTANT]
> **Memory Upgrade не является фоновым сервисом.** Он не наблюдает за неактивными сессиями и не обновляет файлы самостоятельно. Память ведёт активный агент, следуя инструкциям навыка.

## Структура проекта

```text
memory-upgrade/
├── AGENTS.md
├── README.md
├── assets/
│   ├── memory-upgrade-banner.svg
│   └── memory-upgrade-hero.gif
└── skills/
    └── memory-upgrade/
        ├── AGENTS.md
        ├── SKILL.md
        └── templates/
            └── SESSION_MEMORY.md
```

## Участие в проекте

Идеи, сообщения об ошибках и улучшения приветствуются. Для изменений можно открыть [Issue](../../issues) или отправить Pull Request.

Чтобы быстрее разобраться с проблемой, укажите:
- агентную среду и её версию;
- способ установки;
- ожидаемое поведение;
- что произошло фактически.

## Контакты

<div align="center">

**Разработка и обратная связь**

[Telegram · @s1lentpacket](https://t.me/s1lentpacket) &nbsp;·&nbsp; [GitHub · Pre11yhacker](https://github.com/Pre11yhacker)

</div>
