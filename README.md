**Introdução**

Este projeto é um protótipo de semáforo usando LEDs. Ele simula o funcionamento de um semáforo tradicional, alternando entre os estados de luz verde, amarela e vermelha, com o suporte de um som de alerta emitido por um buzzer em determinados momentos.

**1. Componentes Utilizados**

| Componente   | Quantidade | Descrição                                          |
|--------------|------------|----------------------------------------------------|
| Arduino      | 1          | Modelo UNO |
| Protoboard   | 1          | Para montagem do circuito                          |
| LEDs         | 3          | Vermelho, amarelo e verde          |
| Buzzer       | 1          | Emite som de alerta                                |
| Resistores   | 3          | Um para cada LED                         |
| Fios jumper  | Vários     | Para as conexões entre componentes e Arduino       |

**2. Montagem do Circuito**

O circuito completo foi montado segundo a imagem a seguir (repare que o buzzer não está conectado).
<div style="text-align: center;">
    <img src="Assets/foto_4.jpeg" alt="Figura 1" width="50%">
</div>
Repare aqui que foram utilizados fios brancos para a saída dos LEDs e fios coloridos para a entrada. Foi utilizado um buzzer conectado diretamente no Arduino para indicar um sinal sonoro quando o LED vermelho acender. Foram utilizados resistores para evitar a queima dos LEDs.
<div style="text-align: center;">
    <img src="Assets/foto_1.jpeg" alt="Figura 2" width="20%" style="display: inline-block; margin: 0 10px;">
    <img src="Assets/foto_2.jpeg" alt="Figura 3" width="20%" style="display: inline-block; margin: 0 10px;">
    <img src="Assets/foto_3.jpeg" alt="Figura 4" width="20%" style="display: inline-block; margin: 0 10px;">
</div>

Os componentes foram conectados nas seguintes portas:
    - Porta digital 10: LED Vermelho
    - Porta digital 9: LED Amarelo
    - Porta digital 8: LED Verde
    - Porta digital 7: Buzzer

O sistema pode ser visto funcionando nos vídeos a seguir. O primeiro demonstra o buzzer apitando três vezes ao acender o LED verde, visando simular um sinal de pedestres incluindo pedestres com deficiência visual, e o segundo demonstra o semáforo piscando sequencialmente 6s no vermelho, 2s no amarelo, 4s no verde e 2s no amarelo novamente.

<div style="text-align: center;">
    <video width="320" height="240" controls>
        <source src="Assets/video_1.mp4" type="video/mp4">
    </video>
    <video width="320" height="240" controls>
        <source src="Assets/video_2.mp4" type="video/mp4">
    </video>
</div>

**3. Código do Arduino**

O código abaixo controla o protótipo do semáforo na IDE do Arduíno.
```c
// definir variáveis
int vermelho = 10;
int amarelo = 9;
int verde = 8;
int buzzer = 7;
 
void setup() {
  // definir pinos do Arduino
  pinMode(vermelho, OUTPUT);
  pinMode(amarelo, OUTPUT);
  pinMode(verde, OUTPUT);
  pinMode(buzzer, OUTPUT);
}
 
void loop() {
  // piscar vermelho por 6s
  digitalWrite(vermelho, HIGH);
  digitalWrite(amarelo, LOW);
  digitalWrite(verde, LOW);
  delay(6000);

  // piscar amarelo por 2s
  digitalWrite(vermelho, LOW);
  digitalWrite(amarelo, HIGH);
  digitalWrite(verde, LOW);
  delay(2000);

  // piscar verde por 2s
  digitalWrite(vermelho, LOW);
  digitalWrite(amarelo, LOW);
  digitalWrite(verde, HIGH);
  delay(2000);

  // ativar buzzer
  for (int i = 0; i < 3; i++) {
      tone(buzzer, 50, 30); // Beep com frequência de 50 Hz por 30 ms
      delay(300);            // Espera 300 ms entre os beeps
  }

  // adicionar tempo adicional no verde por mais 2 segundos
  delay(2000);

  // piscar amarelo por 2s
  digitalWrite(vermelho, LOW);
  digitalWrite(amarelo, HIGH);
  digitalWrite(verde, LOW);
  delay(2000);
}
```

