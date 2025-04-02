Base de Datos CampusLands - Sistema de Gestión Académica
ER Diagram

📌 Descripción
Este repositorio contiene el diseño e implementación completa de un sistema de gestión académica para CampusLands, diseñado para:

Gestionar el seguimiento académico de campers (estudiantes)

Administrar rutas de aprendizaje y módulos

Controlar evaluaciones y progreso educativo

Organizar asignación de trainers (instructores) y áreas de entrenamiento

🛠 Tecnologías Utilizadas
MySQL 8.0 (o MariaDB 10.5+)

Diagrama ER con Mermaid JS

Normalización hasta 3FN (Tercera Forma Normal)

🗃 Estructura de la Base de Datos
Principales Entidades
Entidad	Descripción
CAMPER	Información de estudiantes
RUTA	Rutas de aprendizaje (Frontend, Backend...)
MODULO	Módulos de cada ruta
EVALUACION	Resultados académicos con cálculos automáticos
TRAINER	Instructores asignados
AREA_ENTRENAMIENTO	Espacios físicos con capacidad limitada
Características Clave
✅ Normalización estricta (3FN)
✅ Columnas generadas para cálculos automáticos
✅ Restricciones avanzadas (CHECK, UNIQUE, FK)
✅ Datos de prueba completos (50+ inserts por tabla)

📊 Diagrama ER
mermaid
Copy
erDiagram
    CAMPER ||--o{ TELEFONO_CAMPER : "tiene"
    CAMPER ||--|| ACUDIENTE : "acudiente"
    CAMPER ||--o{ INSCRIPCION : "inscrito"
    RUTA ||--o{ MODULO : "contiene"
    MODULO ||--o{ EVALUACION : "evalúa"
    TRAINER ||--o{ RUTA_TRAINER : "imparte"
    RUTA ||--o{ RUTA_TRAINER : "asignada"
🚀 Cómo Implementar
Ejecutar scripts SQL en orden:

bash
Copy
mysql -u usuario -p < 01_estructura.sql
mysql -u usuario -p < 02_datos_prueba.sql
Consultas de ejemplo:

sql
Copy
-- Promedio de notas por ruta
SELECT r.nombre, AVG(e.nota_final) as promedio
FROM RUTA r
JOIN INSCRIPCION i ON r.id_ruta = i.id_ruta
JOIN EVALUACION e ON i.id_camper = e.id_camper
GROUP BY r.nombre;

-- Trainers y sus rutas asignadas
SELECT t.nombres, t.apellidos, GROUP_CONCAT(r.nombre) as rutas
FROM TRAINER t
JOIN RUTA_TRAINER rt ON t.id_trainer = rt.id_trainer
JOIN RUTA r ON rt.id_ruta = r.id_ruta
GROUP BY t.id_trainer;
