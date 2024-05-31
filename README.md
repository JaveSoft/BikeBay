# BikeBay

##### Bikebay constiste en una aplicación web diseñada para alquilar bicicletas, las cuales se encuentran en cicloparqueaderos a lo largo de la ciudad



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
