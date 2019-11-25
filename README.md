![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# LiteSpeed参数说明
#### LiteSpeed Database Backup Parameters Explained
**发布-日期: 2014年4月14日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文

自从一次又一次收集LiteSpeed后，可用信息的数量看来有些分散，所以我将发布有关LiteSpeed参数的内容。
# LiteSpeed参数说明。
LiteSpeed提供了许多不同的备份选项，这些选项在LiteSpeed默认值中设置，但可以针对单个备份和还原作业进行更改。

## 解析度
下面讨论的一些选项是高级选项，最好在彻底了解更改的影响时再进行更改。

## 亲和力
在Windows中，这是一个指定正在运行的程序将使用的处理器数的数字。在重负载下运行时，使用此选项可提高多处理器计算机的性能。将该选项保留为0（默认值）可在大多数情况下提供最佳性能。这是一个高级选项，请不要在不
参考LiteSpeed帮助文件或SQL Server联机丛书，通过搜索“亲和力” 获得对该功能的完整说明的情况下来更改此设置。

## 备份线程
这是用于创建备份的同时进行的线程数。用于多处理器环境，备份作业分为多个不同的线程以创建备份文件。当作业负载分布在多个线程中时，大型数据库会往往会更快地备份。每个线程都创建一个单独的备份文件，LiteSpeed
将其作为一个备份文件进行交错。但是，如果使用LiteSpeed提供的Extractor Utility提取本机文件，则创建的文件数与线程的数量相同。这些文件需要作为一个集合一起恢复，使用SQL Server本机恢复命令作为条带备份。

## 加密级别
需要加密级别。 需要输入密码才能解密文件。 目前有9种级别的加密可用。 加密级别越高，执行备份/还原所需的时间越长。

## 压缩等级
备份需要压缩级别。 压缩级别越高，备份/还原文件所需的时间越长。 默认值为1，最大值为11。值为0时，绕过压缩例程，因此，Native和LiteSpeed备份文件大小没有区别。

## 优先
CPU Priority是一种调整后台和前台应用程序接收的CPU周期数的设置。默认值为“正常”。在备份过程运行时，更改此设置将占用更多CPU。有效选项包括：0正常（默认），1高于正常，2高。注意：此参数不可用于还原过程，仅
用于备份过程。

## 最大转移尺寸
这是一起发送到备份设备的数据块的大小。 如果在备份数据库时遇到性能下降，可以更改这些内容。 不应将其设置为大于4Mb（4194304字节）的值，因为这是限制，不应将其设置为低于64Kb（65536字节）。 默认值为1Mb（1048576字节）。

## 缓冲计数
Microsoft建议的计算缓冲区计数是使用下面的公式：
备份设备的数量*3 + 备份设备的数量 + 数据库文件数量 = 缓冲计数
在LiteSpeed中，缓冲区计数的最大值为150。缓冲区计数应设置为一个大于备份设备数的数字。LiteSpeed默认值为20。如果备份遇到性能问题，可以再次更改。你可以使用BufferCount参数更改内存块的数量，这些内存块的大小由
MaxTransferSize参数指定，并且由一个实例的预读功能（read ahead feature）提取。
风门
风门会将备份过程允许的最大CPU使用率设置为百分比。 默认值为100％。
还有许多其他参数可供使用，目前尚未记录，但你必须查找这些参数。 这些是最常见的。


## English
It seems since the acquisition of LiteSpeed again and again has somewhat fragmented the amount of available information, so I’ll post up what I have in my notes about the LiteSpeed Parameters.
# LiteSpeed Parameters explained.
LiteSpeed provides a number of different backup options which are set in the LiteSpeed Defaults but may be changed for individual backup and restore jobs.
## Resolution
Some of the options discussed below are advanced options and should only be changed if there is a thorough understanding of the affects the changes.

## Affinity
In Windows this is a number which specifies the number of processors that will be used by the running process. Use this to increase performance on multi-processor machines, when operating under heavy loads. Leaving this to 0 (default) provides the best performance in most cases. This is an advanced option, do not alter this setting without referring to the LiteSpeed Help File or SQL Server Books Online by searching for ‘affinity’ for a complete explanation of the function.

## Backup Threads
This is the number of simultaneous processes to use to create the backup. This is used on Multi-Processor environments where the backup job is split over a number of different processes to create the backup file. Large databases tend to be backed up faster when the job load is spread over a number of processes. Each process creates a separate backup file which LiteSpeed interleaves as one backup file. However, if the native files were extracted using the Extractor Utility provided by LiteSpeed, the number of files created is the same as the number set for Threads. These files will need to be restored together, as a set, using SQL Server native restore commands as a striped backup.

## Encryption Level
Level of Encryption required. A password will need to be entered to allow the file to be decrypted. There are currently 9 levels of encryption available. The greater the encryption level, the longer it will take to perform the backup/restore.

## Compression Level
The level of compression required for the backup. The greater the level of compression the longer it will take to backup/restore a file. The default value is 1 and the max value is 11. A value of 0, bypasses the compression routines; therefore, there is no difference between the Native and LiteSpeed backup file sizes.

## Priority
CPU Priority is a setting that adjusts the amount of CPU cycles that the background and foreground applications receive. The default is Normal. Changing this Setting will take up more CPU usage while the backup process is running. Valid options are: 0 Normal (Default), 1 AboveNormal , 2 High Note: This parameter is not available for the restore process, only backup

## Max Transfer Size
This is the size of the chunks of data that are sent togethyer over to the backup device. These can be changed if slow performance is being experiencing when backing up databases. This should not be set to a value more than 4Mb (4194304 bytes) as this is the limit and it should not be set below 64Kb (65536 bytes). The default is 1Mb (1048576 bytes).

## Buffer Count
Microsoft recommendations for working out the buffer count is to use the formula below:
NumberofBackupDevices*3 + NumberofBackupDevices + NumberofDatabaseFiles = BufferCount
In LiteSpeed, the maximum value for the buffer count is 150. The buffer count should be set to a number that is greater than the number of backup devices. The LiteSpeed default is 20. Again this can be changed if performance issues are being experienced with the backup. You can use the BufferCount parameter to change the number of memory blocks that are the size as specified by the MaxTransferSize parameter and that are fetched by the read ahead feature at one instance.

## Throttle
This sets the maximum CPU usage allowed for the backup process as a percentage. The default is 100%.
There are also a number of other parameters that can be used, which currently are not documented, but you’ll have to look for those. These are the most common.


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

