# Comparação de Métodos Clássicos e Híbrido Quântico-Clássico para o Cálculo de Energia Mínima do H₂

Repositório do Trabalho de Conclusão de Curso (TCC) em Engenharia Física — EEL USP.

Este projeto implementa e compara quatro métodos computacionais para o cálculo da 
curva de energia potencial da molécula de hidrogênio (H₂) em função da distância 
internuclear: Hartree-Fock (HF), Full Configuration Interaction (FCI), 
DFT/PBE (GGA) e o algoritmo híbrido quântico-clássico VQE (Variational Quantum 
Eigensolver), utilizando o ansatz Hardware-Efficient (HEA) e o otimizador Adam.

---

## Estrutura do Repositório
├── h2dist_GGA.ipynb          # Código principal — pipeline completo HF, FCI, VQE e DFT/PBE
├── diagrama_circuito.ipynb   # Geração do diagrama do circuito HEA via qml.draw_mpl
├── testehamiltoniano.ipynb   # Teste de construção do Hamiltoniano Jordan-Wigner
├── testevqe.ipynb            # Teste do circuito VQE e convergência do otimizador
├── testeambiente.ipynb       # Verificação das dependências e versões instaladas
├── circuito_hea.png          # Diagrama do circuito HEA (4 qubits, 2 camadas)
├── convergencia_teste.png    # Gráfico de convergência do VQE
├── README.md
└── dados/
└── resultados/
├── dft/                      # Dados DFT/PBE calculados via NWChem 7.2.2
├── h2_curva_energia_pbe.png  # Gráfico da curva de energia potencial
├── hamiltoniano_h2.png       # Gráfico dos termos de Pauli do Hamiltoniano
└── vqe_hea_convergencia_h2.png # Gráfico de convergência do VQE

---

## Métodos Implementados

| Método | Biblioteca | Descrição |
|---|---|---|
| Hartree-Fock (HF) | PySCF 2.13.0 | Método de campo médio, sem correlação eletrônica |
| Full CI (FCI) | PySCF 2.13.0 | Solução exata dentro da base STO-3G — referência |
| DFT/PBE | NWChem 7.2.2 | Funcional GGA sem parâmetros empíricos |
| VQE (HEA) | PennyLane 0.44.1 | Algoritmo híbrido quântico-clássico, 4 qubits, 2 camadas |

Todos os cálculos utilizam a base **STO-3G** para comparabilidade direta entre os métodos.

---

## Como Reproduzir os Resultados

Este repositório está configurado para execução direta no **GitHub Codespaces** — 
não é necessária nenhuma instalação local.

**1. Abrir o Codespace**
- Acesse o repositório no GitHub
- Clique em `Code → Codespaces → Create codespace on main`

**2. Executar o código principal**
- Abra o arquivo `h2dist_GGA.ipynb`
- Execute todas as células em ordem (`Run All`)
- Os resultados serão salvos automaticamente na pasta `dados/resultados/`

**3. Notebooks auxiliares (opcional)**
- `testeambiente.ipynb` — verificar se todas as dependências estão instaladas corretamente
- `testehamiltoniano.ipynb` — inspecionar os 15 termos do Hamiltoniano Jordan-Wigner para d = 0.74 Å
- `testevqe.ipynb` — acompanhar a convergência do VQE iteração a iteração
- `diagrama_circuito.ipynb` — regenerar o diagrama do circuito HEA

---

## Dependências

As bibliotecas necessárias já estão disponíveis no ambiente GitHub Codespaces 
configurado para este repositório:

| Biblioteca | Versão | Uso |
|---|---|---|
| Python | 3.12.3 | Linguagem base |
| PennyLane | 0.44.1 | VQE e simulação quântica |
| PySCF | 2.13.0 | HF e FCI |
| SciPy | 1.17.1 | Interpolação cúbica dos dados DFT |
| NumPy | 2.4 | Operações numéricas |
| Matplotlib | 3.10.9 | Visualização |

> Os cálculos DFT/PBE foram realizados externamente com **NWChem 7.2.2** 
> e os dados já estão incluídos na pasta `dados/resultados/dft/`.

---

## Parâmetros do VQE

| Parâmetro | Valor |
|---|---|
| Ansatz | Hardware-Efficient (HEA) |
| Número de qubits | 4 |
| Número de camadas | 2 |
| Número de parâmetros | 16 |
| Otimizador | Adam (α = 0.05) |
| Iterações | 200 |
| Semente aleatória | 42 |
| Mapeamento | Jordan-Wigner |
| Base orbital | STO-3G |

---

## Resultados Principais

| Método | d_eq (Å) | Erro máx. vs FCI (mHa) | Chemical accuracy |
|---|---|---|---|
| FCI | 0.740 | — | Referência |
| VQE | 0.740 | 0.0257 | ✓ |
| DFT/PBE | 0.750 | 34.9896 | ✗ |
| HF | 0.740 | 124.9859 | ✗ |

---

## Referências

- PERUZZO et al. *A variational eigenvalue solver on a photonic quantum processor.* 
  Nature Communications, 2014.
- KANDALA et al. *Hardware-efficient VQE for Small Molecules and Quantum Magnets.* 
  Nature, 2017.
- MCARDLE et al. *Quantum computational chemistry.* 
  Reviews of Modern Physics, 2020.
- DELGADO GRAN, A. *A brief overview of VQE.* PennyLane Demos, Xanadu.

---

## Autor

Estela Hasmann — Engenharia Física, EEL USP  
Orientador: Prof. Luiz Tadeu Fernandes Eleno — CompuTEEL  
Contato: [hasmann86@gmail.com]