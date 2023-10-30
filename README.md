# Домашнее задание к занятию 11 «Teamcity»

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.
4. Авторизуйте агент.
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).

![create_vm1](/screenshots/1.png)  
![create_vm2](/screenshots/2.png)  
![create_fork](/screenshots/3.png)  
![add_agent1](/screenshots/4.png)  
![add_agent2](/screenshots/5.png)  

## Основная часть

1. Создайте новый проект в teamcity на основе fork.
![create_new_project1](/screenshots/6.png)  

2. Сделайте autodetect конфигурации.
![autodetect1](/screenshots/7.png)  

3. Сохраните необходимые шаги, запустите первую сборку master.
![build1](/screenshots/8.png)  

4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.
![build2](/screenshots/9.png)  

5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.
6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
![build3](/screenshots/10.png)  
![build4](/screenshots/11.png)  

7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.
![build5](/screenshots/12.png)  
![build6](/screenshots/13.png)  

8. Мигрируйте `build configuration` в репозиторий.
![build7](/screenshots/14.png)  

9. Создайте отдельную ветку `feature/add_reply` в репозитории.
![build8](/screenshots/15.png)  

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.  
![hunter1](https://github.com/aleks-sh-devops/example-teamcity/blob/master/src/main/java/plaindoll/Welcomer.java)  

11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.  
![hunter2](https://github.com/aleks-sh-devops/example-teamcity/blob/master/src/test/java/plaindoll/WelcomerTest.java)  

12. Сделайте push всех изменений в новую ветку репозитория.  
13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.  
![build9](/screenshots/16.png)  

14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.
![build10](/screenshots/17.png)  

15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.
18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
19. В ответе пришлите ссылку на репозиторий.
