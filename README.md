# 🖥️ Projeto Processador MIPS — Arquitetura de Computadores

Implementação de um processador MIPS monociclo simplificado utilizando o simulador de circuitos digitais **Logisim**. O projeto abrange o datapath completo com suporte a instruções do tipo R, I e J, memória de instruções (ROM), memória de dados (RAM), banco de registradores, ULA com múltiplas operações e unidades de controle.

---

## 👥 Integrantes

| Nome |
|------|
| Arthur Benevides |
| Juan Haddad |
| Guilherme Teixeira |
| Murillo Ando |
| Guilherme Peixirile |

---

## 📁 Estrutura do Projeto

```
mips.circ                         # Arquivo principal do circuito Logisim
Documentacao_Tecnica_MIPS.docx    # Documentação técnica detalhada
README.md                         # Este arquivo
```

---

## 🏗️ Arquitetura — Módulos

O processador é dividido em **6 circuitos** dentro do arquivo `.circ`:

| Módulo | Nome no Logisim | Função |
|--------|----------------|--------|
| **main** | `main` | Integração geral do datapath, RAM, muxes e lógica de PC |
| **Parte 1** | `Contador PC - Parte 1` | Program Counter, busca de instrução na ROM |
| **Parte 2** | `Banco de registradores - Parte 2` | 8 registradores de 32 bits com leitura/escrita |
| **Parte 3** | `ULA - Parte 3` | Unidade Lógica e Aritmética (ADD, SUB, MUL, DIV, SLL, SRL, CMP, NEG) |
| **Parte 4a** | `Unidade de controle - Parte 4` | Decodificador de opcode → sinais de controle |
| **Parte 4b** | `Controle ULA - Parte 4` | Tradução de ALUOp + funct → ULACtrl |

---

## ▶️ Instruções para Execução

### Pré-requisitos

- [**Logisim 2.7.1**](http://www.cburch.com/logisim/) instalado (versão recomendada para compatibilidade com o arquivo `.circ`)
- Java Runtime Environment (JRE) 8 ou superior

### Passos para executar

1. **Abrir o arquivo:**
   - Inicie o Logisim
   - Vá em `File → Open` e selecione o arquivo `mips.circ`

2. **Navegar para o circuito principal:**
   - No painel esquerdo (explorador de circuitos), clique duas vezes em **`main`** para abri-lo

3. **Carregar o programa na ROM:**
   - Clique com o botão direito sobre o componente **ROM** dentro do módulo `Contador PC - Parte 1`
   - Selecione `Edit Contents` e insira as instruções em hexadecimal (uma por linha)

4. **Inicializar o simulador:**
   - Vá em `Simulate → Simulation Enabled` (ou pressione `Ctrl+E`) para ativar a simulação
   - Pressione o botão **ClearMain** (ou use o pino de Clear) para resetar o PC para 0

5. **Executar:**
   - **Passo a passo:** Pressione `Ctrl+T` para avançar um tick de clock por vez
   - **Execução contínua:** Vá em `Simulate → Auto-Tick Enabled` (ou `Ctrl+K`) e ajuste a frequência em `Simulate → Auto-Tick Frequency`
   - **Reset:** Clique no pino `ClearMain` para reiniciar a execução

6. **Observar os resultados:**
   - Use a ferramenta **Poke** (mão) para inspecionar valores nos fios
   - Os valores dos registradores podem ser observados dentro do módulo `Banco de registradores - Parte 2`
   - O resultado da ULA e os sinais de controle são visíveis no módulo `main` via Tunnels

### Atalhos úteis no Logisim

| Ação | Atalho |
|------|--------|
| Ativar/desativar simulação | `Ctrl+E` |
| Avançar um tick | `Ctrl+T` |
| Auto-tick (execução contínua) | `Ctrl+K` |
| Resetar estado dos componentes | `Ctrl+R` |
| Ferramenta de inspeção (Poke) | `Ctrl+M` |

---

## 📄 Documentação Técnica

Consulte o arquivo **`Documentacao_MIPS_Detalhada.docx`** para:

- Diagrama de blocos detalhado da arquitetura
- Descrição de cada módulo e seus componentes internos
- Tabela de sinais de controle por instrução
- Conjunto de instruções suportado (tipo R, I e J)
- Decisões de projeto e justificativas técnicas

---

## ⚙️ Instruções Suportadas

| Instrução | Tipo | Operação |
|-----------|------|----------|
| `ADD rd, rs, rt` | R | `rd = rs + rt` |
| `SUB rd, rs, rt` | R | `rd = rs - rt` |
| `MUL rd, rs, rt` | R | `rd = rs * rt` |
| `DIV rd, rs, rt` | R | `rd = rs / rt` |
| `SLL rd, rt, shamt` | R | `rd = rt << shamt` |
| `SRL rd, rt, shamt` | R | `rd = rt >> shamt` |
| `LW rt, imm(rs)` | I | `rt = Mem[rs + imm]` |
| `SW rt, imm(rs)` | I | `Mem[rs + imm] = rt` |
| `BEQ rs, rt, offset` | I | `if rs==rt: PC += offset<<2` |
| `ADDI rt, rs, imm` | I | `rt = rs + imm` |
| `J target` | J | `PC = target<<2` |
