# BikeBay

##### Bikebay constiste en una aplicación web diseñada para alquilar bicicletas, las cuales se encuentran en cicloparqueaderos a lo largo de la ciudad


![](https://www.plantuml.com/plantuml/png/VP5DJiCm48NtSmfVe1U8K5KA6oHsiA-czgGToJ_fUCm6UdSI8jiYI2pd9JFlUy-7h2XQWWUm7dCsHxPiFIb-0hl1l4Ib2md45Cv2WtbJuNY1W6AnJSj6cb1kXT2HfC4yRHHmbAtmP3d5jeR-LjYJK1xCAsTzU6p27aQoLpoXcvNCwzepAe6YzzYvQEPtgPrK51vn_ZMLioUurrHRdd_3PN9zEDS-AkIn2dl0YKIBp7xl70WiamZLeKofEpIG6l4NG3SPUly6IYuetCDTa-29uzB6Qf8LmxJA8yUjbllz3_H9MYkrisDAdZ0kSDtr_hNR_Ns-YltpkJC272Yw4lmt)

Clases:
* Cicloparqueadero: Representa el parqueadero donde se ubicaran las bicicletas en cada sede.
* Bicicleta: Representa las caracteristicas de las bicicletas que se van a poder alquilar.
* Alquiler: Representa las caracteristicas del alquiler de una bicicleta

# CU001 - Añadir Bicicleta

Flujo de eventos 

| Actor | Sistema |
|-------|---------|
|1. Selecciona el boton "Añadir bicicleta"|
|2. Ingresa los datos de la bicicleta|
|3. Selecciona el cicloparqueadero donde se encuentra la bicicleta|
|4. Selecciona el boton "Guardar"|
||5. Registra los datos en la base de datos|
||6. Muestra un mensaje de confirmación|
||7. Retorna a la pantalla principal|

# CU002 - Eliminar Bicicleta

Flujo de eventos 

| Actor | Sistema |
|-------|---------|
|1. Selecciona el boton "Eliminar bicicleta"|
||2. Muestra un mensaje de confirmación de eliminación|
|3. Selecciona el boton "Aceptar"|
||4. Busca el ID de la bicicleta seleccionada en la base de datos|
||5. Elimina la bicicleta de la base de datos|
||6. Muestra un mensaje de confirmación|
||7. Retorna a la lista de bicicletas|

# CU003 - Mostrar Bicicletas

Flujo de eventos 

| Actor | Sistema |
|-------|---------|
|1. Selecciona el boton "Mostrar bicicletas"|
||2. Muestra una lista con las bicicletas registradas|

# CU004 - Editar Bicicleta

Flujo de eventos 

| Actor | Sistema |
|-------|---------|
|1. Selecciona el boton "Editar bicicleta"|
|2. Cambia las caracteristicas que requiera actualizar|
|3. Selecciona el boton "Guardar"|
||4. Actualiza los datos en la base de datos|
||5. Muestra un mensaje de confirmación|
||6. Retorna a la lista de bicicletas|

# CU005 - Alquilar Bicicleta

Flujo de eventos

| Actor | Sistema |
|-------|---------|
|1.Selecciona el boton "Alquilar bicicleta"|
|2. Ingresa el periodo de tiempo que desea alquilarla|
|3. Selecciona la opción "Alquilar"|
||4. Elimina la disponibilidad de la bicicleta en el periodo de tiempo alquilado, registra el alquiler y cambia el estado de la bicicleta a "Alquilada"|
||5. Muestra un mensaje de confirmación|
||6. Retorna a la pantalla principal|

## Base de datos

##### Para acoplar la aplicación con la base de datos MySQL es necesario crear 3 tablas que representen las entidades del modelo de dominio junto a sus atributos


###### - Tabla Cicloparqueadero
CREATE TABLE Cicloparqueadero (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(255) NOT NULL,
    sede VARCHAR(255) NOT NULL,
    apertura TIME NOT NULL,
    cierre TIME NOT NULL,
    cupo INT NOT NULL
);

###### - Tabla Bicicleta
CREATE TABLE Bicicleta (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(255) NOT NULL,
    marca VARCHAR(255) NOT NULL,
    cicloparqueadero_id INT,
    descripcion TEXT,
    fecha_adquisicion DATE NOT NULL,
    talla INT NOT NULL,
    estado VARCHAR(255) NOT NULL,
    tarifa DOUBLE NOT NULL,
    FOREIGN KEY (cicloparqueadero_id) REFERENCES Cicloparqueadero(id)
);

###### - Tabla Alquiler
CREATE TABLE Alquiler (
    id INT PRIMARY KEY AUTO_INCREMENT,
    bicicleta_id INT,
    usuario VARCHAR(255) NOT NULL,
    hora_inicio TIMESTAMP NOT NULL,
    hora_fin TIMESTAMP,
    horas INT,
    valor DOUBLE,
    estado BOOLEAN NOT NULL,
    FOREIGN KEY (bicicleta_id) REFERENCES Bicicleta(id)
);
