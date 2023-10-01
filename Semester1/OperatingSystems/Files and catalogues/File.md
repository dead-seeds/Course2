Файл в Unix — это либо именованная совокупность данных в файловой системе, либо интерфейс для доступа к физическому или виртуальному устройству, либо интерфейс для доступа к некоторым средствам межпроцессного (трубы) и сетевого (сокеты) взаимодействия.

<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD:Semester1/OperatingSystems/Files and catalogues/File.md
New file has no allocated memory for data. [[OS]] give file disk space while writing new data.
=======
=======

=======
<<<<<<< HEAD:Semester1/OperatingSystems/Files and catalogues/File.md
>>>>>>> d14664a (Clafifications from previous lecture)
New file has no allocated memory for data. [[OS]] give file disk space while writing new data.
=======
Another, more concise definition
> File is object that can be read and written to
>>>>>>> 52db4bb (Clafifications from previous lecture):Semester1/OperatingSystems/Files/File.md

<<<<<<< HEAD
>>>>>>> c0ee077 (Clafifications from previous lecture)
Another, more concise definition
> File is object that can be read and written to
>>>>>>> 52db4bb (Clafifications from previous lecture):Semester1/OperatingSystems/Files/File.md
=======
Another, more concise definition
> File is object that can be read and written to
>>>>>>> fc2c424 (Directories permissions + notes from two lectures (#6))
=======
Another, more concise definition
> File is object that can be read and written to
>>>>>>> fc2c424 (Directories permissions + notes from two lectures (#6))

=======
>>>>>>> d14664a (Clafifications from previous lecture)
Files are not necessarily stored on disk - they can be just interfaces to network, another process, output device, etc.

New file has no allocated memory for data. OS give file disk space while writing new data. But only if it is a regular file on disk.

File size stores in data structure [[inode]]. Actually, there is no `EOF` symbol in the end of file.

<<<<<<< HEAD
Text and binary files are the same to [[Kernel]]. The difference start on the level of user programs like [[vim]], [[nano]], etc
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
=======
>>>>>>> be7dfd4 (Start of dynamic memory management, good + bad source to find information, file clarifications)
=======
<<<<<<< HEAD
>>>>>>> c0ee077 (Clafifications from previous lecture)

## Sparse files
In a file there can be "holes" - places where no write operation was performed. No memory is allocated for that "hole". There are a number of applications for those files:
- Hash maps. Those are usually sparse, so it is handy to store them like in memory.
<<<<<<< HEAD
- Torrent files. Torrents are downloaded in parts, so it can be useful to write those parts where they belong right away, instead of rearranging them afterwards.
=======
<<<<<<< HEAD
>>>>>>> fc2c424 (Directories permissions + notes from two lectures (#6))
=======
- Torrent files. Torrents are downloaded in parts, so it can be useful to write those parts where they belong right away, instead of rearranging them afterwards.
>>>>>>> be7dfd4 (Start of dynamic memory management, good + bad source to find information, file clarifications)
=======
>>>>>>> fc2c424 (Directories permissions + notes from two lectures (#6))
=======
Text and binary files are the same to [[Kernel]]. The difference start on the level of user programs like [[vim]], [[nano]], etc
>>>>>>> d14664a (Clafifications from previous lecture)
>>>>>>> c0ee077 (Clafifications from previous lecture)
