# Рефакторинг

После проведения рефакторинга были выявлены следующие проблемы в коде:
1. Небезопасные поля в классах
2. Нечитаемость кода
3. Неиспользуемый код


### 1)
В классе chatViewController было обнаружено 2 public-поля "chatId" и "chatName" (14,15 cтрока), значения данных полей изменялись напрямую
в классах FriendListController  и MessagesController.
(Commit: https://github.com/ggnsta/SWIFT-VK/commit/c9563bb6aeaf0c2e9abb21c6120d978c77c8b90f),

Решение: Инкапсулируем данные поля. Сделаем данные поля приватными и создадим для них set-методы.

### 2)
В классе MessagesController  метод(101-111 строка) func tableView(_ tableView: UITableView, editActionsForRowAt indexPath: IndexPath) 
является трудным 
для чтения, а так же выполняет несколько операций (отображение кнопки "delete", отображение диалоговых окон 
и непосредственно само удаление диалога)(Commit: https://github.com/ggnsta/SWIFT-VK/commit/f592ad46dd75f1e4defa3f327982044e18c918e8)

Решение: произведем извлечение метода. Создадим новый метод showDeleteDialogAlert, который возьмет на себя часть функционала
и который будет вызываться в исходном методе.

### 3)
В классе FriendListController точно такая же ситуация как и в пунктие 2, этот метод выполняет два действия: удаляет пользователя и 
отркывает диалог с ним. (Commit:https://github.com/ggnsta/SWIFT-VK/commit/8d5eb32d99ba2fcfa361321428f808c26790d477).

Решение: произведем извлечение метода. Создадим 2 новых метода showDeleteFriendAlert и showSendMessageAlert.

### 4)
Неиспользуемая сторонняя библиотека alamofire

Решение: удалить.


### 5)
В проекте присутствует 2 неиспользуемых класса 

Messages MessageInfo, на которых опробовалась работа с vk_ios_sdk  (commit: https://github.com/ggnsta/SWIFT-VK/commit/dd6f459e1e63e71face66a01e9c7c8b840886ac8)

Решение: удалить.
