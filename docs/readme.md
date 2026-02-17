# Base de Datos

Curso de Base de Datos con ejemplos prácticos y ejercicios.

---

## SQL Commands

| Categoría | Comandos |
|-----------|----------|
| **DQL** (Data Query Language) | SELECT |
| **DDL** (Data Definition Language) | CREATE, DROP, ALTER, TRUNCATE |
| **DML** (Data Manipulation Language) | INSERT, UPDATE, DELETE |
| **DCL** (Data Control Language) | GRANT, REVOKE |
| **TCL** (Transaction Control Language) | COMMIT, ROLLBACK, SAVEPOINT |

---

## Creación de Tablas

### Tabla 1: users

```sql
CREATE TABLE users(
    id INT PRIMARY KEY AUTO_INCREMENT,
    names VARCHAR(55),
    lastname VARCHAR(55),
    email VARCHAR(125) UNIQUE
);
```

### Tabla 2: users2

```sql
CREATE TABLE users2(
    id INT PRIMARY KEY AUTO_INCREMENT,
    names VARCHAR(45),
    lastname VARCHAR(45),
    document VARCHAR(45),
    email VARCHAR(45),
    address VARCHAR(45),
    phone VARCHAR(45),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Tabla 3: products

```sql
CREATE TABLE products(
    id INT PRIMARY KEY AUTO_INCREMENT,
    names VARCHAR(45),
    description VARCHAR(45),
    price VARCHAR(45),
    image VARCHAR(45),
    is_expired TINYINT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Actividad

**Objetivo**: Insertar diez registros en la tabla `users` y diez registros en la tabla `products`.

#### Solución - Insertar Datos

```sql
INSERT INTO table_name (column_a, column_b)
VALUES ("value_a", "value_b");
```

---

## DQL, DDL y DML explicados.

### DQL | Data Query Language

Utilizada para recuperar datos de bases de datos mediante la instrucción **SELECT**.

---

### DDL | Data Definition Language

Comandos para definir la estructura de la base de datos:

| Comando | Descripción |
|---------|-------------|
| **CREATE** | Permite construir objetos de la base de datos (tablas, bases de datos, índices) |
| **ALTER** | Se usa para modificar la estructura de un objeto existente |
| **DROP** | Elimina un objeto completo de la base de datos, incluyendo su estructura y datos |
| **TRUNCATE** | Elimina todas las filas de una tabla, pero mantiene su estructura intacta |

---

### Tipos de Datos y Restricciones

#### Tipos de Datos

- `INT` - Enteros
- `VARCHAR` - Cadena de caracteres variable
- `DATE` - Fecha
- `BOOLEAN` - Valor lógico (verdadero/falso)
- `DECIMAL(p,s)` - Número decimal con precisión

#### Restricciones (Constraints)

| Restricción | Descripción |
|-------------|-------------|
| **PRIMARY KEY** | Garantiza la unicidad e identifica de forma exclusiva cada fila |
| **FOREIGN KEY** | Establece un vínculo entre dos tablas, manteniendo la coherencia referencial |
| **UNIQUE** | Asegura que todos los valores en una columna son diferentes |
| **NOT NULL** | Obliga a que una columna siempre contenga un valor |

---

### DML | Data Manipulation Language

Comandos para manipular datos:

| Comando | Descripción |
|---------|-------------|
| **INSERT** | Insertar nuevos registros |
| **UPDATE** | Actualizar registros existentes |
| **DELETE** | Eliminar registros |

#### Sintaxis INSERT

```sql
INSERT INTO table_name (column_a, column_b)
SELECT valor_a, valor_b FROM otra_tabla;
```

#### Sintaxis UPDATE

```sql
UPDATE table_name
SET column = value
WHERE condition;
```

#### Sintaxis DELETE

```sql
DELETE FROM table_name
WHERE condition;
```

---

### DCL | Data Control Language

Comandos para gestionar permisos:

#### GRANT - Otorgar Permisos

```sql
GRANT privilege_name ON object_name TO {user_name | PUBLIC | role_name} [WITH GRANT OPTION];
```

#### REVOKE - Quitar Permisos

```sql
REVOKE privilege_name ON object_name FROM user_name;
```

---

## Repaso y Ejercicios.

### Ejemplos de DQL (SELECT)

```sql
-- Seleccionar todos los usuarios
SELECT * FROM users u;

-- Mostrar solo nombre, apellido y email
SELECT first_name, last_name, email FROM users u;

-- Filtrar usuarios cuyo rol sea 'admin'
SELECT * FROM users u WHERE role = 'admin';

-- Filtrar usuarios con documento tipo 'CC'
SELECT * FROM users u WHERE document_type = 'CC';

-- Filtrar usuarios menores de 18 años (fecha de nacimiento mayor a 2006)
SELECT * FROM users u WHERE u.birth_date < '2026-01-01';

-- Filtrar usuarios cuyo nombre empiecen por "a"
SELECT * FROM users u WHERE u.first_name LIKE 'a%';

-- Filtrar usuarios sin empresa
SELECT * FROM users u WHERE u.company IS NULL;

-- Usuarios mayores de 18 años que sean empleados
SELECT * FROM users u WHERE u.birth_date < '2001-01-01' AND role = 'employee';

-- Usuarios con 'CC' que estén activos
SELECT * FROM users u WHERE u.document_type = 'CC' AND u.is_active = '1';
```

---

### Actividades - Niveles de Dificultad.

#### Nivel 1: Fundamentos

```sql
-- Listar todos los usuarios
SELECT * FROM users u;
```
![Evidencia](./img/n1_1.png)

```sql
-- Mostrar solo first_name, last_name, email
SELECT u.first_name, u.last_name, u.email FROM users u;
```
![Evidencia](./img/n1_2.png)

```sql
-- Filtrar usuarios cuyo role sea 'admin'
SELECT * FROM users u WHERE role = 'admin'
```
![Evidencia](./img/n1_3.png)

```sql
-- Filtrar usuarios con document_type = 'CC' 
SELECT * FROM users u WHERE u.document_type = 'CC'
```
![Evidencia](./img/n1_4.png)

```sql
-- Mostrar usuarios mayores de 18 años
SELECT * FROM users u WHERE u.birth_date < '2006-01-01'
```
![Evidencia](./img/n1_5.png)

```sql
-- Mostrar usuarios con ingreso mayor a 5,000,000 
SELECT * FROM users u WHERE u.monthly_income > '5000000'
```
![Evidencia](./img/n1_6.png)

```sql
--  Mostrar usuarios cuyo nombre empiece por "A"
SELECT * FROM users u WHERE u.first_name LIKE 'a%'
```
![Evidencia](./img/n1_7.png)

```sql
-- Mostrar usuarios que no tengan company 
SELECT * FROM users u WHERE u.company IS NULL
```
![Evidencia](./img/n1_8.png)

#### Nivel 2: Combinación de Condiciones

```sql
-- Usuarios mayores de 25 años que sean 'employee'
SELECT * FROM users u WHERE u.birth_date < '2001-01-01' AND role = 'employee';
```
![Evidencia](./img/n2_1.png)

```sql
-- Usuarios con 'CC' que estén activos
SELECT * FROM users u WHERE u.document_type = 'CC' AND u.is_active = '1';
```
![Evidencia](./img/n2_2.png)

```sql
-- Usuarios mayores de edad sin empleo
SELECT * FROM users u WHERE u.birth_date < '2006-01-01' AND u.company IS NULL;
```
![Evidencia](./img/n2_3.png)

```sql
-- Usuarios con empleo y con ingresos mayores a 3,000,000
SELECT * FROM users u WHERE u.company IS NOT NULL AND u.monthly_income > '3000000';
```
![Evidencia](./img/n2_4.png)

```sql
-- Usuarios casados con al menos 1 hijo
SELECT * FROM users u WHERE u.marital_status = 'Casado' AND u.children_count >= '1';
```
![Evidencia](./img/n2_5.png)

```sql
-- Usuarios entre 30 y 40 años (Forma 1)
SELECT * FROM users u WHERE u.birth_date < '1996-01-01' AND u.birth_date > '1986-01-01';
```
![Evidencia](./img/n2_6_f1.png)

```sql
-- Usuarios entre 30 y 40 años (Forma 2 - BETWEEN)
SELECT * FROM users u WHERE u.birth_date BETWEEN '1986-01-01' AND '1996-01-01';
```
![Evidencia](./img/n2_6_f2.png)

```sql
-- Usuarios 'admin' verificados mayores de 25 años
SELECT * FROM users u WHERE (u.birth_date < '2001-12-31' AND role = 'admin') AND (is_active = 1);
```
![Evidencia](./img/n2_7.png)

#### Nivel 3: Agregaciones

```sql
-- Contar usuarios por role
SELECT role, COUNT(*) AS 'quantity' FROM users u GROUP BY role;
```
![Evidencia](./img/n3_1.png)

```sql
-- Contar usuarios por document_type
SELECT document_type, COUNT(*) AS 'quantity' FROM users u GROUP BY u.document_type;
```
![Evidencia](./img/n3_2.png)

```sql
-- Contar cuántos usuarios están desempleados
SELECT company, COUNT(*) AS 'quantity' FROM users u WHERE company IS NULL GROUP BY u.company;
```
![Evidencia](./img/n3_3.png)

```sql
-- Calcular el promedio general de ingresos
SELECT AVG(u.monthly_income) AS 'average' FROM users u;
```
![Evidencia](./img/n3_4.png)

```sql
-- Calcular el promedio de ingresos por role
SELECT role, AVG(u.monthly_income) AS 'average' FROM users u GROUP BY u.role;
```
![Evidencia](./img/n3_5.png)

#### Nivel 4: Pensamiento Analítico

```sql
-- Mostrar profesiones con más de 10 personas
SELECT profession, COUNT(*) AS 'quantity_employees' 
FROM users u 
WHERE profession IS NOT NULL 
GROUP BY u.profession 
HAVING COUNT(*) > 10;
```
![Evidencia](./img/n4_1.png)

```sql
-- Mostrar la ciudad con más usuarios
SELECT city, COUNT(*) AS 'users' 
FROM users u 
GROUP BY u.city 
ORDER BY 'users' LIMIT 1;
```
![Evidencia](./img/n4_2.png)

```sql
-- Comparar cantidad de menores vs mayores de edad
SELECT CASE WHEN birth_date > '2008-01-01' THEN 'minor' ELSE 'adult' END AS age_group, 
COUNT(*) AS result 
FROM users u  
GROUP BY age_group;
```
![Evidencia](./img/n4_3.png)

```sql
-- Promedio de ingresos por ciudad ordenado de mayor a menor
SELECT city, AVG(u.monthly_income) AS average 
FROM users u 
WHERE u.monthly_income IS NOT NULL 
GROUP BY city, u.monthly_income 
HAVING COUNT(*) > 0 
ORDER BY average DESC;
```
![Evidencia](./img/n4_4.png)

```sql
-- Mostrar las 5 personas con mayor ingreso
SELECT first_name, monthly_income 
FROM users u 
WHERE u.monthly_income IS NOT NULL 
GROUP BY u.first_name,u.monthly_income 
ORDER BY u.monthly_income DESC LIMIT 5;
```
![Evidencia](./img/n4_5.png)

#### Nivel 5: Ingeniero

```sql
-- Clasificar usuarios como: "Menor", "Adulto", "Adulto mayor" (1ra Forma)
SELECT first_name,
    COUNT(CASE WHEN birth_date >= '2008-01-01' THEN 0 END) AS minors,
    COUNT(CASE WHEN birth_date BETWEEN '1970-01-01' AND '2008-01-01' THEN 0 END) AS adult,
    COUNT(CASE WHEN birth_date <= '1970-01-01' THEN 0 END) AS older_adult 
FROM users u 
GROUP BY first_name, u.birth_date 
ORDER BY u.birth_date DESC;
```
![Evidencia](./img/n5_1_f1.png)

```sql
-- Clasificar usuarios (2da Forma - CASE)
SELECT first_name,
    CASE 
        WHEN birth_date >= '2008-01-01' THEN 'minors' 
        WHEN birth_date BETWEEN '1970-01-01' AND '2008-01-01' THEN 'adult' 
        ELSE 'older_adult' 
    END AS Clasification
FROM users u 
GROUP BY first_name, u.birth_date 
ORDER BY u.birth_date DESC;
```
![Evidencia](./img/n5_1_f2.png)

```sql
-- Mostrar cuántos usuarios hay en cada clasificación
SELECT 
    COUNT(CASE WHEN birth_date >= '2008-01-01' THEN 0 END) AS minors,
    COUNT(CASE WHEN birth_date BETWEEN '1970-01-01' AND '2008-01-01' THEN 0 END) AS adult,
    COUNT(CASE WHEN birth_date <= '1970-01-01' THEN 0 END) AS older_adult 
FROM users u;
```
![Evidencia](./img/n5_2.png)

```sql
-- Ranking de ingresos por ciudad
SELECT city, SUM(u.monthly_income), 
RANK() OVER (ORDER BY SUM(u.monthly_income) DESC) AS ranking 
FROM users u 
GROUP BY u.city;
```
![Evidencia](./img/n5_3.png)

```sql
-- Profesión con mayor ingreso promedio
SELECT profession, AVG(u.monthly_income) AS average 
FROM users u 
GROUP BY u.profession 
ORDER BY average DESC LIMIT 1;
```
![Evidencia](./img/n5_4.png)

```sql
-- Mostrar usuarios cuyo ingreso esté por encima del promedio general
SELECT first_name, monthly_income 
FROM users u 
WHERE u.monthly_income > (SELECT AVG(u.monthly_income) FROM users u) 
ORDER BY u.monthly_income DESC;
```
![Evidencia](./img/n5_5.png)

---

## Herramientas y Tecnologías

### Node.js

```bash
# Verificar versión de Node.js
node --v
```

### Docusaurus

**Docusaurus** es un generador de sitios estáticos. Construye una aplicación de una sola página con navegación rápida del lado del cliente, aprovechando todo el poder de React para hacer su sitio interactivo.

**Recursos**:
- [Sitio oficial](https://docusaurus.io/)
- [Guía de instalación](https://gist.github.com/andrescortesdev/6f7cf37dd45e68dac7f78248e0fffb2a)

#### Instalación

```bash
# Crear nuevo proyecto Docusaurus
npx create-docusaurus@latest my-website classic

# Iniciar servidor de desarrollo
cd my-website
npx docusaurus start

# Compilar para producción
npm run build

# Instalar la CLI de Firebase
npm install -g firebase-tools

# Iniciar sesión en Firebase
firebase login

# Inicia la configuración de Firebase
firebase init

# Este comando despliega tu sitio a Firebase Hosting.
firebase deploy

```

#### Notas
- Seleccionar **TypeScript** cuando se solicite
- Instalar dependencias con: `npm install`
- Si el proyecto ya existe: `npm start`

#### Dependencias Adicionales

```bash
npm install @docusaurus/core @docusaurus/preset-classic
```

### Firebase

Permite desplegar nuestra aplicación en internet.

---

## Normalización de Bases de Datos.

La normalización es el proceso de organizar datos en una base de datos para:

- Eliminar redundancia
- Evitar anomalías de inserción, actualización y eliminación
- Mejorar la integridad de los datos

### Formas Normales

| Forma Normal | Objetivo |
|--------------|----------|
| **1FN** (Primera Forma Normal) | Elimina listas y valores múltiples. Los atributos deben ser atómicos |
| **2FN** (Segunda Forma Normal) | Suprime dependencias parciales en claves primarias compuestas |
| **3FN** (Tercera Forma Normal) | Elimina dependencias transitivas |

> **Nota**: La mayoría de bases de datos llegan hasta la 3FN por balancear integridad y rendimiento. Las formas 4FN, 5FN y superiores son para casos especiales (sectores críticos como banca, salud o investigación).

---

### Cardinalidad

La cardinalidad define la unicidad de los datos en una columna o el número de filas en una tabla.

#### Tipos de Cardinalidad

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Uno a Uno (1:1)** | Una fila en Tabla A se relaciona solo con una en Tabla B | Usuario y Perfil |
| **Uno a Muchos (1:N)** | Una fila en Tabla A se relaciona con varias en Tabla B | Cliente y Pedidos |
| **Muchos a Muchos (N:M)** | Varias filas en A con varias en B | Estudiantes y Cursos |

---

### Relaciones entre Tablas

#### Relación Identificada

- La entidad hija no existe sin el padre
- La clave primaria del padre forma parte de la clave primaria del hijo
- **Gráfico (ERD)**: Línea continua sólida
- **Ejemplo**: Relación entre "Factura" (Padre) y "DetalleFactura" (Hija)

#### Relación No Identificada

- La entidad hija puede existir independientemente del padre
- La clave primaria del padre se incluye solo como clave foránea (FK)
- **Gráfico (ERD)**: Línea discontinua o punteada
- **Ejemplo**: Relación entre "Empleado" y "Departamento"

---

### INNER JOIN

La palabra clave SELECT selecciona los registros que tienen valores coincidentes en las dos tablas.

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;
```

---

### Ejercicios de Normalización

#### Normalización 1

**Tabla Original (Sin normalizar)**

```sql
CREATE TABLE table_original (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name_student VARCHAR(50),
    email_student VARCHAR(50),
    id_course INT,
    name_course VARCHAR(50),
    teacher_course VARCHAR(50)
);
```

**Tablas Normalizadas**

```sql
-- Tabla Estudiantes
CREATE TABLE students (
    id_students INT PRIMARY KEY,
    name_student VARCHAR(50),
    email_student VARCHAR(50)
);

-- Tabla Profesores
CREATE TABLE teachers (
    id_teachers INT PRIMARY KEY,
    name_teacher VARCHAR(50)
);

-- Tabla Cursos
CREATE TABLE courses (
    id_course INT PRIMARY KEY,
    name_course VARCHAR(50),
    id_teachers INT,
    FOREIGN KEY (id_teachers) REFERENCES teachers(id_teachers)
);

-- Tabla Estudiante-Curso
CREATE TABLE students_courses (
    id_students INT,
    id_course INT,
    PRIMARY KEY (id_students, id_course),
    FOREIGN KEY (id_students) REFERENCES students(id_students),
    FOREIGN KEY(id_course) REFERENCES courses(id_course)
);
```
![Evidencia](./img/norma1.png)

---

#### Normalización 2

**Tabla Original**

```sql
CREATE TABLE table_original (
    id INT NOT NULL AUTO_INCREMENT,
    name_student VARCHAR(50) NOT NULL,
    email_student VARCHAR(100) NOT NULL,
    university VARCHAR(50) NOT NULL,
    city_university VARCHAR(50) NOT NULL,
    id_course INT NOT NULL,
    name_course VARCHAR(50) NOT NULL,
    teacher VARCHAR(50) NOT NULL,
    email_teacher VARCHAR(50) NOT NULL,
    semester INT NOT NULL,
    PRIMARY KEY (id)
);
```

**Tablas Normalizadas**

```sql
-- Tabla Universidades
CREATE TABLE universitys (
    id_university INT PRIMARY KEY,
    name_university VARCHAR(50),
    city_university VARCHAR(50)
);

-- Tabla Estudiantes
CREATE TABLE students (
    id_students INT PRIMARY KEY,
    name_students VARCHAR(50),
    email_students VARCHAR(50),
    id_university INT,
    FOREIGN KEY (id_university) REFERENCES universitys(id_university)
);

-- Tabla Profesores
CREATE TABLE teachers (
    id_teachers INT PRIMARY KEY,
    name_teachers VARCHAR(50),
    email_teachers VARCHAR(100)
);

-- Tabla Cursos
CREATE TABLE courses (
    id_courses INT PRIMARY KEY,
    name_courses VARCHAR(50),
    id_teachers INT,
    FOREIGN KEY (id_teachers) REFERENCES teachers(id_teachers)
);

-- Tabla Matrículas
CREATE TABLE registrations (
    id_students INT,
    id_courses INT,
    semester VARCHAR(10),
    PRIMARY KEY (id_students, id_courses, semester),
    FOREIGN KEY (id_students) REFERENCES students(id_students),
    FOREIGN KEY (id_courses) REFERENCES courses(id_courses)
);
```
![Evidencia](./img/norma2.png)

---

#### Normalización 3

**Tabla Original**

```sql
CREATE TABLE table_original (
    id INT NOT NULL AUTO_INCREMENT,
    id_order INT NOT NULL,
    date_order DATE NOT NULL,
    id_client INT NOT NULL,
    name_client VARCHAR(50) NOT NULL,
    email_client VARCHAR(100) NOT NULL,
    city_client VARCHAR(50) NOT NULL,
    id_product INT NOT NULL,
    name_product VARCHAR(50) NOT NULL,
    category_product VARCHAR(50) NOT NULL,
    provider VARCHAR(50) NOT NULL,
    provider_phone VARCHAR(20) NOT NULL,
    quantity INT NOT NULL,
    price_unitary VARCHAR(50) NOT NULL,
    order_total VARCHAR(50) NOT NULL,
    PRIMARY KEY (id)
);
```

**Tablas Normalizadas**

```sql
-- Tabla Clientes
CREATE TABLE clients (
    id_client INT PRIMARY KEY,
    name_client VARCHAR(50),
    email_client VARCHAR(100),
    city_client VARCHAR(50)
);

-- Tabla Proveedores
CREATE TABLE providers (
    id_provider INT PRIMARY KEY,
    name_provider VARCHAR(50),
    provider_phone VARCHAR(20)
);

-- Tabla Categorías
CREATE TABLE categories (
    id_category INT PRIMARY KEY,
    category_product VARCHAR(50)
);

-- Tabla Productos
CREATE TABLE products (
    id_product INT PRIMARY KEY,
    name_product VARCHAR(50),
    id_category INT,
    id_provider INT,
    price_unitary DECIMAL(12,2),
    FOREIGN KEY (id_category) REFERENCES categories(id_category),
    FOREIGN KEY (id_provider) REFERENCES providers(id_provider)
);

-- Tabla Pedidos
CREATE TABLE orders (
    id_order INT PRIMARY KEY,
    date_order DATE NOT NULL,
    id_client INT,
    FOREIGN KEY (id_client) REFERENCES clients(id_client)
);

-- Tabla Detalles del Pedido
CREATE TABLE orders_details (
    id_order INT,
    id_product INT,
    quantity INT,
    PRIMARY KEY (id_order, id_product),
    FOREIGN KEY (id_order) REFERENCES orders(id_order),
    FOREIGN KEY (id_product) REFERENCES products(id_product)
);
```
![Evidencia](./img/norma3.png)

---

#### Normalización 4

**Tabla Original**

```sql
CREATE TABLE table_original (
    id INT NOT NULL AUTO_INCREMENT,
    ref_operation INT NOT NULL,
    date_operation DATE NOT NULL,
    id_people INT NOT NULL,
    people VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL,
    ubication VARCHAR(50) NOT NULL,
    id_article INT NOT NULL,
    description_article VARCHAR(50) NOT NULL,
    type_article VARCHAR(50) NOT NULL,
    organization VARCHAR(50) NOT NULL,
    organization_contact VARCHAR(20) NOT NULL,
    quantity INT NOT NULL,
    price_unit VARCHAR(50) NOT NULL,
    total_value_of_transaction VARCHAR(50) NOT NULL,
    PRIMARY KEY (id)
);
```

**Tablas Normalizadas**

```sql
-- Tabla Personas
CREATE TABLE peoples (
    id_people INT PRIMARY KEY,
    name_people VARCHAR(50),
    email VARCHAR(50),
    ubication VARCHAR(50)
);

-- Tabla Organizaciones
CREATE TABLE organizations (
    id_organization INT PRIMARY KEY,
    name_organization VARCHAR(50),
    organization_contact VARCHAR(20)
);

-- Tabla Tipos de Artículo
CREATE TABLE type_articles (
    id_type INT PRIMARY KEY,
    type_article VARCHAR(50)
);

-- Tabla Artículos
CREATE TABLE articles (
    id_article INT PRIMARY KEY,
    description_article VARCHAR(100),
    id_type INT,
    id_organization INT,
    price_unit DECIMAL(12,2),
    FOREIGN KEY (id_type) REFERENCES type_articles(id_type),
    FOREIGN KEY (id_organization) REFERENCES organizations(id_organization)
);

-- Tabla Operaciones
CREATE TABLE operations (
    ref_operation INT PRIMARY KEY,
    date_operation DATE,
    id_people INT,
    FOREIGN KEY (id_people) REFERENCES peoples(id_people)
);

-- Tabla Detalle de Operaciones
CREATE TABLE operations_details (
    ref_operation INT,
    id_article INT,
    quantity INT,
    PRIMARY KEY (ref_operation, id_article),
    FOREIGN KEY (ref_operation) REFERENCES operations(ref_operation),
    FOREIGN KEY (id_article) REFERENCES articles(id_article)
);
```
![Evidencia](./img/norma4.png)

---

## Node.js y Express

### Instalación de Dependencias

```bash
# Inicializar proyecto Node.js
npm init -y

# Instalar Express
npm install express

# Instalar MySQL2
npm install express mysql2
```

### Conexión a MySQL con Express

```javascript
// conexion pool ExpressJS con mysql2:
const pool = mysql.createPool({
    host: ' ',                    // servidor MySQL
    user: 'root',                // usuario
    password: ' ',              // contraseña
    database: ' ',             // base de datos
    waitForConnections: true, // si no hay conexiones, esperar
    connectionLimit: 10,     // máximo de conexiones simultáneas
    queueLimit: 0           // sin límite de cola
});
```

---

## Recursos Adicionales

- [DocusaurusWeb](https://docusaurus-e9f64.web.app/)
- [Express.js](https://expressjs.com/es/)
- [Guía Docusaurus](https://gist.github.com/andrescortesdev/6f7cf37dd45e68dac7f78248e0fffb2a)
- [Actividad Clase 4](https://gist.github.com/andrescortesdev/af60b67b38e14a1adde6e58fdc45b8a7)
- [Presentación de la Clase 2](https://www.canva.com/design/DAHA1jxPFmA/6V0965VUuE4b1Yz5rGsYgg/edit)
- [Formulario de entrega](https://docs.google.com/forms/d/e/1FAIpQLSerGMjF3yC_NEFIbx8oJT6zbkAkriLp9Niqg5XbJEAt76THsw/viewform)

---

> **Nota**: Este documento contiene material del curso de Base de Datos. Para actividades y proyectos, consulta las instrucciones específicas proporcionadas por el instructor.