Файл в Unix — это либо именованная совокупность данных в файловой системе, либо интерфейс для доступа к физическому или виртуальному устройству, либо интерфейс для доступа к некоторым средствам межпроцессного (трубы) и сетевого (сокеты) взаимодействия.

New file has no allocated memory for data. [[OS]] give file disk space while writing new data.

Another, more concise definition
> File is object that can be read and written to

Files are not necessarily stored on disk - they can be just interfaces to network, another process, output device, etc.

New file has no allocated memory for data. OS give file disk space while writing new data. But only if it is a regular file on disk.

File size stores in data structure [[inode]]. Actually, there is no `EOF` symbol in the end of file.

Text and binary files are the same to [[Kernel]]. The difference start on the level of user programs like [[vim]], [[nano]], etc
