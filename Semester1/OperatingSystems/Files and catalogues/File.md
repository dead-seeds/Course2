Файл в Unix — это либо именованная совокупность данных в файловой системе, либо интерфейс для доступа к физическому или виртуальному устройству, либо интерфейс для доступа к некоторым средствам межпроцессного (трубы) и сетевого (сокеты) взаимодействия. (at [[CRITS (23-24)]] there is a better definition (by Irtegov))


New file has no allocated memory for data. [[OS]] give file disk space while writing new data.

Another, more concise definition
> File is object that can be read and written to

Files are not necessarily stored on disk - they can be just interfaces to network, another process, output device, etc.

New file has no allocated memory for data. OS give file disk space while writing new data. But only if it is a regular file on disk.

File size stores in data structure [[inode]]. Actually, there is no `EOF` symbol in the end of file.


## Sparse files
In a file there can be "holes" - places where no write operation was performed. No memory is allocated for that "hole". There are a number of applications for those files:
- Hash maps. Those are usually sparse, so it is handy to store them like in memory.
- Torrent files. Torrents are downloaded in parts, so it can be useful to write those parts where they belong right away, instead of rearranging them afterwards.
