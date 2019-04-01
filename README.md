# Pendahuluan

Apa itu shell ? shell adalah program (penterjemah perintah) yang menjembatani user dengan sistem operasi dalam hal ini kernel (inti sistem operasi), umumnya shell menyediakan prompt sebagai user interface, tempat dimana user mengetikkan perintah-perintah yang diinginkan baik berupa perintah internal shell (internal command), ataupun perintah eksekusi suatu file progam (eksternal command), selain itu shell memungkinkan user menyusun sekumpulan perintah pada sebuah atau beberapa file untuk dieksekusi sebagai program.

# Kebutuhan Dasar

Sebelum mempelajari pemrograman Bash shell di linux sebaiknya anda telah mengetahui dan menggunakan perintah - perintah dasar shell baik itu internal command yang telah disediakan shell maupun eksternal command atau utility, seperti 
>cd, pwd, times, alias, umask, exit, logout, fg, bg, ls, mkdir, rmdir, mv, cp, rm, clear, ...

>utilitas seperti cat, cut, paste, chmod, lpr,...

>redirection (cara mengirim output ke file atau menerima input dari file), menggunakan operator redirect >, >>, <, <<, contohnya:
```
ls > data
hasil ls dikirim ke file data, jika file belum ada akan dibuat tetapi jika sudah ada isinya akan ditimpa.
ls >> data
hampir sama, bedanya jika file sudah ada maka isinya akan ditambah di akhir file.
cat < data
file data dijadikan input oleh perintah cat
```
>pipa (output suatu perintah menjadi input perintah lain), operatornya : | , contoh:
```
ls -l | sort -s
ouput perintah ls -l (long) menjadi input perintah sort -s (urutkan secara descending), mending pake ls -l -r saja :-)
ls -l | sort -s | more
cat <data | sort > databaru
```
>Wildcard dengan karakter *, ?, [ ], contohnya:
```
ls i*
tampilkan semua file yang dimulai dengan i
ls i?i
tampilkan file yang dimulai dengan i, kemudian sembarang karakter tunggal, dan diakhiri dengan i
ls [ab]*
tampilkan file yang dimulai dengan salah satu karakter a atau b
```

