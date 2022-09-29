# SQLite
Programas y documentación SQLite.
Programs de consultas genéricas y utilidades.

Exportar la estructura de toda la BD.
sqlite> .output c:/sqlite/chinook_structure.sql 
sqlite> .schema 
sqlite> .output stdout

Exporting Data
sqlite> .output file.sql
sqlite> .dump            // Podemos elegir solo alguna tabla .dump tabla
sqlite> .output stdout

Importing Data
Para importar datos usamos .read (si hemos usado .dump para exportar)
sqlite> drop table tabla;
sqlite> .read file.sql

Ejercicio Export/Import
D:\SQLite>sqlite3.exe D:\SQLite\chinook\chinook.db
sqlite> .output file.sql
sqlite> .dump
sqlite> .output stdout
sqlite> .exit
D:\SQLite>sqlite3.exe D:\SQLite\Pruebas
sqlite> .read file.sql

Segundo método.
Podemos crear un fichero con los campos separados por comas.
sqlite> .mode csv
sqlite> .output file.sql
sqlite> select * from genres;
sqlite> .output stdout

GenreId,Name
1,Rock
2,Jazz
3,Metal

CREATE TABLE IF NOT EXISTS "genres2"
(
    [GenreId] INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
    [Name] NVARCHAR(120)
);
sqlite> .import file.sql genres2

Nota: Antes de importar borrar la cabecera de las columnas. (GenreId,Name)
           Creo que el primer método es más fácil.
Evidentemente para crear una copia de la BD podemos simplemente Copiarla a través del S.O. Pero usando el metodo SQL, es mas compatible con distintas versiones de SQLite. 
Antes de copiar la BD es conveniente compactarla, sqlite3.exe test.db VACUUM


Modificar una Tabla.

Si queremos modificar algún campo existente.

1 Exportamos la Tabla.
  .mode column
  .output file.sql
  .dump Tabla
  .output stdout

2 Editamos file.sql y hacemos los cambios.

3 Borramos la Tabla, drop table tab_name;

4 Importamos la Tabla, y activamos las foreign_keys.
  .read file.sql
  PRAGMA foreign_keys=ON;

Si queremos añadir un campo usaremos:
	ALTER TABLE equipment ADD COLUMN location text;

The master table holds the key information about your database tables and it is called sqlite_master

sqlite>.schema sqlite_master

