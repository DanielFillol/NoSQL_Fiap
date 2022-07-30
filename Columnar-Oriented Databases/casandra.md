a) create account on [asta datastax](https://astra.datastax.com)

b) create a database (remember the keyspace name you chose)

c) on CQL Console ```use [keyspace]``` (select the "table" you will work on)

d) on CQL Console ```DESCRIBE KEYSPACES;``` show the database keyspaces


```
CREATE TABLE songs (
	id uuid PRIMARY KEY,
	title text,
	artist text,
	data blob);
```

``` 
CREATE TABLE playlists (
	id uuid,
	song_order int,
	song_id uuid,
	title text,
	album text,
	artist text,
	PRIMARY KEY (id, song_order)
);
```

``` 
INSERT INTO playlists (id, song_order, song_id, title, artist, album) VALUES (
	62c36092-82a1-3a00-93d1-46196ee77204,4,
	7db1a490-5878-11e2-bcfc-0800200c9a66,
	'Ojo Rojo', 'Fu Manchu', 'No One Rides for Free');
```

``` 
select * from playlists;
```

``` 
INSERT INTO playlists (id, song_order, song_id, title, artist, album) VALUES (
	now(),4,
	7db1a490-5878-11e2-bcfc-0800200c9a66,
	'Ojo Rojo', 'Fu Manchu', 'No One Rides for Free');
```

``` 
select album, title from playlists where artist = 'Fu Manchu';
```
It will return a error.

```
select album, title from playlists where artist = 'Fu Manchu' ALLOW FILTERING;
```
usar com moderação

```
CREATE INDEX ON playlists ( artist ); evitar criar indices
```

```
select album, title from playlists where artist = 'Fu Manchu';
``` 
now it works

```
CREATE TABLE users (user_id text PRIMARY KEY, first_name text, last_name text, emails set<text>);
```

```
INSERT INTO users (user_id, first_name, last_name, emails) VALUES ('frodo', 'Frodo','Baggins',{'f@baggins.com', 'baggins@gmail.com'});
```

```
select * from users
```

```
UPDATE users SET emails = emails + {'f@fellowship.com'} WHERE user_id = 'frodo';
```

```
ALTER TABLE playlists ADD tags set<text>;
```

 ```
 UPDATE playlists SET tags = tags + {'2007'} WHERE id = 62c36092-82a1-3a00-93d1-46196ee77204 AND song_order = 2;
 UPDATE playlists SET tags = tags + {'covers'} WHERE id = 62c36092-82a1-3a00-93d1-46196ee77204 AND song_order = 2;
 UPDATE playlists SET tags = tags + {'1973'} WHERE id = 62c36092-82a1-3a00-93d1-46196ee77204 AND song_order = 1;
 UPDATE playlists SET tags = tags + {'blues'} WHERE id = 62c36092-82a1-3a00-93d1-46196ee77204 AND song_order = 1;
 UPDATE playlists SET tags = tags + {'rock'} WHERE id = 62c36092-82a1-3a00-93d1-46196ee77204 AND song_order = 4;
 ```

```
create table if not exists transacoes (
    num_conta text,
    ano int,
    data_transacao timestamp,
    id_transacao text,
    localizacao text,
    descricao text,
    valor_transacao double,
    tags set<text>,
    PRIMARY KEY ((num_conta, ano), data_transacao)
    )  WITH CLUSTERING ORDER BY (data_transacao desc);
```

```
INSERT INTO transacoes (num_conta, ano, data_transacao, id_transacao, localizacao, descricao, valor_transacao, tags) VALUES ('1234123412341234', 2020, '2020-01-26 15:30:14', '1231514114', 'Sao Paulo/SP', 'Restaurante xxx', 50.00,{'Alimentação', 'Restaurante'});
```

```
INSERT INTO transacoes (num_conta, ano, data_transacao, id_transacao, localizacao, descricao, valor_transacao, tags) VALUES ('1234123412341234', 2020, '2020-01-27 15:30:14', '1231514123', 'Sao Paulo/SP', 'Iphone Store', 3000.00, {'Eletrônico', 'Restaurante'});
```

```
select * from transacoes;
```
