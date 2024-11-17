# Pull Request - Projeto Maloca das iCoisas

## Descrição do Pull Request

### O que foi implementado:

- Implementação de um sistema de monitoramento de batimentos cardíacos com alerta via LEDs.
- Integração do sensor de pulso (PulseSensor) para leitura de frequência cardíaca.
- Configuração de LEDs (verde e vermelho) para indicar estado normal ou crítico.
- Simulação do sistema no Tinkercad com validação funcional.

### Contexto e Motivação:
- Necessidade de um sistema acessível para monitoramento cardíaco em tempo real como parte do contexto de IoT na saúde.
- Projeto visa demonstrar a viabilidade de integrar sensores e atuadores simples em soluções práticas de monitoramento biométrico.

## Testes Realizados

### Descrição dos Testes:
- Teste de Sensores: Validação da leitura do PulseSensor em tempo real no Monitor Serial.
- Teste de LEDs: Verificação das condições de alerta (LED verde para BPM normal, LED vermelho para BPM crítico).
- Teste de Código: Execução do código em Arduino IDE e simulação no Tinkercad para confirmação de funcionamento.


### Resultados dos Testes:
- Monitor Serial exibiu valores de BPM com precisão esperada dentro do intervalo simulado.
- LEDs acionaram corretamente conforme os valores de   BPM simulados:
  -    BPM entre 60-100: LED verde ligado.
  - BPM fora do intervalo: LED vermelho ligado.
- Simulação no Tinkercad apresentou comportamento consistente com o esperado.


## Checklist

- [✓ ] Código atende às normas do projeto e foi formatado de acordo com as diretrizes.
- [✓ ] Código foi testado e validado em ambiente de desenvolvimento com hardware real (Arduino, Raspberry Pi, ESP32) ou simulação (tinkercad).
- [✓ ] Documentação atualizada para refletir as mudanças realizadas.
- [✓ ] Código escrito e comentado em **C** ou **Python** de acordo com os padrões do projeto.
- [✓ ] Testes com sensores e atuadores específicos incluídos e detalhados na descrição dos testes.

## Tipo de Mudança

   - [ ] Correção de bug
- [ ✔] Nova funcionalidade
   - [ ] Alteração de funcionalidade existente
- [ ✓] Documentação

## Informações Adicionais

### Hardware Utilizado:
- Arduino Uno.
- PulseSensor (sensor de frequência cardíaca).
- LEDs (verde e vermelho) com resistores de 220Ω.

### Simulação Utilizado:
- Simulação do sistema no Tinkercad.
- Link da Simulação: https://www.tinkercad.com/things/diNXBp7jY2n-monitor-de-batimentos-cardiacos-com-alerta-via-led?sharecode=Eh0NAm455gc2cGZ-tbGXkeiGWD5VI6SkQIKg53SIBV0

### Observações:
- O sistema pode ser expandido com melhorias como integração Bluetooth para envio de dados para dispositivos móveis.
- Adição de armazenamento local para registrar históricos de BPM está em planejamento.

## Issue Relacionada


Closes #

---

**Nota:** Esse preenchimento detalhado demonstra a implementação e validação completa, ajudando a garantir uma revisão rápida e eficaz.
