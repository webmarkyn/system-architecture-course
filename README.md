Для низкого TTM был выбран монолит в качестве основы + микросервис для заявок от котов-работников, чтобы в случае ддоса или других ошибок лег только он.
Сервис заявок держит только сами заявки и при одобреннии делает запрос к основному монолиту для создания сущности работника.

Админ панель - отдельное SPA, в основном запросы идут к монолиту, но для заявок котов-работников делаются запросы в микросервис заявок

## Монолит:

Был выбран монолит для ускорения разработки + простоты деплоя.
Client Module
Отвечает за все, связанное с клиентами
Service Module
Отвечает за все задачи, расходники, отчеты воркера по задаче
Worker Module
Отвечает за все, связанное с воркерами, кроме их заявок. То есть в модуле только уже одобренные воркеры
Payment Module
Отвечает за все платежи внутри системы, генерацию инвойсов, бухгалтерию
Notifications Module
Отвечает за все нотификации внутри приложения
Management Module
Отвечает за управление системой, настройку типов услуг, ставки, проверка качества выполнения задач

## Worker Application микросервис:

Был выбран для защиты от DDos атак а также масштабируемости. Независим от основного монолита.
Хранит только заявки котов-воркеров. В качестве теста для каждого нового кота воркера дается ссылка на Гугл Форму, результат которой записывается обратно в заявку воркера. Когда воркер одобряется, сервис отправляет информацию в очередь для монолита
