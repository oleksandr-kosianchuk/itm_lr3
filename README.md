# Мета роботи

За допомогою Terraform максимально оптимізувати процес створення віртуальної машини у сабнетворк в новому проекті. Пояснити internal та external IP-адреси.

## Хід роботи

По-перше потрібно встановити terraform. Я зробив це за допомогою Chocolatey. Відркрив Windows PowerShell і виконав таку команду:

![](/images/itm_lr3_1.png)


Після того, як terraform було вставновленно, я перейшов у Google Cloud Platform та создав новий 
проект з назвою lr-3

![](/images/itm_lr3_2.png)


Для дальнішої роботи мені необхіден був Compute Engine API, активував його.

![](/images/itm_lr3_3.png)


Тепер, треба створити сервіс акаунт. Для цього перейшов до вкладки IAM & Admin->Service Accounts. 

![](/images/itm_lr3_4.png)


Натискаємо зверху сторінки кнопку CREATE SERVICE ACCOUNT, вводимо ім'я нового акаунта та тиснемо CREATE AND CONTINUE. 

![](/images/itm_lr3_5.png)
![](/images/itm_lr3_6.png)



Сформуємо ключ у форматі JSON, це треба для terraform щоб він міг авторизуватися локально з GCP.натиснемо на 3 крапки біля назви сервіс акаунта, далі Manage keys. На відкритій сторінці натискаємо ADD KEY та Create new key.

![](/images/itm_lr3_7.png)


При натисканні CREATE буде завантажено JSON файл. 

![](/images/itm_lr3_8.png)


Також, необхідно надати роль створеному сервіс акаунту. Для цього переходимо до "IAM & Admin/IAM" та зверху тиснемо на GRANT ACCESS. В New principals записуємо свій сервіс акаунт і обираємо роль "Basic/Editor".

![](/images/itm_lr3_9.png)


Тепер я локально створювати папку з проектом, назвав її "itm_lr3", в якій буду зберігатися дані terraform. 
Переніс туди наш JSON ключ та зробимо файл з назвою "main.tf", це буде стартова точка входу для 
terraform. Також, треба вказати клауд з яким працюємо у полі source

![](/images/itm_lr3_10.png)


Надалі вказуємо дані необхідні для роботи, тобто ключ, проект, з яким будемо працювати, регіон та зону. Їх буде записано в окремому файлі "variables.tf"
У цьому є файлі я створив нетворк.

![](/images/itm_lr3_11.png)


Тепер створимо сабнетворк.
Створив окремий файл у корні проекта, та записав наступні строки: 

![](/images/itm_lr3_20.png)

Тут ми вказуємо ім'я нашого сабнетворку, та налаштування нашої машини.Тут я вказав назву машини, тип,додав теги та назву образа - Debian 11. Під network_interface задаємо мережу та сабнетворк, створені раніше.

Створив файл "outputs.tf".Він буде зберігати вихідні дані.
![](/images/itm_lr3_21.png)

Тепер, спробуємо все запустити)
У Windows PowerShell перейдемо до папки з файлами написаного коду та використаємо команду.

```
terraform init
```

![](/images/itm_lr3_12.png)


Далі вводимо

```
terraform apply
```

Та пишемо "yes".

![](/images/itm_lr3_13.png)


При правильному налаштуванні усе повинно спрацювати і виглядати так:

![](/images/itm_lr3_16.png)


У консолі, ми бачимо, що нетворки й сабнетворки створилися.
Перейдемо у GCP та подивимося

![](/images/itm_lr3_17.png)


Дійсно, все працює, сервер активен.
Тепер, зруйнуємо цей інстанс. При запиті підтвердження пишемо "yes".

![](/images/itm_lr3_18.png)


Впевнимося, що знищення пройшло успішно за допомогою перевірки на GCP.
![](/images/itm_lr3_19.png)

Все пройшло успішно, робота виконана.


## Висновки

Я навчився працювати з таким інстрментом, як Terraform який дозволяє керувати та автоматизувати ресурси клауд сервісів за допомогою API, наприклад створення мереж або віртуальних машин.
