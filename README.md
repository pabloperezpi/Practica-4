## PRACTICA 4:  SISTEMAS OPERATIVOS EN TIEMPO REAL

### CODIGO
``` cpp
void setup()
{
Serial.begin(112500);
xTaskCreate(anotherTask,"another Task",10000,NULL,1,NULL); 
}

void loop()
{
Serial.println("this is ESP32 Task");
delay(1000);
}

void anotherTask( void * parameter )
{
for(;;)
{
Serial.println("this is another Task");
delay(1000);
}
vTaskDelete( NULL );
}
```
## FUNCIONAMIENTO
Mediante la función xTaskCreate(), se crea una nueva tarea. La función AnotherTask() es la tarea generada dentro de setup(), donde se imprime repetidamente el mensaje "this is another task".

En el bucle principal loop(), se imprime constantemente el mensaje "this is ESP32 Task".

Al final, se llama a vTaskDelete(NULL) para eliminar la tarea. Sin embargo, debido al bucle infinito dentro de AnotherTask(), esta llamada nunca se ejecutará, por lo que la tarea creada continuará ejecutándose indefinidamente.



En caso de que el programa este bien ejecutado imprimira en la consola el siguiente mensaje:
```cpp
this is ESP32 Task - (espera 1 segundo) - this is another Task - (espera 1 segundo) - this is ESP32 Task - (espera 1 segundo) - etc.
```

