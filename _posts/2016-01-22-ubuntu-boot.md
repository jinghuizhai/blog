---
layout: default
title: '配置ubuntu的开机启动项'
---
#配置ubuntu的开机启动项
<p>在重装系统之后，开机启动界面的ubuntu引导不见了，直接进入新安装的window系统中。下面是如何恢复ubuntu引导的方法：</p>
<ol>
	<li>准备一张ubuntu系统安装盘；</li>
	<li>将ubuntu系统安装盘放入光驱，重新启动计算机，进入BIOS，将开机启动设置为光驱(CD/ROM)启动方式；</li>
	<li>
		<p>然后保存设置退出，等待片刻就进入到ubuntu的安装界面，此时有两个选择</p>
		<ol>
			<li>
				在该光盘上试用ubuntu系统
			</li>
			<li>
				将ubuntu系统安装到计算机上
			</li>
		</ol>
	</li>
	<li>
		选择"在该光盘上试用ubuntu系统"，进入到ubuntu系统之后，打开终端(快捷键组合是Ctrl+Alt+T)；在终端下输入sudo -i(获得管理员权限)
	</li>
	<li>
		在终端下输入fdisk -l(是小写的字母'L'，查看盘符列表)会出现类似下面的信息:
		<pre><code>
			Disk /dev/sda: 320.1 GB, 320072933376 bytes 　　　　255 heads, 63 sectors/track, 38913 cylinders 　　　　Units = cylinders of 16065 * 512 = 8225280 bytes 　　　　Disk identifier: 0x70f7ab9c
　　　　Device Boot Start End Blocks Id System 　　　　/dev/sda1 1 1627 13060096 27 Unknown 　　　　Partition 1 does not end on cylinder boundary. 　　　　/dev/sda2 * 1627 1639102400 7 HPFS/NTFS 　　　　Partition 2 does not end on cylinder boundary. 　　　　/dev/sda3 1639 8166 52429859 7 HPFS/NTFS 　　　　/dev/sda4 8167 38913 246975277+ 5 Extended 　　　　/dev/sda5 8167 32385 194539082+ 7 HPFS/NTFS 　　　　/dev/sda6 32386 38788 51432066 83 Linux 　　　　/dev/sda7 38789 38913 1004031 82 Linux swap / Solaris
		</code></pre>

	</li>
	<li>
		然后找到ID为83的盘符，根据上面显示的信息可知当时装ubuntu时是装在sda6这个分区。在终端输入mount /dev/sda* /mnt
(*代表ubuntu系统所在的分区，即上一步显示结果中ID为83的分区号，如上面显示的是在sda6这个分区， 
所以输入的是mount /dev/sda6 /mnt
注意:mount后面有一个空格，sda6后面也有一个空格，这两个空格千万不要漏掉，否则会报错)
	</li>
	<li>
	上一步结束之后，继续在终端中输入grub-install --root-directory=/mnt /dev/sda
等待一会儿，若出现Installationfinished,No Error Reported则表示成功了
(注意:grub-install之间没有空格，--root前面有一个空格，--root前面是两个'-'，/mnt后面有一个空格)
	</li>
	<li>
		到此，ubuntu引导基本恢复，重启电脑后，就可以看到熟悉的ubuntu引导界面了，进入ubuntu系统，打开终端输入
sudo update-grub
等待片刻显示以下信息：
<pre><code>
	Generating grub.cfg ... 　　　　Found linux image: /boot/vmlinuz-2.6.31-20-generic 　　　　Found initrd image: /boot/initrd.img-2.6.31-20-generic 　　　　Found memtest86+ image: /boot/memtest86+.bin 　　　　Found Windows Vista (loader) on /dev/sda1 　　　　Found Windows 7 (loader) on /dev/sda2 　　　　done
</code></pre>
恢复工作便全部完成了。
	</li>
</ol>
<hr/>
完。