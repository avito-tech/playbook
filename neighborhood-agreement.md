# Соседское соглашение

- [Цель](https://github.com/avito-tech/playbook/blob/master/neighborhood-agreement.md#цель)
- [Краткое руководство](https://github.com/avito-tech/playbook/blob/master/neighborhood-agreement.md#краткое-руководство)
- [Правила внесения изменений в чужой функционал](https://github.com/avito-tech/playbook/blob/master/neighborhood-agreement.md#правила-внесения-изменений-в-чужой-функционал)
- [Ответственность владельца](https://github.com/avito-tech/playbook/blob/master/neighborhood-agreement.md#ответственность-владельца)
- [Меры контроля качества автоматизации тестирования](https://github.com/avito-tech/playbook/blob/master/neighborhood-agreement.md#меры-контроля-качества-автоматизации-тестирования)


## Цель
Снизить коммуникационные издержки и сократить баги от внесения изменений юнитами в функционал друг друга. Для этого нужно определить подход в автоматизации тестирования при изменении своего или чужого функционала и избежать негативных последствий для продуктов Avito.


## Краткое руководство


Правило  | Руководство к действию 
------------- | -------------
Правило бойскаута	| Оставь код репозитория лучше, чем он был до твоего прихода.
Куда хочешь, туда и пушь | Делать PR можно в любой репозиторий, если это не запрещено внутренними политиками безопасности или соответствиями внешним стандартам.
В чужой код со своим уставом не лезь | У команд есть Coding Standard и политика Code Review. Нужно использовать Coding Standard команды, которая владеет кодом. Если Code Standard в команде отсутствует — подсвети проблему оунеру.
Запушил в чужой код, не мержь без согласия владельца	| Следуем политике Code Review команды, которая владеет кодом.
Написал новый код, напиши и тесты	 | Тесты качественные и являются частью документации.
Написал новый код, а тесты не упали? Проверь и исправь тесты | Покрываем тестами так, что баг ломает тесты. Если логику поломали, а тесты «зеленые», значит их надо исправлять. Исправляет CODE OWNER, который владеет этим функционалом.
Кто сломал, тот и чинит | Кто сломал автотесты, уронил метрики или удалил логирование, тот их и исправляет.
Отклоняешь на ревью, аргументируй | Оунер репозитория не может отклонить пулл-реквест без четкого объяснения причин с аргументами.
Пришел тикет на ревью? Проведи его сегодня, не откладывай на завтра | Code Review должно проходить не позже, чем на следующий день.
Если сломали твой код, а ты не узнал – сам виноват	| Используешь соседнее API, напиши тест, который его проверяет и скажет, что это затронуло ваш юнит. Команда — оунер результата. Всегда мониторим зависимости, которые могут поломать сервис.
Владеешь кодом – отвечаешь за его тесты и метрики	| Оунишь репозиторий — покрой тестами, метриками и необходимым логированием.
***

## Правила внесения изменений в чужой функционал

Основное правило - «Keep Going Green». Нормальное состояние билдов и тестов, в том числе UI — зеленое, значит функционал работает и был проверен достаточно полно.
У нас есть принципы, согласно которым мы вносим изменения:
- Всегда нужно сначала получить одобрение от владельца функционала, а потом вносить изменения.
- Важно поддерживать работоспособность не только функционала, но и мониторинга, метрик и авто-тестов владельца.
- Все авто-тесты юнита поддерживаются в актуальном состоянии. Чтобы проверить их актуальность, нужно запустить автотесты с уже внесёнными изменениями. Это касается тех юнитов, функциональность которых была затронута изменениями.
- Утративший актуальность или необходимость тест должен быть удален по согласованию с владельцем.
- Тест, который стал падать из-за изменений и не по причине бага в функциональности, должен быть актуализирован в соответствии с этими изменениями.
- При расширении функционала покрытие не должно снижаться.
- Чьё изменение завалило тесты на staging, тот их и чинит.
- Юнит владелеца авто-теста информируется об изменении с помощью COP — Code Ownership Plugin.

## Ответственность владельца

- Низкое покрытие тестами кода приводит к скрытию дефектов и проявлению их в продакшене. В интересах владельца кода поддерживать уровень покрытия фукнционала кода тестами в районе 50%-80%.
- Если баг обнаружился через несколько релизов или несколько дней, то его исправляет владелец.
- Юнит должен понимать, что проверяет каждый автоматизированный тест, которым владеет — DB-tests, Unit-tests, API-tests, UI-tests.
- Если есть старые тесты и они были «зеленые», а какие-то новые правки их сломали и автор правок не может понять причину, то это не проблема владельца тестов. Автор правок обязан исправить тесты, сколько бы времени это не заняло, либо удалять их по согласованию с владельцем.
- Чтобы не тормозить общие релизные процессы, владелец обязан поддерживать работоспособность своего функционала на тестовых средах, которые используются для тестирования кросс-юнитного функционала, например, Staging.
- Ответственность за сохранение функционала, его содержание в рабочем состоянии и последствия от изменений лежит на том, кто последним его правил.

## Меры контроля качества автоматизации тестирования

- Команда QA кластера выполняет ревью тестов с произвольной периодичностью для поддержания общей культуры разработки авто-тестов и наращивания стабильности и полноты автоматизации тестирования.
- Соблюдаются общие требования к авто-тестам без привязки к реализации.
- Проводится ревью авто-тестов для поддержания общего порядка.
- Разрабатываются рекомендации по автоматизации тестирования — простые подходы и практики эффективной автоматизации тестирования.