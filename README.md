# Для чего этот скрипт
Этот скрипт предназначен для выделения строки с ФИО сотрудника в таблице Confluence. Скрипт проверяет ФИО, указанное в личном кабинете пользователя (в верхнем правом углу), и если оно совпадает с ФИО в таблице, выделяет соответствующую строку. Для этого нужно вставить скрипт в макрос HTML на странице Confluence.

До:<br>
![image](https://github.com/user-attachments/assets/be229ff7-6273-428b-a070-9b4a0aa75d3b)

После:<br>
![image](https://github.com/user-attachments/assets/bf584061-fc57-47ed-a02b-c5513e84a435)


## Шаги для использования:
1.	Перейдите на страницу Confluence, где находится таблица с данными сотрудников.<br>
2.	Откройте страницу для редактирования.<br>
3.	Добавьте макрос HTML на страницу:<br>
    1. Нажмите "Вставить прочий контент" > "Другие макросы" > "HTML".<br>
     ![image](https://github.com/user-attachments/assets/ccdf7533-8269-4653-995d-396a64db083d)
     ![image](https://github.com/user-attachments/assets/8829a091-cac8-4249-926d-70cbf3096e1d)
     ![image](https://github.com/user-attachments/assets/b8f6b4cb-2fd3-4467-a5fa-6232c7bf7e88)
     ![image](https://github.com/user-attachments/assets/332843ac-55b1-4fb4-8895-24f03c0b55c3)
    2. Вставьте код в поле макроса.<br>
4.	Сохраните изменения.<br>
5.	При загрузке страницы, скрипт автоматически выполнится, выделив строку с вашим ФИО, если оно присутствует в таблице.


## Код скрипта:
```
<script>
function highlightUserRow() {
    // Получаем ФИО из личного кабинета пользователя
    const fullName = document.querySelector('#user-menu-link').title;
    const [lastName, firstName] = fullName.split(' ');  // Разделяем ФИО на фамилию и имя
    const fullUserName = `${lastName} ${firstName}`;  // Составляем полное имя для сравнения

    // Получаем все ячейки таблицы с возможными совпадениями
    const tableCells = document.querySelectorAll('.confluenceTh.tf-floating, td');

    // Проходим по всем ячейкам и ищем совпадение с ФИО
    tableCells.forEach(cell => {
        if (cell.textContent.trim() === fullUserName) {
            // Подсвечиваем строку, если имя совпадает
            const row = cell.closest('tr');
            if (row) {
                row.style.fontWeight = 'bold';
                row.style.fontSize = '16px';
                row.style.backgroundColor = '#f0f0f0';
                row.style.borderBottom = '3px solid black';
            }
        }
    });
}

// Запускаем функцию после загрузки страницы с небольшой задержкой
window.addEventListener('load', () => {
    setTimeout(highlightUserRow, 500);
});
</script>
```
