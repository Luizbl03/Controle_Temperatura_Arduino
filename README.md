# Controle de Temperatura com TMP36 e Arduino
**Autor:**[Luizbl03]
(https://github.com/Luizbl03/Controle_Temperatura_Arduino.git)
**Data:** 16 de Agosto de 2025
Este projeto monitora a temperatura ambiente usando um sensor LM35 e controla um cooler (ventoinha) para resfriar um sistema quando a temperatura atinge 30°C. O circuito também possui um LED e um buzzer que alertam quando a temperatura atinge um nível crítico de 50°C.

### Componentes
| Nome | Quantidade | Componente |
|---|---|---|
| UArduinoBoard | 1 | Arduino Uno R3 |
| U1 | 1 | Temperature Sensor [TMP36] |
| K1 | 1 | Relay SPDT |
| M1 | 1 | DC Motor |
| BAT1 | 1 | 9V Battery |
| D6 | 1 | Diode |
| T1, T2 | 2 | NPN Transistor (BJT) |
| R6, R8 | 2 | 1 kΩ Resistor |
| U5 | 1 | 5V Regulator [LM7805] |
| C1 | 1 | 10 uF, 16 V Polarized Capacitor |
| C2 | 1 | 0.1 uF, 16 V Polarized Capacitor |
| PIEZO1 | 1 | Piezo |
| D1 | 1 | Red LED |
| R7 | 1 | 330 kΩ Resistor |

### Diagrama de Circuito
![Diagrama do Circuito no Tinkercad](Simulacao_estufa.png)

### Código
```c++
//Definições de pinos
const int sensorPin = A0;
const int relePin = 2;
const int ledPin = 3;
const int buzzerPin = 4;

void setup() {
	pinMode(relePin, OUTPUT);
	pinMode(ledPin, OUTPUT);
	pinMode(buzzerPin, OUTPUT);
	Serial.begin(9600);
}

void loop() {
	int leitura = analogRead(sensorPin);
  
	// Conversão da leitura para temperatura em Celsius
	float tensao = leitura * (5.0 / 1023.0);
	float temperatura = (tensao - 0.5) * 100;
	Serial.print("Temperatura: ");
	Serial.println(temperatura);
  
	// Controle da ventoinha
	if (temperatura >= 30) {
		digitalWrite(relePin, HIGH); // Liga ventoinha
	} else {
		digitalWrite(relePin, LOW); // Desliga ventoinha
	}
  
	// Alerta de temperatura crítica
	if (temperatura >= 50) {
		digitalWrite(ledPin, HIGH);
		digitalWrite(buzzerPin, HIGH);
	} else {
		digitalWrite(ledPin, LOW);
		digitalWrite(buzzerPin, LOW);
	}
  
	delay(2000); // Aguarda 2 segundos
}
```
### Licença
Este projeto está sob a Licença MIT.

### Créditos
- Desenvolvido por [Luizbl03]


  
