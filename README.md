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

# Simple Bash Script
Buat file, ubah permision menjadi +x dan tulis script
```
touch testing.sh && chmod +x testing.sh && pico testing.sh

#!/bin/bash
echo "Hello, apa khabar"

./testing.sh
```

# Pemakaian Variabel
Secara sederhana variabel adalah pengenal (identifier) berupa satuan dasar penyimpanan yang isi atau nilainya sewaktu-waktu dapat berubah baik oleh eksekusi program (runtime program) ataupun proses lain yang dilakukan sistem operasi. dalam dokumentasi ini saya membagi variabel menjadi 3 kategori:
- Environment Variable
- Positional Parameter
- User Defined Variable

### Environment Variable
>Variabel yang digunakan khusus oleh shell atau sistem untuk proses kerja system seperti variabel `PS1, PS2, HOME, PATH, USER, SHELL,dsb...`

### Positional Parameter
>Variabel yang digunakan shell untuk menampung argumen yang diberikan terhadap shell baik berupa argumen waktu sebuah file dijalankan atau argumen yang dikirim ke subrutin. variabel yang dimaksud adalah `1,2,3,dst..`lebih jelasnya lihat contoh script berikut :
```
#!/bin/bash
#argumen.sh

clear
echo "Nama script anda : $0";
echo "Banyak argumen   : $#";
echo "Argumennya adalah: $*";
```
Hasilnya:
```
$ ./argumen.sh 1 2 3 empat
Nama script anda  : ./argumen.sh
Banyak argumen    : 4
Argumennya adalah : 1 2 3 empat
```

### User Defined Variable
>Variabel yang didefinisikan sendiri oleh pembuat script sesuai dengan kebutuhannya, beberapa hal yang perlu diperhatikan dalam mendefenisikan variabel adalah:

-   dimulai dengan huruf atau underscore
-   hindari pemakaian spesial karakter seperti *,$,#,dll...
-   bash bersifat case sensitive, maksudnya membedakan huruf besar dan kecil, `a` berbeda dengan `A`, `nama` berbeda dengan `Nama,NaMa,dsb..`

>Untuk mengeset nilai variabel gunakan operator assignment (pemberi nilai)`"="`, contohnya :

- myos="linux"	#double-quoted
- nama='pinguin'	#single-quoted 
- hasil=`ls -l`;	#back-quoted
- angka=12

>kalau anda perhatikan ada 3 tanda kutip yang kita gunakan untuk memberikan nilai string ke suatu variabel, adapun perbedaannya adalah:

-   dengan kutip ganda (double-quoted), bash mengizinkan kita untuk menyisipkan variabel di dalamnya. contohnya:
```
#!/bin/bash
nama="pinguin"
kata="Hi $nama, apa khabarmu"    #menyisipkan variabel nama
echo $kata;

Hasilnya:
Hi pinguin, apa khabarmu
```
-   dengan kutip tunggal (single-quoted), akan ditampilkan apa adanya. contohnya:
```
#!/bin/bash
nama="pinguin"
kata='Hi $nama, apa khabarmu'    #menyisipkan variabel nama
echo $kata;

Hasilnya:
Hi $nama, apa khabarmu
```
    
-   dengan kutip terbalik (double-quoted), bash menerjemahkan sebagai perintah yang akan dieksekusi, contohnya:
```
#!/bin/bash
hapus=`clear`;
isi=`ls -l`;        

#hapus layar
echo $hapus
#ls -l
echo $isi;
```

>untuk operasi matematika ada 3 cara yang dapat anda gunakan, dengan statement builtin `let` atau `expr` atau perintah `subtitusi` seperti contoh berikut:
```
#!/bin/bash
#mat1

a=10
b=5
#memakai let
let jumlah=$a+$b
let kurang=$a-$b
let kali=$a*$b

#memakai expr
bagi=`expr $a / $b`

#memakai perintah subtitusi $((ekspresi))
modul =$(($a%$b))  #sisa pembagian

echo "$a+$b=$jumlah"
echo "$a-$b=$kurang"
echo "$a*$b=$kali"
echo "$a/$b=$bagi"
echo "$a%$b=$mod"

Hasilnya:
10+5=15
10-5=5
10*5=50
10/5=2
10%5=0
```

fungsi `expr` begitu berdaya guna baik untuk operasi matematika ataupun string contohnya:
```
#!/bin/bash
#mat1

mystr="linux"
expr length $mystr

Hasilnya : 
5
```

>Bash menyediakan statement `declare` dengan opsi `-i` hanya untuk data integer (bilangan bulat). Contohnya:
```
#!/bin/bash

declare -i angka
angka=100;
echo $angka;
```
>apabila variabel yang dideklarasikan menggunakan `declare -i` ternyata anda beri nilai string (karakter), maka Bash akan mengubahnya ke nilai 0, tetapi jika anda tidak menggunakannya maka dianggap sebagai string.
