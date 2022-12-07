"# Curso DevOps 2022" 

Para hacer funcionar la aplicación (desde cmd):

1- Establecer la variable PYTHONPATH aputando a esta carpeta:

SET PYTHONPATH=.

2.- Desde esta carpeta ejecutar la app:

python app\calc.py

3.- Otros componentes de la prueba

* flask: Ejecución de microservicios:

SET FLASK_APP=app\api.py
flask run

* Wiremocks: Para respuesta falsas a microservicios

java -jar C:\Users\david\Downloads\wiremock-jre8-standalone-2.35.0.jar  --port 9090 --root-dir test\wiremock

* pytest: Para pruebas unitarias, para ejecutarlo:

pytest test\unit
pytest test\rest