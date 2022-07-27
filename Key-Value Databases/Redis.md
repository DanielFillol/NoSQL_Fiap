Redis

```Ping ```
//test if everything is ok

```Set mykey labfiap```
//Creates a key with labfiap as value

```get mykey```
//Get the value of the key

```Set mykey  “LabFiap” ex 60```
//Creates a key with a value that expires in 60 seconds.

```Ttl mykey ```
//Show how long the key is still active

```Mset chave1 valor1 chave2 valor2 chave3 valor3 chave4 valor4```
//Creates multiple keys with multiple values

```Keys *```
//Shows all keys

```keys "chave*"```
//Search for keys with “chave” as identifier

```Mget chave1 chave2```
//Get keys 

```Hset Aula:4 NoSQL Redis```
//Creates a key “Aula:4” column NoSQL and the value is Redis

```Hmset user:001 username teste aluno FIAP disciplina NoSQL unidade Paulista```
//Creates key and many couples

```lPush nosql mongodb```
//Creates list

```Lrange nosql 0 -1```
//Brings up all list

```Sadd alunos:Paulucci	Joaquim Beto Ana```
//Conjunto and unique values, this defers from list

```Sadd amigos:Joaquim Joao Ana```
//add repete values

```Smembers amigos: Joaquim```
//Show only uniques

```Zadd notas 7 Joaquim 5 Beto 8 Ana 9 Joao```
//Conjunto ordenado

```Zcount notas 1 7```
//How many values between 1 and 7

```Zrank notas Joaquim```
//Show position on conjunto ordenado

```Set msg “O Redis é rápido”```
//Creates a string

```Strlen msg```
//Len of mesege

```Getrange msg 0 10```
//Get range of string

