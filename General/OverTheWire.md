> [!info] OverTheWire: Bandit  
> The Bandit wargame is aimed at absolute beginners.  
> [https://overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)  

```Shell
ssh bandit0@bandit.labs.overthewire.org -p 2220 bandit0 | cat readme
ssh bandit1@bandit.labs.overthewire.org -p 2220 NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL  | cat < -
ssh bandit2@bandit.labs.overthewire.org -p 2220 rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi  | cat 'spaces in this filename'ssh bandit3@bandit.labs.overthewire.org -p 2220 aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG  | cat inhere/.hidden
ssh bandit4@bandit.labs.overthewire.org -p 2220 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe  | file ./*ssh bandit5@bandit.labs.overthewire.org -p 2220 lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR  | find ./ -readable ! -executable -size 1033c
ssh bandit6@bandit.labs.overthewire.org -p 2220 P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU  | find / -user bandit7 -group bandit6 -size 33c 2>/dev/null OR find / -user bandit7 -group bandit6 -size 33c | grep bandit7
ssh bandit7@bandit.labs.overthewire.org -p 2220 z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S  | cat data.txt | grep millionth
ssh bandit8@bandit.labs.overthewire.org -p 2220 TESKZC0XvTetK0S9xNwm25STk5iWrBvP  | cat data.txt | sort | uniq -u OR sort data.txt | uniq -ussh bandit9@bandit.labs.overthewire.org -p 2220 EN632PlfYiZbn3PhVK3XOGSlNInNE00t  | strings data.txt | grep -E "="ssh bandit10@bandit.labs.overthewire.org -p 2220 G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s | base64 -d data.txt
ssh bandit11@bandit.labs.overthewire.org -p 2220 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM | tr 'a-zA-Z' 'n-za-mN-ZA-M' < data.txt # hint Read [ROT13 - Wikipedia](https://en.wikipedia.org/wiki/ROT13)ssh bandit12@bandit.labs.overthewire.org -p 2220 JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv | cat data.txt | xxd -r > data | file data | mv data data2.gz | gzip -d data2.gz | mv data2 data3.bz | bzip2 -d data3.bz | mv data3 data4.gz | gzip -d data4.gz | mv data4 data5.tar | tar -xf data5.tar | mv data5.bin data6.tar | tar -xf data6.tar | mv data6.bin data7.bz | bzip2 -d data7.bz | mv data7 data8.tar | tar -xf data8.tar | mv data8.bin data9.gz | gzip -d data9.gz | cat data9
ssh bandit13@bandit.labs.overthewire.org -p 2220 wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw |
```