# ЭХО РУИН (Echo of Ruins)

Учебный проект производственной (технологической (проектно-технологической)) практики.
Жанр: 2D-платформер-роглайт с элементами метроидвании. Движок: Unity 2022.3 LTS (2D URP).

## Как запустить
1. Склонируйте репозиторий: `git clone <ссылка>`
2. Откройте проект в Unity 2022.3 LTS (или новее).
3. Откройте сцену `Assets/Scenes/Biome01_Coast.unity` и нажмите Play.

## Управление
| Действие | Клавиша |
|---|---|
| Движение | A/D или стрелки |
| Прыжок | Space |
| Рывок | Left Shift |
| Эхо-импульс (сонар) | Q |

## Состав скриптов
- `PlayerController.cs` — движение, прыжок (coyote time, jump buffer), рывок с кадрами неуязвимости.
- `EchoPulse.cs` — сонар-импульс, подсвечивающий интерактивные объекты (тег `Interactable`).
- `HealthSystem.cs` — единая система здоровья игрока и врагов (интерфейс `IDamageable`).
- `EnemyAI.cs` — ИИ врага: конечный автомат Патруль → Преследование → Атака.
- `DifficultyManager.cs` — адаптивная балансировка сложности («резинка»: рост за прогресс, сброс за смерти).
- `LevelManager.cs` — чекпоинты, возрождение, переходы между биомами.

## Настройка сцены (минимум)
1. Игрок: спрайт + Rigidbody2D (Gravity Scale 3–4, Freeze Rotation Z) + Collider2D + скрипты PlayerController, EchoPulse, HealthSystem. Тег `Player`.
2. Земля: GameObject с Collider2D на слое `Ground` (LayerMask назначить в PlayerController.groundMask).
3. Враг: спрайт + Rigidbody2D + Collider2D + EnemyAI + HealthSystem; patrolPoints — два пустых объекта-маркера.
4. Чекпоинт: пустой объект + триггер-коллайдер, при входе вызывает `LevelManager.SetCheckpoint()`.
5. Интерактивные объекты (терминалы, скрытые проходы): тег `Interactable`, скрипт с методом `OnEchoRevealed()`.

## Как опубликовать (ответ на кейс-задачи 3–5)
1. Создайте публичный репозиторий на GitHub (например, `echo-of-ruins-practice`).
2. Загрузите: этот README, папку Scripts, скриншоты сцены, экспортированный unitypackage.
3. Ссылку на репозиторий укажите в отчёте по практике как ответ на кейс-задачи 3–5.
4. Бонус: сборку для Windows (`File → Build Settings → Windows`) можно выложить в Releases репозитория.
