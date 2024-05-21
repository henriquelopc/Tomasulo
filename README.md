# Simulador de Tomasulo

Este repositório contém uma implementação em C++ do algoritmo de Tomasulo, utilizado para o escalonamento dinâmico de instruções em processadores superescalares.

## Visão Geral

O simulador permite a execução e visualização passo a passo das instruções, gerenciando as unidades de reserva, buffers de carga/armazenamento e estado dos registradores. A saída é exibida em uma interface de console, proporcionando uma visão clara do estado do processador em cada ciclo de execução.

## Pseudocódigo

### Função Simulate()
pseudo
short currentCycleNumber = 0;
while (there is an instruction remaining) {
    printInformationOnScreen();
    waitForUserToPressAKey();
    currentCycleNumber++;
    issueInstruction();
    executeInstructions();
    writeBackInstructions();
}


### Funções Utilizadas pela Função Simulate()

#### issueInstruction()
pseudo
if (Required ReservationStations / Buffers are Busy) {
    return; // não emite a instrução atual devido a um hazard estrutural
} else {
    1. Leia os valores dos registradores de origem Rs e Rt nos campos Vj e Vk, respectivamente.
    2. Se algum registrador de origem não estiver disponível, escreva o nome da estação de reserva/buffer que produzirá o resultado no Qj/Qk (tratamento de hazard de dependência de dados - RAW).
    3. Na tabela de status do registrador, registre que esta estação de reserva/buffer escreverá o resultado no registrador de destino Rd.
    4. Marque a estação de reserva/buffer como ocupada.
    5. Defina IssuedInstruction.issued = currentCycleNumber.
    6. currentInstructionToBeIssued++; (Essa variável inteira é o contador de instruções)
}


#### executeInstructions()
pseudo
for-each issued Instruction {
    1. Se todos os valores dos registradores de origem estiverem disponíveis, execute a instrução (remainingExecutionCycles--); caso contrário, continue para a próxima iteração do loop.
    2. Se este for o primeiro ciclo de execução da instrução, defina Instruction.ExecutionStartedOn = currentCycleNumber.
    3. Se este for o último ciclo de execução da instrução, defina Instruction.ExecutionFinishedOn = currentCycleNumber.
}


#### writeBackInstructions()
pseudo
for-each issued Instruction {
    1. Se a instrução completou seus ciclos de execução (Instruction.remainingExecutionCycles = 0), vá para a linha 2, caso contrário, continue para a próxima iteração do loop.
    2. Defina Instruction.writeBack = currentCycleNumber.
    3. Transmita os resultados para as estações de reserva/buffers dependentes.
    4. Marque a estação de reserva/buffer como livre.
}


## Funcionalidades

1. *Conjunto de Instruções Flexível*: As instruções podem ocorrer em qualquer ordem, sem limitação no número de instruções que podem ser executadas pelo simulador.
2. *Configuração Personalizável*: É possível aumentar ou diminuir o número de buffers e estações de reserva.
3. *Ciclos de Execução Configuráveis*: O número de ciclos que cada tipo de instrução leva em sua fase de execução pode ser especificado.
4. *Registradores Variáveis*: O número de registradores pode ser ajustado conforme necessário.

## Ferramentas Utilizadas

1. *Diagrama de Classes*: NClass.
2. *Programação*: C++.
3. *IDE*: Visual Studio 2017.
4. *Documentação*: Microsoft Word.

## Como Usar

1. Compile o código-fonte usando um compilador C++ compatível.
2. Certifique-se de que o arquivo de entrada "source.txt" esteja presente no diretório do executável.
3. Execute o programa resultante.
4. Siga as instruções na tela para avançar ciclo a ciclo na simulação.
5. Observe a saída no console para visualizar o estado do processador.
   
## Integrantes:
- Erton Leite
- Henrique Lourenço
- Pedro Kreuzer
- João Vitor Reis
   

