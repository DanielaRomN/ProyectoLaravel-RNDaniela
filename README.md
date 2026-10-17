# CI Pipeline para Laravel

## Objetivo

Automatizar la instalación de dependencias y la ejecución de pruebas de la aplicación Laravel mediante GitHub Actions, verificando cada cambio enviado a la rama principal.

## Tecnologías

- PHP [tu versión, ej. 8.4]
- Laravel [tu versión, ej. 11]
- Composer
- PHPUnit
- Git y GitHub
- GitHub Actions

## Requisitos

- PHP compatible con el proyecto
- Composer
- Git
- Cuenta y repositorio en GitHub

## Instalación local

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/[tu-usuario]/[tu-repo].git
   cd [tu-repo]

2. Instalar dependencias:
    composer install

3. Copiar el archivo de entorno y generar la clave:

    cp .env.example .env
    php artisan key:generate

4. Configurar la base de datos requerida (para pruebas se usa SQLite en memoria).

5. Ejecutar migraciones si son necesarias:

    php artisan migrate

6. Ejecutar las pruebas:

    php artisan test

## Integración continua
    El workflow .github/workflows/ci.yml se ejecuta automáticamente al hacer push a la rama main o al crear un pull request dirigido a ella.

    El pipeline realiza lo siguiente:

    Obtiene el código del repositorio.

    Configura PHP con las extensiones necesarias.

    Valida composer.json.

    Instala las dependencias.

    Prepara el entorno Laravel (.env y key:generate).

    Ejecuta las pruebas automatizadas con php artisan test.

## Pruebas
    La prueba principal es tests/Feature/HomePageTest.php, que realiza una petición HTTP a la ruta / y verifica que la respuesta sea exitosa (HTTP 200).

    php
    public function test_home_page_is_accessible(): void
    {
        $response = $this->get('/');
        $response->assertSuccessful();
    }

## Resultado esperado
    La prueba debe pasar en local y en GitHub Actions.

    El pipeline debe finalizar en verde.

## Resultado obtenido
    Ejecución local: [PASS / FAIL]

    Ejecución en GitHub Actions: [PASS / FAIL]

## Evidencias
Repositorio: https://github.com/DanielaRomN/ProyectoLaravel-RNDaniela/actions/runs/38983624785

Ejecución exitosa inicial: [enlace a la ejecución]

Ejecución fallida controlada: [enlace a la ejecución]

Ejecución exitosa posterior a la corrección: [enlace a la ejecución]

Ejecución fallida controlada
Se modificó la aserción de assertSuccessful() a assertStatus(404). Como la ruta / responde con HTTP 200, la prueba falló con el mensaje:

text
Expected response status code [404] but received 200.
GitHub Actions marcó el job como fallido, demostrando que el pipeline detecta y reporta errores correctamente.

Solución: restaurar la aserción original assertSuccessful().

Ejecución exitosa posterior
Tras restaurar la aserción y hacer push, el pipeline volvió a pasar en verde, confirmando que el flujo de integración continua funciona de extremo a extremo.