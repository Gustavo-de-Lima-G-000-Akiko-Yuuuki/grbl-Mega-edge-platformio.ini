# GRBL para Arduino Mega2560 com PlatformIO: Firmware Otimizado para Fresagem CNC
![Imagem de Propaganda](https://github.com/Gustavo-de-Lima-G-000-Akiko-Yuuuki/GPU-Selenium-web-search/blob/main/Image2.png?raw=true)

Este repositório contém uma versão otimizada do firmware GRBL, projetada especificamente para ser executada em placas Arduino Mega2560. Integrado com o PlatformIO, este projeto oferece uma solução de alto desempenho e baixo custo para controle de movimento em máquinas de fresagem CNC, garantindo precisão e estabilidade.

## Visão Geral

O GRBL é um firmware de código aberto amplamente reconhecido por sua eficiência no controle de movimento para CNC. Esta implementação foca na compatibilidade com o Arduino Mega2560, aproveitando seus recursos para oferecer uma experiência de fresagem CNC superior. O firmware é escrito em C altamente otimizado, garantindo temporização precisa e operação assíncrona, capaz de manter até 30kHz de pulsos de controle estáveis e sem jitter.

## Funcionalidades Principais

*   **Controle de Movimento Preciso:** Mantém pulsos de controle estáveis e sem jitter para movimentos suaves e precisos.
*   **Compatibilidade com G-code:** Aceita G-code padrão e foi rigorosamente testado com diversas ferramentas CAM, suportando arcos, círculos e movimento helicoidal.
*   **Gerenciamento de Aceleração com Look-ahead:** Antecipa até 24 movimentos futuros para planejar velocidades, proporcionando aceleração suave e curvas sem solavancos.
*   **Overrides em Tempo Real:** Permite a alteração imediata do estado de funcionamento da máquina (avanço, rápido, velocidade do fuso, etc.) com latência mínima, característica comum em máquinas industriais.
*   **Modo de Jogging Dedicado:** Comandos de jogging operam independentemente do parser de G-code, prevenindo alterações indesejadas no estado do parser e permitindo controle responsivo.
*   **Modo Laser:** Um modo específico para operações a laser, permitindo movimentos contínuos e escalonamento dinâmico da potência do laser com a velocidade para evitar cantos queimados.
*   **Modo de Suspensão:** Permite colocar o GRBL em um estado de baixa energia, desativando funções e drivers de passo, ideal para quando a máquina não está em uso.
*   **Melhorias na Interface:** Relatórios de status otimizados, feedback de erro/alarme aprimorado com códigos específicos e comandos em tempo real em Extended-ASCII para maior desempenho e facilidade de desenvolvimento de GUIs.
*   **Recursos OEM:** Inclui funcionalidades como estacionamento de porta de segurança e opções de configuração para fabricantes de equipamentos originais.

## Instalação e Configuração

Para utilizar este firmware, você pode baixar os arquivos `.hex` pré-compilados na aba `Release` do repositório ou compilar o projeto usando o PlatformIO.

### Pré-requisitos

*   Arduino Mega2560
*   PlatformIO (instalado como extensão no VSCode ou CLI)

### Compilação com PlatformIO

1.  **Clone o Repositório:**
    ```bash
    git clone https://github.com/Gustavo-de-Lima-G-000-Akiko-Yuuuki/grbl-Mega-edge-platformio.ini.git
    cd grbl-Mega-edge-platformio.ini
    ```
2.  **Abra no VSCode com PlatformIO:** Abra a pasta do projeto no VSCode. O PlatformIO detectará automaticamente o projeto.
3.  **Compile e Carregue:** Utilize as ferramentas do PlatformIO para compilar o firmware e carregá-lo para o seu Arduino Mega2560.

## Uso

Após carregar o firmware, você pode interagir com o GRBL através de qualquer software de controle CNC compatível com G-code. As melhorias na interface e os novos comandos em tempo real permitem um controle mais preciso e responsivo da sua máquina.

## Contribuição

Contribuições são bem-vindas! Se você tiver sugestões de melhorias, encontrar bugs ou quiser adicionar novas funcionalidades, sinta-se à vontade para abrir uma [issue](https://github.com/Gustavo-de-Lima-G-000-Akiko-Yuuuki/grbl-Mega-edge-platformio.ini/issues) ou enviar um [pull request](https://github.com/Gustavo-de-Lima-G-000-Akiko-Yuuuki/grbl-Mega-edge-platformio.ini/pulls).

## Licença

Este projeto é de código aberto e está distribuído sob a licença GPLv3. Consulte o arquivo `COPYING` para obter mais detalhes.
