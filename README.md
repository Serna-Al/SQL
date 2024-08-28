# Base de Datos para un Gimnasio

Este proyecto define la estructura de una base de datos para la gestión de un gimnasio. La base de datos permite el registro de usuarios, tipos de membresías, pagos realizados, y el control de asistencias de los usuarios.

## Estructura de la Base de Datos

La base de datos está compuesta por las siguientes tablas:

1. **Usuarios**
   - Almacena la información personal de los usuarios.
   - Campos:
     - `UsuarioID` (INT): Identificador único del usuario.
     - `Nombre` (VARCHAR): Nombre del usuario.
     - `Apellido` (VARCHAR): Apellido del usuario.
     - `FechaNacimiento` (DATE): Fecha de nacimiento del usuario.
     - `CorreoElectronico` (VARCHAR): Correo electrónico del usuario.
     - `Telefono` (VARCHAR): Número de teléfono del usuario.
     - `FechaRegistro` (DATE): Fecha en la que el usuario se registró en el gimnasio.

2. **Membresias**
   - Almacena los diferentes tipos de membresías ofrecidas por el gimnasio.
   - Campos:
     - `MembresiaID` (INT): Identificador único de la membresía.
     - `TipoMembresia` (VARCHAR): Nombre o tipo de la membresía.
     - `DuracionDias` (INT): Duración de la membresía en días.
     - `Costo` (DECIMAL): Costo de la membresía.

3. **Pagos**
   - Registra los pagos de membresías realizados por los usuarios.
   - Campos:
     - `PagoID` (INT): Identificador único del pago.
     - `UsuarioID` (INT): Identificador del usuario que realizó el pago.
     - `MembresiaID` (INT): Identificador de la membresía adquirida.
     - `FechaPago` (DATE): Fecha en la que se realizó el pago.
     - `MontoPagado` (DECIMAL): Monto pagado por la membresía.
     - `FechaExpiracion` (DATE): Fecha de expiración de la membresía.

4. **Asistencias**
   - Registra las asistencias de los usuarios al gimnasio.
   - Campos:
     - `AsistenciaID` (INT): Identificador único de la asistencia.
     - `UsuarioID` (INT): Identificador del usuario que asistió.
     - `FechaAsistencia` (DATE): Fecha de la asistencia.
     - `HoraAsistencia` (TIME): Hora de la asistencia.

## Consultas Útiles

### Ver Membresías Activas de un Usuario

Consulta para obtener las membresías activas de un usuario, ordenadas por la fecha de expiración más reciente:

```sql
SELECT 
    u.Nombre, 
    u.Apellido, 
    m.TipoMembresia, 
    p.FechaPago, 
    p.FechaExpiracion 
FROM 
    Pagos p
JOIN 
    Usuarios u ON p.UsuarioID = u.UsuarioID
JOIN 
    Membresias m ON p.MembresiaID = m.MembresiaID
WHERE 
    p.FechaExpiracion > CURRENT_DATE
ORDER BY 
    p.FechaExpiracion DESC;
```

## Consideraciones

- Esta es una estructura básica que se puede expandir según las necesidades del gimnasio.
- Se pueden agregar tablas adicionales para gestionar entrenadores, clases, reservas, etc.
- Asegúrate de tener los permisos adecuados y realizar respaldos antes de hacer cambios en la base de datos.
- 
