Trabalho referente ao circuito PWM

Aluno.: Lucas Tatin
Professor: Rafael Rodrigues Barbosa

_________________________________________________________________________________

<h1>1. INTRODUÇÃO AO PWM<h1>

<p>É frequentemente utilizado para controlar dispositivos ou sistemas que requerem a variação de potência, como motores, lâmpadas de LED, fontes de alimentação e inversores. A sua versatilidade e eficiência tornam-no uma escolha popular em diversas aplicações.
É uma técnica essencial na eletrônica para controlar a potência entregue a dispositivos e sistemas, através da variação da largura dos pulsos em uma onda quadrada. Sua aplicação abrange uma ampla gama de equipamentos e proporciona controle preciso e eficiente.
<p>

_________________________________________________________________________________

<h1>2. COMPONENTES NECESSÁRIOS<h1>

<p>Arduino Nano<p>

<div align=center>
<img height="200em" src="./imagens/arduinoNano.png">
</div>

<p>L293D (Circuito integrado dedicado ao controle de pequenos motores DC)<p>

<div align=center>
<img height="200em" src="./imagens/l293d.png">
</div>

<p>Motor (Máquina de Corrente Contínua)<p>

<div align=center>
<img height="200em" src="./imagens/motor.png">
</div>

<p>Terminal GND<p>

<div align=center>
<img height="200em" src="./imagens/terminalGround.png">
</div>

<p>Osciloscópio<p>

<div align=center>
<img height="200em" src="./imagens/oscilos.png">
</div>

<p>Voltímetro<p>

<div align=center>
<img height="200em" src="./imagens/voltimetro.png">
</div>

<p>Resistor(es)<p>

<div align=center>
<img height="200em" src="./imagens/resistor.png">
</div>

<p>Bateria<p>

<div align=center>
<img height="200em" src="./imagens/bateria.png">
</div>

<p>Botão<p>

<div align=center>
<img height="200em" src="./imagens/botao.png">
</div>
_________________________________________________________________________________

<h1>3. ESQUEMÁTICO<h1>

<p>Segue anexo no schematics do projeto no formato PDF<p>

_________________________________________________________________________________

<h1>4. CÓDIGO FONTE<h1>

<style>
    .texto-roxo {
        color: purple;
    }
</style>


<p class="texto-roxo"

 #include Arduino H

#define BUTTON_PIN 2
#define PWM 9

int estado_botao = 0;
int pwm = 0;
int ultimo_estado_botao = 0;
unsigned long tempo_acionado = 0;
unsigned long tempo_delay = 50;

void setup() {
  pinMode(PWM, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {

  int leitura = digitalRead(BUTTON_PIN);

  if (leitura != ultimo_estado_botao) {
    ultimo_estado_botao = leitura;
    if (leitura == HIGH) {  
      tempo_acionado = millis();
    }
  }

  if (leitura == HIGH && ((millis() - tempo_acionado) > tempo_delay)) {
    pwm += 64;//pwm = pwm + 64
      if(pwm >255){
        pwm = 0;
      }
  }

  analogWrite(PWM, pwm);
  delay(50);
}</p>
_________________________________________________________________________________

<h1>5. INSTRUÇÕES DE MONTAGEM<h1>

<p>Pode ser visto também no anexo no schematics do projeto no formato PDF<p>
_________________________________________________________________________________

<h1>6. FUNCIONAMENTO DO PROJETO<h1>

<p>O sinal de saída do comparador é combinado com a onda portadora após passar pelo filtro. O resultado é uma forma de onda modulada por largura de pulso. A largura dos pulsos é controlada pelo sinal de controle do comparador. Quanto maior a largura do pulso, maior será a potência entregue ao dispositivo ou sistema controlado. Da mesma forma, uma largura de pulso menor resultará em uma potência mais baixa.

O ciclo de trabalho (duty cycle) é uma medida importante no funcionamento do circuito PWM. Ele representa a proporção de tempo em que o sinal está em nível alto (ligado) em relação ao período completo da onda portadora. O ciclo de trabalho é expresso como uma porcentagem, onde 0% significa que o sinal está sempre desligado, e 100% significa que o sinal está sempre ligado.

Ao variar o ciclo de trabalho (alterando a largura dos pulsos), é possível controlar a média de potência entregue ao dispositivo ou sistema. Essa técnica permite um controle preciso e eficiente da potência, possibilitando o ajuste contínuo da velocidade, brilho, tensão ou qualquer outra característica do dispositivo ou sistema controlado pelo circuito PWM.

Em resumo, o circuito PWM utiliza a modulação por largura de pulso para controlar a potência entregue a dispositivos ou sistemas. Ao variar a largura dos pulsos em uma onda portadora, é possível controlar a média de potência de forma precisa e eficiente.<p>

<div align=center>
<img height="200em" src="./imagens/funcionamento.png">
</div>
________________________________________________________________________________