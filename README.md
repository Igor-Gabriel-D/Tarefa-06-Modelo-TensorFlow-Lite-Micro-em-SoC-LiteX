# TensorFlow Lite Micro em SoC LiteX

Nesta tarefa eu implementei um sistema capaz de rodar inferência TinyML usando um processador softcore VexRiscv dentro de uma FPGA ColorLight i9. A ideia foi usar o modelo Hello World do TensorFlow Lite Micro, aquele que aproxima uma função seno, e aproveitar a saída para controlar uma barra de 8 LEDs, criando um efeito visual proporcional ao valor previsto pela rede neural.

## Visão Geral do Sistema

O projeto é baseado em um SoC gerado com o LiteX, que inclui CPU, memória e periféricos de I/O. No firmware, escrito em C++, eu carrego o runtime do TFLM e executo o modelo repetidamente dentro do loop principal.

### Diagrama de Blocos
```mermaid
graph TD
    A[VexRiscv CPU] --> B[SRAM/SDRAM]
    B -->|Armazena| C[Firmware + Modelo TFLM]
    A -->|Bus| D[GPIO Controller]
    D -->|Sinal Digital| E[Barra de 8 LEDs]
    
    subgraph "FPGA ColorLight i9"
    A
    B
    D
    end
    
    subgraph "Interface Externa"
    E
    end

```
