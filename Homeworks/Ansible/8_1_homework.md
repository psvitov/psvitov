# Домашнее задание к занятию "08.01 Введение в Ansible"

## Подготовка к выполнению
1. Установите ansible версии 2.10 или выше.
2. Создайте свой собственный публичный репозиторий на github с произвольным именем.
3. Скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

---
### Ответ
---

1. Установленный `Ansible`:

![8_1_1.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_1.png)

2. Публичный репозиторий с загруженным `playbook`:

![8_1_2.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_2.png)



## Основная часть
1. Попробуйте запустить playbook на окружении из `test.yml`, зафиксируйте какое значение имеет факт `some_fact` для указанного хоста при выполнении playbook'a.
2. Найдите файл с переменными (group_vars) в котором задаётся найденное в первом пункте значение и поменяйте его на 'all default fact'.
3. Воспользуйтесь подготовленным (используется `docker`) или создайте собственное окружение для проведения дальнейших испытаний.
4. Проведите запуск playbook на окружении из `prod.yml`. Зафиксируйте полученные значения `some_fact` для каждого из `managed host`.
5. Добавьте факты в `group_vars` каждой из групп хостов так, чтобы для `some_fact` получились следующие значения: для `deb` - 'deb default fact', для `el` - 'el default fact'.
6.  Повторите запуск playbook на окружении `prod.yml`. Убедитесь, что выдаются корректные значения для всех хостов.
7. При помощи `ansible-vault` зашифруйте факты в `group_vars/deb` и `group_vars/el` с паролем `netology`.
8. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь в работоспособности.
9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.
10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.
11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь что факты `some_fact` для каждого из хостов определены из верных `group_vars`.
12. Заполните `README.md` ответами на вопросы. Сделайте `git push` в ветку `master`. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым `playbook` и заполненным `README.md`.

---
### Ответ:
---

1. Запускаем `playbook` на окружении `test.yml`:

>   root@DevOps:~/Homeworks/hw81/playbook# ansible-playbook site.yml -i inventory/test.yml

Результат:

![8_1_3.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_3.png)

Значение `some_fact` для данного хоста: 12

2. Файл с переменными, в котором здается новое значение находится в директории `~/playbook/group_vars/all/`

Замена на `all default fact` дает результат:

![8_1_4.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_4.png)

3. Создано окружение из 2-х docker-контейнеров:

![8_1_5.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_5.png)

4. Запускаем `playbook` на окружении `prod.yml`:

>   root@DevOps:~/Homeworks/hw81/playbook# ansible-playbook site.yml -i inventory/prod.yml

Результат:

![8_1_6.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_6.png)

`some_fact` для `centos7` - el

`some_fact` для `ubuntu`  - deb

5. Внесение изменений в файлы групп хостов:

![8_1_7.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_7.png)

6. Повторяем запуск `playbook` на окружении `prod.yml`:

![8_1_8.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_8.png)

7. Шифруем факты в `group_vars/deb` и `group_vars/el` с паролем `netology` и проводим проверку шифрования:

![8_1_9.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_9.png)

8. Повторяем запуск `playbook` на окружении `prod.yml`:

![8_1_10.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_10.png)

9. Так как все плагины в Ansible выполняются в контексте локального хоста, то подойдет плагин `local`

10. Внесение изменений в файл `prod.yml':

![8_1_11.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_11.png)

11. Повторяем запуск `playbook` на окружении `prod.yml`:

![8_1_12.png](https://github.com/psvitov/devops-netology/blob/main/Homework/mnt_homework_8_1/8_1_12.png)

12. Ссылка за измененый [`playbook`](https://github.com/psvitov/mnt_homework_8_1)
