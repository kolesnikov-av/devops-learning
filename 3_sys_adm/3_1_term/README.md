Задание

1. С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:

Создайте директорию, в которой будут храниться конфигурационные файлы Vagrant. В ней выполните vagrant init. Замените содержимое Vagrantfile по умолчанию следующим:

 Vagrant.configure("2") do |config|
 	config.vm.box = "bento/ubuntu-20.04"
 end
Выполнение в этой директории vagrant up установит провайдер VirtualBox для Vagrant, скачает необходимый образ и запустит виртуальную машину.

vagrant suspend выключит виртуальную машину с сохранением ее состояния (т.е., при следующем vagrant up будут запущены все процессы внутри, которые работали на момент вызова suspend), vagrant halt выключит виртуальную машину штатным образом.

2. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?

        CPU: 2
        RAM: 1Gb
        HHD: 64Gb

3. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?

         Vagrant.configure("2") do |config|
                config.vm.box = "bento/ubuntu-20.04"

                config.vm.provider "virtualbox" do |v|
                        v.memory = 2048
                        v.cpus = 4
                end
        end

4. Команда vagrant ssh из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.
   
        alex@MBP-MakBuk vagrant_conf % vagrant ssh
        Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-110-generic x86_64)

        * Documentation:  https://help.ubuntu.com
        * Management:     https://landscape.canonical.com
        * Support:        https://ubuntu.com/advantage

        System information as of Thu 24 Nov 2022 06:39:49 PM UTC

        System load:  0.0                Processes:             139
        Usage of /:   11.9% of 30.63GB   Users logged in:       0
        Memory usage: 10%                IPv4 address for eth0: 10.0.2.15
        Swap usage:   0%


        This system is built by the Bento project by Chef Software
        More information can be found at https://github.com/chef/bento
        Last login: Wed Nov 23 19:20:10 2022 from 10.0.2.2
        vagrant@vagrant:~$ whoami
        vagrant

5. Ознакомьтесь с разделами man bash, почитайте о настройках самого bash:

какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?
что делает директива ignoreboth в bash?

        $HISTSIZE
        629 строка
        A value of ignoreboth is shorthand for ignorespace and ignoredups.


6. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
   
   A sequence expression takes the form {x..y} - для генерации последовательностей
   805 строка

7. С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?

        touch test{000000..100000}.txt
        ошибка: Argument list too long, скорее всего связана с какими-то установленными ограничениями

8. В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]

        Приверяет, существует ли папка /tmp

9.  Сделайте так, чтобы в выводе команды type -a bash первым стояла запись с нестандартным путем, например bash is ... Используйте знания о просмотре существующих и создании новых переменных окружения, обратите внимание на переменную окружения PATH

bash is /tmp/new_path_directory/bash
bash is /usr/local/bin/bash
bash is /bin/bash
(прочие строки могут отличаться содержимым и порядком) В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.

        mkdir -p /tmp/new_path_directory/bash
        cp /bin/bash /tmp/new_path_directory/bash
        export PATH=/tmp/new_path_directory/bash:$PATH
        type -a bash

        vagrant@vagrant:~$ type -a bash
        bash is /tmp/new_path_directory/bash/bash
        bash is /usr/bin/bash
        bash is /bin/bash

10. Чем отличается планирование команд с помощью batch и at?
    
        batch запускается при низкой нагрузке

1.  Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.
    
        vagrant halt


