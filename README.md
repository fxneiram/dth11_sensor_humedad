# Dth11 Sensor de humedad

> Hola. Este repositorio cuneta con una carpeta llamada ***libraries*** cuyo contenido deberá ser copiado en la carpeta de librerias Arduino en su equipo.

## Esquemático
![alt text](https://github.com/fxneiram/dth11_sensor_humedad/blob/master/Montaje_esquem%C3%A1tico.png)
## Montaje op1
![alt text](https://github.com/fxneiram/dth11_sensor_humedad/blob/master/Montaje1_bb.png)
## Montaje op2
![alt text](https://github.com/fxneiram/dth11_sensor_humedad/blob/master/Montaje2_bb.png)
```c
#include <DHT_U.h>

#include <DHT.h>
 
// Definimos el pin digital donde se conecta el sensor
#define DHTPIN 2
// Dependiendo del tipo de sensor
#define DHTTYPE DHT11
 
// Inicializamos el sensor DHT11
DHT dht(DHTPIN, DHTTYPE);
 
void setup() {
  // Inicializamos comunicación serie
  Serial.begin(9600);
  // Comenzamos el sensor DHT
  dht.begin();
 
}

void loop() {
    // Esperamos 5 segundos entre medidas
  delay(5000);
 
  // Leemos la humedad relativa
  float h = dht.readHumidity();
  // Leemos la temperatura en grados centígrados
  float t = dht.readTemperature();
  // Leemos la temperatura en grados Fahreheit
  float f = dht.readTemperature(true);
 
  // Comprobamos algún error en la lectura
  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println("Error obteniendo los datos del sensor DHT11");
    return;
  }
 
  // Calcular el índice de calor en Fahreheit
  float hif = dht.computeHeatIndex(f, h);
  // Calcular el índice de calor en grados centígrados
  float hic = dht.computeHeatIndex(t, h, false);
 
  Serial.print("Humedad: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperatura: ");
  Serial.print(t);
  Serial.print(" *C ");
  Serial.print(f);
  Serial.print(" *F\t");
  Serial.print("Índice de calor: ");
  Serial.print(hic);
  Serial.print(" *C ");
  Serial.print(hif);
  Serial.println(" *F");
 
}

```
