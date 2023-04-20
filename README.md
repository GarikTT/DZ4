Домашнее задание.

Цели задания:
1. Определить алгоритм с наилучшим сжатием
2. Определить какие алгоритмы сжатия поддерживает zfs (gzip, zle, lzjb, lz4);
3. Создать 4 файловых системы на каждой применить свой алгоритм сжатия;

4. Для сжатия использовать либо текстовый файл, либо группу файлов:
Определить настройки пула
5. С помощью команды zfs import собрать pool ZFS;
6. Командами zfs определить настройки:
    - размер хранилища;
    - тип pool;
    - значение recordsize;
    - какое сжатие используется;
    - какая контрольная сумма используется.
7. Работа со снапшотами
	скопировать файл из удаленной директории.   https://drive.google.com/file/d/1gH8gCL9y7Nd5Ti3IRmplZPF1XjzxeRAG/view?usp=sharing 
	восстановить файл локально. zfs receive
	найти зашифрованное сообщение в файле secret_message

8. Выполнение:
	1. script --timing=time_homework_log homework.log
	1. vagrant up
	2. vagrant ssh
	3. sudo -i
	4. lsblk
	5. Создаём пул из двух дисков в режиме RAID 1:
		[root@zfs ~]# zpool create otus1 mirror /dev/sdb /dev/sdc
	6. Создадим ещё 3 пула: 
		[root@zfs ~]# zpool create otus2 mirror /dev/sdd /dev/sde
		[root@zfs ~]# zpool create otus3 mirror /dev/sdf /dev/sdg
		[root@zfs ~]# zpool create otus4 mirror /dev/sdh /dev/sdi
	7. zpool list
	8. zfs set compression=lzjb otus1
	9. zfs set compression=lz4 otus2
	10. zfs set compression=gzip-9 otus3
	11. zfs set compression=zle otus4
	12. for i in {1..4}; do wget -P /otus$i https://gutenberg.org/cache/epub/2600/pg2600.converter.log; done
	13. ls -l /otus*
	14. zfs list
	15. wget -O archive.tar.gz --no-check-certificate 'https://drive.google.com/u/0/uc?id=1KRBNW33QWqbvbVHa3hLJivOAt60yukkg&export=download'
	16. tar -xzvf archive.tar.gz
	17. zpool import -d zpoolexport/
	18. zpool import -d zpoolexport/ otus
	19. zpool status
#	20. zpool import -d zpoolexport/ otus newotus   ?????????!!!!!!!!! zpool import -d zpoolexport/ newotus // Надо создать пул newotus!!!
	21. zpool get all otus
	22. zfs get available otus
	23. zfs get readonly otus
	24. zfs get recordsize otus
	25. zfs get compression otus
	26. wget -O otus_task2.file --no-check-certificate "https://drive.google.com/u/0/uc?id=1gH8gCL9y7Nd5Ti3IRmplZPF1XjzxeRAG&export=download"
	27. zfs receive otus/test@today < otus_task2.file
	28. find /otus/test -name "secret_message" /otus/test/task1/file_mess/secret_message
	29. cat /otus/test/task1/file_mess/secret_message
	30. Про Украину прикольно.
	31. scriptreplay --timing=time_homework_log homework.log -d 20
