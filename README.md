# Simulador QNodeOS — Arquitetura de Sistemas Operacionais para Redes Quânticas

Simulador visual e interativo inspirado na arquitetura do **QNodeOS** (*Delle Donne et al., Nature, 2025*), o primeiro sistema operacional totalmente programável projetado para executar aplicações distribuídas em nós de redes quânticas.

Este projeto foi desenvolvido como prova de conceito prática para acompanhar um artigo acadêmico da disciplina de **Sistemas Operacionais** (Universidade Federal do Ceará — Campus Sobral), mapeando os conceitos clássicos da obra *Sistemas Operacionais Modernos* (Andrew S. Tanenbaum) para o paradigma da computação quântica em rede[cite: 1, 2].

---

## Funcionalidades e Conceitos Simulados

O simulador emula em tempo real o comportamento de um nó quântico dividido entre domínio clássico (**CNPU**) e domínio quântico (**QNPU / QDevice**)[cite: 2]:

* **Processos Híbridos e Estados Estendidos:** Execução de aplicações compostas por código clássico e instruções quânticas (`NetQASM`), introduzindo o estado **Aguardando Emaranhamento** (*Waiting-for-Entanglement*) além dos estados clássicos (*Pronto, Executando, Bloqueado*)[cite: 2, 3].
* **Escalonamento Não-Preemptivo:** Implementação de fila com prioridade máxima para o **Processo de Rede (Kernel)** e política **FCFS** (*First-Come, First-Served*) sem preempção para processos de usuário, evitando perda de coerência durante trocas de contexto[cite: 3].
* **Gerenciamento de Memória Quântica (QMMU):** Tradução dinâmica entre *qubits virtuais* e *qubits físicos*, com monitoramento contínuo do tempo de coerência ($T_1 / T_2$)[cite: 3].
* **Prevenção de Deadlocks (Watchdog $T_{coh}$):** Demonstração prática de como a expiração do tempo de coerência força a preempção temporal e libera qubits retidos, quebrando condições de *posse e espera* (hold-and-wait).
* **Entrada/Saída Híbrida (E/S):** Separação entre canal clássico (**TCP/IP**) para troca de bits de medição e canal óptico quântico (**ER Sockets**) para geração de pares emaranhados[cite: 4].
* **Agnosticismo de Hardware (Virtualização/HAL):** Alternância em tempo real da camada `QDriver` entre **Centros de Vacância em Diamante (NV Centers)** e **Processadores de Íons Aprisionados**[cite: 2, 4].
* **Segurança Física e Teorema da Não-Clonagem:**
  * Simulação de interceptação no canal óptico (*Eavesdropper / Eve*), detectando o colapso do estado quântico e abortando a sessão[cite: 4].
  * Bloqueio físico de operações de *swapping* para disco rígido, ilustrando a impossibilidade de clonar estados quânticos desconhecidos[cite: 3].

---

## Estrutura do Projeto

* `simulador_qnodeos.html` — Interface web interativa completa com visualização da QMMU, barras de decaimento de coerência ($T_{coh}$), controle de processos, injeção de falhas e console de logs do kernel.
* `simulador_qnodeos.py` — Versão em linha de comando (CLI) desenvolvida em Python puro (`asyncio`) para simulação de eventos discretos no terminal.

---

## Como Executar

### Versão Interativa (Web)
Não requer instalação de dependências ou servidor:
1. Baixe ou clone este repositório:
   ```bash
   git clone [https://github.com/SEU-USUARIO/simulador-qnodeos.git](https://github.com/SEU-USUARIO/simulador-qnodeos.git)
