1. Модуль [copy][1] позволяет копировать данные с локальной или удаленной машины на удаленную машину.
2. Модуль [fetch][2] позволяет копировать файлы с удаленных машин.
3. Модуль [files][3] позвоялется устанавливать атрибуты файлов, директорий и ссылок. Так же с помощью него можно удалять файлы.
4. Модуль [shell][4] позволяет выполнять shell команды на удаленной машине, так же есть модуль [command][5], который тоже выполняет shell команды на удаленной машине, но переменные и операции **"<", ">", "|", ";"** и **"&"** не будут в нем работать.
5. Модуль [git][6] позволяет работать с гитом.
6. Модуль [get_url][7] позволяет качать файлы по HTTP, HTTPS или FTP.
7. Модуль [service][8] позволяет управлять процессами.

Все примеры, которые есть в документации написаны для плейбуков, но всеми этим модулями можно пользоваться так же и через командную строку.




[1]: https://docs.ansible.com/ansible/2.9/modules/copy_module.html#copy-module
[2]: https://docs.ansible.com/ansible/2.9/modules/fetch_module.html#parameter-flat
[3]: https://docs.ansible.com/ansible/2.9/modules/file_module.html#file-module
[4]: https://docs.ansible.com/ansible/2.9/modules/shell_module.html#shell-module
[5]: https://docs.ansible.com/ansible/2.9/modules/command_module.html#command-module
[6]: https://docs.ansible.com/ansible/2.9/modules/git_module.html#git-module
[7]: https://docs.ansible.com/ansible/2.9/modules/get_url_module.html#get-url-module
[8]: https://docs.ansible.com/ansible/2.9/modules/service_module.html#service-module