"# Curso DevOps 2022" 

Para hacer funcionar la aplicación (desde cmd):

1- Establecer la variable PYTHONPATH aputando a esta carpeta:

SET PYTHONPATH=.

2.- Desde esta carpeta ejecutar la app:

python app\calc.py



===========================

Componentes para la prueba:

* flask: Ejecución de microservicios:

SET FLASK_APP=app\api.py

* pytest: Para pruebas unitarias, para ejecutarlo:

pytest test\unit