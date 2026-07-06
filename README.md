# SEL0433 - Projeto 3
### Integrantes: 
* João Henrique Viana de Oliveira - 15462907
* Pedro Brandi Pereira - 15640990

Este projeto consiste na exploração de conceitos de comunicação serial e modulação por largura de pulso (PWM) por meio da programação de um microcontrolador de 32 bits. O sistema foi desenvolvido na linguagem C para a plataforma ESP32 DevKit e teve sua montagem, validação e execução de circuitos implementadas e testadas integralmente através do ambiente de simulação virtual Wokwi.

O objetivo primário do sistema divide-se em duas etapas de controle embarcado: a primeira atua no controle contínuo e independente da intensidade luminosa de um LED RGB de catodo comum via canais PWM, reportando os dados em tempo real via interface serial UART. A segunda etapa foca no acionamento de atuadores mecânicos, compreendendo o controle posicional manual de um servomotor a partir da leitura analógica de um potenciômetro pelo ADC da ESP32, evoluindo para o desenvolvimento de uma aplicação avançada de acionamento de motores utilizando bibliotecas nativas de controle, exibição de parâmetros em tempo real via display OLED em barramento I2C e integração com recursos adicionais de hardware/software.

A descrição técnica minuciosa de cada decisão de engenharia, a inicialização dos periféricos, a estruturação das tarefas e os cálculos de variação de duty cycle estão atribuídos diretamente nos arquivos de código-fonte presentes neste repositório em formato de comentários detalhados.

## Funcionalidades Apresentadas

* Modulação de iluminação RGB: O sistema gera sinais PWM independentes para os terminais vermelho, verde e azul de um LED RGB conectado através de resistores de 220 Ω. O duty cycle de cada canal varia continuamente de 0% a 100% em loop, aplicando taxas de incremento predefinidas e distintas para cada cor.

* Monitoramento de dados via Serial UART: O microcontrolador envia mensagens contínuas pela interface serial, configurada a uma taxa de transferência (baud rate) de 115200. Essas mensagens informam exatamente os valores de incremento e os duty cycles em tempo real aplicados em cada canal de cor.

* Posicionamento analógico de Servomotor: Realiza a leitura do sinal analógico de tensão gerado por um potenciômetro utilizando o conversor analógico-digital (ADC) da ESP32. O valor lido é processado e mapeado em valores de ângulo/largura de pulso, controlando de forma manual e progressiva o duty cycle (0 a 100%) e a posição física do servomotor.

* Acionamento customizado de Atuador: Controle avançado de parâmetros do sistema, como velocidade, sentido de rotação, posicionamento ou potência, modelado especificamente para um contexto de controle embarcado.

* Interface visual via Display OLED: Exibição gráfica e contínua dos parâmetros de funcionamento, estados operacionais e variáveis de controle do atuador por meio de um display OLED interligado via barramento I2C.

## Arquitetura Implementada

* Geração de PWM para iluminação (LEDC): Configuração dos canais da biblioteca nativa LED Control PWM (LEDC) operando com resolução fixa de 8 bits e frequência de sinal de 5 kHz, garantindo um controle suave e sem cintilação visível no LED RGB.

* Acionamento de Servomotores (ESP32 Servo): Utilização da biblioteca otimizada ESP32 Servo para o mapeamento dos pulsos de controle angular na primeira etapa do controle de motores, abstraindo a geração de frequências específicas de 50 Hz exigidas por padrão por esses atuadores.

* Controle Avançado de Motores (MCPWM): Emprego da biblioteca nativa Motor Control PWM (MCPWM) para o gerenciamento de precisão da aplicação principal de acionamento, aproveitando os blocos geradores de PWM dedicados de hardware da ESP32 para controlar os sinais de direção e velocidade aplicados.

* Barramento de Comunicação I2C e UART: Inicialização da interface serial UART0 a 115200 bps para envio de relatórios de depuração. Configuração dos pinos de clock e dados do hardware I2C para comunicação em alta velocidade e envio de buffers de escrita para o display OLED.

* Leitura Analógico-Digital (ADC): Uso do módulo ADC nativo para quantização da tensão de entrada do potenciômetro. Os valores brutos obtidos são traduzidos matematicamente em tempo de execução para determinar as frações de período ativo do sinal PWM aplicado ao atuador.

* Otimização de Hardware e Lógica de Incrementos: Estruturação de loops de repetição que gerenciam passos independentes por cor sem travar a execução das leituras analógicas ou a atualização do display I2C.

## Imagens de simulação 

## Resultados obtidos

O resultado obtido foi um sistema embarcado completo e funcional em ambiente de simulação virtual Wokwi. O microcontrolador foi capaz de gerenciar múltiplos canais de modulação PWM simultaneamente, sustentando o esmaecimento contínuo e independente de um LED RGB enquanto interagia dinamicamente com o usuário na variação de posição de um servomotor e na condução de um atuador mecânico customizado através da biblioteca MCPWM. O monitoramento em tempo real foi validado tanto pelo fluxo contínuo de dados transmitidos via serial UART quanto pelo retorno visual instantâneo projetado no display OLED via barramento I2C.

Tais resultados são satisfatórios e cumprem todos os objetivos esperados da prática.



