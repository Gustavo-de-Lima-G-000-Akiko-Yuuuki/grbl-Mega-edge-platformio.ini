# Firmware GRBL para Fresagem CNC

![Logo do GitHub](https://github.com/gnea/gnea-Media/blob/master/Grbl%20Logo/Grbl%20Logo%20250px.png?raw=true)

***
_Clique na aba `Release` para baixar arquivos `.hex` pré-compilados ou simplesmente [clique aqui](https://github.com/gnea/grbl-Mega/releases)_
***

O Grbl é uma alternativa de alto desempenho, baixo custo e sem compromissos ao controle de movimento baseado em porta paralela para fresagem CNC. Esta versão específica do Grbl foi projetada para rodar exclusivamente em um Arduino Mega2560.

O firmware do controlador é meticulosamente desenvolvido em C altamente otimizado, aproveitando todos os recursos inteligentes dos chips AVR para alcançar temporização precisa e operação assíncrona. Ele é capaz de manter até 30kHz de pulsos de controle estáveis e sem jitter, garantindo movimentos suaves e precisos da máquina.

O Grbl aceita G-code em conformidade com os padrões e foi rigorosamente testado com a saída de várias ferramentas CAM, demonstrando compatibilidade perfeita. Ele suporta totalmente arcos, círculos e movimento helicoidal, além de todos os outros comandos primários de G-code. Embora funções de macro, variáveis e a maioria dos ciclos fixos não sejam diretamente suportados, geralmente é recomendado que as Interfaces Gráficas de Usuário (GUIs) lidem com a tradução destes para G-code padrão para desempenho e flexibilidade ideais.

Uma característica chave do Grbl é seu gerenciamento abrangente de aceleração, que inclui capacidades de antecipação (look-ahead). O controlador pode antecipar até 24 movimentos futuros, planejando suas velocidades com antecedência para fornecer aceleração excepcionalmente suave e curvas sem solavancos. Este planejamento de movimento inteligente melhora significativamente a qualidade e a eficiência das operações de usinagem.

*   **Licenciamento**: O Grbl é um software livre, distribuído sob a licença GPLv3.

*   Para informações mais detalhadas e ajuda, por favor, consulte nossas **[páginas da Wiki!](https://github.com/gnea/grbl/wiki)** Nós encorajamos contribuições da comunidade para manter as informações atualizadas e precisas. Se você notar conteúdo desatualizado, por favor, considere editá-lo ou notificar nossa comunidade. Sua ajuda é muito apreciada!

*   **Desenvolvedor Principal**: Sungeun "Sonny" Jeon, Ph.D. (EUA), também conhecido como @chamnit.

*   **Fundação**: Construído sobre o excelente firmware Grbl v0.6 (2011), originalmente de autoria de Simen Svale Skogsrud (Noruega).

***

### Apoiadores Oficiais do Projeto Grbl CNC
![Apoiadores Oficiais](https://github.com/gnea/gnea-Media/blob/master/Contributors.png?raw=true)

***

## Resumo das Atualizações do Grbl v1.1

O Grbl v1.1 introduz melhorias significativas e novos recursos, aprimorando o desempenho, a experiência do usuário e a compatibilidade. Abaixo está um resumo das principais atualizações:

-   **Limpeza e Restauração da EEPROM**: Uma mudança crucial na v1.1 envolve a limpeza e restauração da sua EEPROM com novas configurações. Isso se deve principalmente à integração de duas novas configurações `$` de velocidade do fuso, garantindo a configuração e funcionalidade adequadas.

-   **Overrides em Tempo Real**: Este novo e poderoso recurso permite a alteração imediata do estado de funcionamento da máquina, incluindo controles de avanço, rápido, velocidade do fuso, parada do fuso e alternância de refrigerante. Ao contrário de muitos sistemas CNC de hobby que sofrem com atrasos significativos, o Grbl executa esses overrides em tempo real, em dezenas de milissegundos. Essa capacidade, comumente encontrada apenas em máquinas industriais, é inestimável para otimizar velocidades e avanços durante um trabalho em andamento.

-   **Modo de Jogging**: Os novos comandos de jogging operam independentemente do parser de G-code. Este design impede que o estado do parser seja alterado inadvertidamente, o que poderia levar a possíveis falhas se não fosse restaurado corretamente. A documentação abrangente é fornecida, detalhando sua funcionalidade e como pode ser utilizada para controle de máquina de baixa latência e responsivo através de dispositivos como joysticks ou seletores rotativos.

-   **Modo Laser**: Um modo "laser" dedicado permite que o Grbl se mova continuamente através de comandos G1, G2 e G3 consecutivos, mesmo com alterações na velocidade do fuso. Quando o modo "laser" está desativado, o Grbl fará uma pausa para garantir que o fuso atinja a velocidade correta. Os overrides de velocidade do fuso também funcionam no modo laser, permitindo ajustes de potência do laser em tempo real durante um trabalho. Você pode alternar entre os modos "laser" e "normal" através de uma configuração `$`.

    -   **Escalonamento Dinâmico da Potência do Laser com a Velocidade**: Para máquinas com capacidades de aceleração mais baixas, o Grbl dimensiona inteligentemente a potência do laser com base em sua velocidade de deslocamento. Isso evita cantos queimados quando a máquina CNC precisa fazer uma curva. Este recurso é ativado pelo comando `M4` do fuso (sentido anti-horário) quando o modo laser está habilitado.

-   **Modo de Suspensão**: O Grbl agora pode ser colocado em um estado de "suspensão" usando o comando `$SLP`. Este comando desativa todas as funções, incluindo os drivers de passo, fornecendo uma maneira conveniente de desligar a máquina automaticamente quando não supervisionada. Apenas um reset pode sair do estado de suspensão.

-   **Melhorias Significativas na Interface**: A interface foi refinada para aumentar o desempenho geral, fornecer mais dados em tempo real e simplificar a manutenção e o desenvolvimento de GUIs. Essas melhorias são baseadas no feedback direto de vários desenvolvedores de GUI e em extensos testes de desempenho em bancada. *NOTA: As GUIs precisarão atualizar seu código para garantir a compatibilidade com a v1.1 e versões posteriores.*

    -   **Novos Relatórios de Status**: Para acomodar dados de override adicionais, os relatórios de status foram otimizados para incluir mais informações, mantendo-se menores que as versões anteriores. A documentação detalha as mudanças.
    -   **Feedback de Erro/Alarme Aprimorado**: Todas as mensagens de erro e alarme do Grbl agora incluem um código específico. Cada código está vinculado a um problema particular, fornecendo aos usuários informações precisas sobre os problemas sem a necessidade de adivinhação. A documentação e um arquivo CSV de fácil análise estão incluídos no repositório.
    -   **Comandos em Tempo Real em Extended-ASCII**: Todos os overrides e futuros comandos em tempo real são definidos no espaço de caracteres extended-ASCII. Embora não seja facilmente digitável em um teclado padrão, este design evita comandos acidentais de arquivos de G-code que contenham esses caracteres e oferece amplo espaço para expansão futura.
    -   **Prefixos de Mensagem**: Cada tipo de mensagem do Grbl agora possui um prefixo exclusivo. Isso permite que as GUIs identifiquem imediatamente o tipo de mensagem e a analisem de acordo, eliminando a necessidade de interpretação dependente do contexto, que anteriormente complicava o desenvolvimento da GUI.

-   **Novos Recursos Específicos para OEM**: Esta versão inclui novos recursos adaptados para Fabricantes de Equipamentos Originais (OEMs), como estacionamento de porta de segurança, uma opção de compilação de arquivo de configuração único, restrições e controles de restauração da EEPROM e a capacidade de armazenar informações de dados do produto.

-   **Movimento de Estacionamento da Porta de Segurança**: Uma nova opção de compilação permite o estacionamento da porta de segurança. Quando ativado, o Grbl irá retrair, desativar o fuso/refrigerante e estacionar perto da posição Z-max. Ao retomar, ele reverterá essas ações e continuará o programa. Este recurso é altamente configurável, permitindo mais de um movimento de estacionamento. Consulte `config.h` para configurações detalhadas.

-   **Novas Configurações `$` do Grbl para RPM do Fuso**: Novas configurações `$` para RPM máximo e mínimo do fuso permitem o ajuste fino da saída PWM para corresponder com mais precisão ao RPM real do fuso. Se o RPM máximo for definido como zero ou menor que o RPM mínimo, o pino PWM D11 funcionará como uma simples saída de habilitação/desabilitação.

-   **Comportamento Atualizado do G28 e G30**: O comportamento do G28 e G30 foi atualizado para se alinhar com a descrição do G-code do LinuxCNC, diferindo do NIST. Essencialmente, se um movimento intermediário for especificado, apenas os eixos especificados se moverão para as coordenadas armazenadas, em vez de todos os eixos como nas versões anteriores.

-   **Correções de Bugs e Refatoração**: Inúmeras pequenas correções de bugs e uma extensa refatoração de código foram implementadas para aumentar a eficiência e a flexibilidade em todo o firmware.

```
Lista de Códigos G Suportados no Grbl v1.1:
  - Comandos Não-Modais: G4, G10L2, G10L20, G28, G30, G28.1, G30.1, G53, G92, G92.1
  - Modos de Movimento: G0, G1, G2, G3, G38.2, G38.3, G38.4, G38.5, G80
  - Modos de Taxa de Avanço: G93, G94
  - Modos de Unidade: G20, G21
  - Modos de Distância: G90, G91
  - Modos de Distância IJK do Arco: G91.1
  - Modos de Seleção de Plano: G17, G18, G19
  - Modos de Compensação de Comprimento da Ferramenta: G43.1, G49
  - Modos de Compensação de Corte: G40
  - Modos de Sistema de Coordenadas: G54, G55, G56, G57, G58, G59
  - Modos de Controle: G61
  - Fluxo do Programa: M0, M1, M2, M30*
  - Controle de Refrigerante: M7*, M8, M9
  - Controle do Fuso: M3, M4, M5
  - Palavras Válidas Sem Comando: F, I, J, K, L, N, P, R, S, T, X, Y, Z
```

-------------
O Grbl é um projeto de código aberto, impulsionado pela dedicação de nossos intrépidos administradores e usuários altruístas. Se você deseja contribuir, todos os lucros serão utilizados para financiar hardware de suporte e equipamentos de teste. Obrigado pelo seu apoio!

[![Doar](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CUGXJHXA36BYW)





# Integração do PlatformIO com o GRBL

Esta seção detalha como o PlatformIO pode ser utilizado para compilar e carregar o firmware GRBL, destacando as vantagens e desvantagens desta abordagem.

## Por que usar o PlatformIO com o GRBL?

O PlatformIO é um ecossistema de código aberto para desenvolvimento embarcado que oferece uma alternativa robusta e flexível ao IDE do Arduino. Para projetos como o GRBL, que se beneficiam de controle de versão, gerenciamento de dependências e automação de compilação, o PlatformIO pode ser uma ferramenta poderosa.

## Configurando um Projeto PlatformIO para o GRBL

Para começar, você precisará ter o CLI (Interface de Linha de Comando) do PlatformIO ou a extensão do PlatformIO para o VS Code instalados.

### 1. Crie um Novo Projeto PlatformIO

Você pode iniciar um novo projeto PlatformIO e configurá-lo para o Arduino Mega 2560 (ou sua placa específica para o GRBL):

```bash
platformio project init --board megaatmega2560
```

Este comando criará uma estrutura de diretórios básica para o seu projeto.

### 2. Adicione o Código Fonte do GRBL

Copie os arquivos de origem do GRBL (normalmente encontrados na pasta `grbl` ou `grbl-mega` do repositório oficial) para a pasta `src` do seu projeto PlatformIO. Certifique-se de que todos os arquivos `.c`, `.h` e a estrutura de diretórios necessária estão incluídos.

### 3. Configure o `platformio.ini`

O arquivo `platformio.ini` é a configuração central do seu projeto PlatformIO. Aqui está um exemplo de como ele pode ser configurado para o GRBL:

```ini
[env:megaatmega2560]
platform = atmelavr
board = megaatmega2560
framework = arduino

; Caminho para os arquivos de origem do GRBL
; Certifique-se de que a pasta 'grbl' (ou onde quer que seus arquivos GRBL estejam) está dentro de 'src'
build_src_filter = +<*>

; Incluir diretórios de cabeçalho do GRBL
build_flags = -I src/grbl

; Opções do monitor serial (ajuste a porta e a velocidade conforme necessário)
monitor_speed = 115200
monitor_port = /dev/ttyUSB0 ; ou COMx no Windows

; Opções de upload (ajuste a porta conforme necessário)
upload_port = /dev/ttyUSB0 ; ou COMx no Windows

; Para o GRBL, você pode precisar de algumas definições de compilação específicas
; Exemplo: definir a frequência do cristal, se não for o padrão
; build_flags = -D F_CPU=16000000UL

; Se você tiver um arquivo config.h personalizado, certifique-se de que ele seja incluído
; build_flags = -I src/grbl -D GRBL_CUSTOM_CONFIG_H
```

**Notas:**
*   Ajuste `board` para a sua placa específica (ex: `uno`, `nanoatmega328`).
*   `build_src_filter` e `build_flags` são cruciais para que o PlatformIO localize os arquivos do GRBL e seus cabeçalhos.
*   As portas `monitor_port` e `upload_port` devem ser ajustadas para a porta serial correta do seu Arduino.

### 4. Compile e Carregue

Com o `platformio.ini` configurado, você pode compilar e carregar o GRBL para o seu Arduino usando os seguintes comandos:

```bash
platformio run
```

Para apenas compilar:

```bash
platformio run -t build
```

Para apenas carregar:

```bash
platformio run -t upload
```

## Pontos Fortes de Usar o PlatformIO com o GRBL

*   **Gerenciamento de Dependências:** O PlatformIO simplifica o gerenciamento de bibliotecas externas. Embora o GRBL tenha poucas dependências externas, este recurso é altamente benéfico para outros projetos.
*   **Ambiente de Desenvolvimento Unificado:** Suporta múltiplas plataformas e frameworks, fornecendo um ambiente de desenvolvimento consistente para vários projetos embarcados.
*   **Automação de Compilação:** A compilação e o upload por linha de comando são ideais para fluxos de trabalho de integração contínua e testes automatizados.
*   **Integração com o VS Code:** A extensão do VS Code oferece um IDE abrangente com recursos como autocompletar, depuração e outras funcionalidades avançadas.
*   **Controle de Versão:** Facilita o uso de sistemas de controle de versão como o Git, permitindo um gerenciamento mais eficaz de suas modificações no GRBL.
*   **Portabilidade:** Projetos do PlatformIO são mais portáteis entre diferentes sistemas operacionais e ambientes de desenvolvimento.

## Pontos Fracos de Usar o PlatformIO com o GRBL

*   **Curva de Aprendizagem:** Para usuários acostumados apenas com o IDE do Arduino, o PlatformIO pode apresentar uma curva de aprendizado inicial mais acentuada devido à sua flexibilidade e opções de configuração.
*   **Configuração Inicial:** Configurar o `platformio.ini` pode ser um tanto complexo no início, especialmente para projetos que não seguem a estrutura padrão do PlatformIO, como o GRBL.
*   **Depuração:** Embora o PlatformIO suporte depuração, configurá-lo para microcontroladores AVR pode ser mais complicado e pode exigir hardware adicional (ex: um programador JTAG/SWD).
*   **Sobrecarga do Projeto:** Para projetos muito simples, a sobrecarga de um projeto PlatformIO pode parecer excessiva em comparação com a simplicidade do IDE do Arduino.

## Conclusão

Utilizar o PlatformIO para o desenvolvimento do firmware GRBL oferece vantagens significativas em termos de automação, gerenciamento de projetos e integração com ferramentas modernas. Embora exija uma configuração inicial mais detalhada, os benefícios a longo prazo para o desenvolvimento e manutenção do firmware superam os desafios, especialmente para usuários que buscam um ambiente de desenvolvimento mais profissional e flexível.





## Instalação do JRE-Flip-Installer-3.4.7.112 para Arduino

Para utilizar o GRBL com o PlatformIO, é necessário instalar o JRE-Flip-Installer-3.4.7.112, que é um componente essencial para a comunicação com o Arduino. Siga os passos abaixo para realizar a instalação:

1.  **Baixe o JRE-Flip-Installer-3.4.7.112**: Acesse o link de download fornecido e baixe o instalador para o seu sistema operacional. Certifique-se de baixar a versão correta para o seu sistema (Windows, macOS, Linux).

    [Link para Download do JRE-Flip-Installer-3.4.7.112](https://www.microchip.com/developmenttools/ProductDetails/PIC-FLIP)

2.  **Execute o Instalador**: Após o download, execute o arquivo instalador e siga as instruções na tela para concluir a instalação. É recomendável aceitar as configurações padrão, a menos que você tenha necessidades específicas.

3.  **Verifique a Instalaçã
(Content truncated due to size limit. Use page ranges or line ranges to read remaining content)


ao vivo
