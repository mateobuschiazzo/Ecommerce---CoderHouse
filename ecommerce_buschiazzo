CREATE database ecommerce;
USE ecommerce;
CREATE TABLE clientes(
  id_cliente  INT AUTO_INCREMENT PRIMARY KEY,
  email   VARCHAR(50) NOT NULL UNIQUE,
  nombre_completo  VARCHAR(50) NOT NULL,
  telefono INT NOT NULL)
;
CREATE TABLE direcciones (
  id_direccion  INT AUTO_INCREMENT PRIMARY KEY,
  id_cliente   INT  NOT NULL,
  alias   VARCHAR(50) NOT NULL, 
  calle  VARCHAR(200) NOT NULL,
  ciudad   VARCHAR(100) NOT NULL,
  provincia  VARCHAR(100) NOT NULL,
  codigo_postal  VARCHAR(20) NOT NULL,
  pais   VARCHAR(100) NOT NULL,
  CONSTRAINT fk_dir_cliente
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);

CREATE TABLE categorias (
  id_categoria   INT AUTO_INCREMENT PRIMARY KEY,
  nombre   VARCHAR(120) NOT NULL UNIQUE
);

CREATE TABLE productos (
  id_producto INT AUTO_INCREMENT PRIMARY KEY,
  sku   VARCHAR(64) NOT NULL UNIQUE,
  nombre  VARCHAR(200) NOT NULL,
  descripcion VARCHAR(2000),
  precio  DECIMAL(12,2) NOT NULL,
  activo   BOOLEAN NOT NULL DEFAULT TRUE,
  id_categoria  INT NOT NULL,
  CONSTRAINT fk_prod_categoria
    FOREIGN KEY (id_categoria) REFERENCES categorias(id_categoria)
);
CREATE TABLE pedidos (
  id_pedido    INT AUTO_INCREMENT PRIMARY KEY,
  id_cliente    INT NOT NULL,
  id_direccion   INT NOT NULL,
  moneda   CHAR(3) NOT NULL,
  importe_subtotal   DECIMAL(12,2) NOT NULL,
  importe_descuento  DECIMAL(12,2) NOT NULL DEFAULT 0,
  importe_envio    DECIMAL(12,2) NOT NULL DEFAULT 0,
  importe_impuesto  DECIMAL(12,2) NOT NULL DEFAULT 0,
  importe_total    DECIMAL(12,2) AS (importe_subtotal - importe_descuento + importe_envio + importe_impuesto) STORED,
  fecha_pedido   DATETIME NOT NULL,

  CONSTRAINT fk_ped_cliente
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente),
  CONSTRAINT fk_ped_direccion
    FOREIGN KEY (id_direccion) REFERENCES direcciones(id_direccion)
);
CREATE TABLE lineas_pedido (
  id_pedido         INT NOT NULL,
  id_producto       INT NOT NULL,
  cantidad            INT  NOT NULL,
  precio_unitario     DECIMAL(12,2) NOT NULL,
  descuento_unitario  DECIMAL(12,2) NOT NULL DEFAULT 0,
  PRIMARY KEY (id_pedido, id_producto),
  CONSTRAINT fk_lp_pedido
    FOREIGN KEY (id_pedido)   REFERENCES pedidos(id_pedido),
  CONSTRAINT fk_lp_producto
    FOREIGN KEY (id_producto) REFERENCES productos(id_producto)
)
