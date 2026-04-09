# painel_analitico_ti
Automação de painéis web para NOC utilizando Python + Microsoft Edge

# 📺 Edge NOC Automation
Automação de painéis web para NOC utilizando Python + Microsoft Edge

---

## 📌 Visão Geral

O **Edge NOC Automation** é um projeto desenvolvido em **Python** para automatizar a abertura, alternância e controle de páginas web em ambientes de **NOC / Monitoramento 24x7**, como:

- Zabbix
- ServiceNow
- Dashboards corporativos
- Portais internos

O sistema foi projetado para ser **simples, robusto e compatível com ambientes corporativos**, evitando dependências complexas como Selenium ou Playwright.

Principais características:
- Uma janela do Edge por link
- Alternância automática entre janelas
- Interface gráfica (GUI) para controle
- Atalhos globais de teclado
- Scroll automático específico para Zabbix
- Inicialização via arquivo `.bat`
- Totalmente baseado em WinAPI + Edge padrão

✅ Ideal para TVs, painéis e salas de monitoramento.

---

## ✅ Funcionalidades

### 🔁 Alternância automática
- Alterna entre janelas do Edge em intervalo configurável
- Cada URL é aberta em **uma janela independente**

### 🖥️ Interface Gráfica (GUI)
- Adicionar / editar / remover links
- Configurar opções por link
- Iniciar / parar o loop

### ⌨️ Atalhos Globais (Hotkeys)
Funcionam mesmo com a janela fora de foco.

| Função | Atalho |
|------|------|
| Pausar / Retomar | Ctrl + Alt + P |
| Liberar mouse | Ctrl + Alt + M |
| Próxima janela | Ctrl + Alt + N |
| Janela anterior | Ctrl + Alt + B |
| Zoom + | Ctrl + Alt + + |
| Zoom - | Ctrl + Alt + - |

⚠️ Os atalhos **não utilizam setas direcionais**, evitando conflito com drivers de vídeo (rotação de tela).

---

### 🔍 Zoom
- Implementado via **Ctrl + Scroll**
- Funciona em qualquer layout de teclado

---

### 📜 Scroll Automático (Zabbix)

O Zabbix utiliza **containers internos**, que não respondem corretamente a:
- Mouse wheel
- PageDown
- Home / End

✅ Solução aplicada (validada manualmente):

1. Ao ativar o link do Zabbix:
2. Envia **1 TAB** para focar o container correto
3. Executa scroll usando **seta ↓**
4. Respeita:
   - Quantidade de passos
   - Delay configurado na GUI

Essa abordagem é **robusta**, **determinística** e funciona sem DOM.

---

### 🌐 Compatibilidade com ServiceNow
- Corrige automaticamente `&amp;`
- Corrige double-encoding (`%253D → %3D`)
- Normaliza URLs para `nav_to.do?uri=...`
- Evita redirecionamento para `$pa_dashboard.do`
- Força navegação correta na primeira ativação

---

## 📁 Estrutura do Projeto
C:\EdgeNOC\
│
├── iniciar_edge_noc.bat
│
└── app\
    └── edge_noc_automation\
        ├── main.py
        ├── edge_controller.py
        ├── winapi.py
        ├── config_store.py
        ├── links.txt
        ├── config.json

---

## ⚙️ Requisitos

- Windows 10 ou Windows 11
- Microsoft Edge instalado
- Python 3.10 ou superior (recomendado 3.11)
- Permissão para executar arquivos `.bat`

---

## 🐍 Instalação do Python (em outra máquina)

Abra **PowerShell (usuário normal)** e execute:

```powershell
winget install -e --id Python.Python.3.11

**Verifique a instalação:**

python --version

---

## **📄 Arquivo .bat de Inicialização**

Criar o launcher
Crie um arquivo chamado:
iniciar_edge_noc.bat

**Conteúdo do arquivo:**

@echo off
REM ==============================
REM Edge NOC Automation - Launcher
REM ==============================

REM Ajuste o caminho conforme a instalação
set PROJECT_DIR=C:\Tools\edge_noc_automation

REM Se o Python estiver no PATH
set PYTHON_CMD=python

cd /d "%PROJECT_DIR%"

%PYTHON_CMD% main.py

pause

---

## **📜 Arquivos de Configuração**

links.txt

Contém apenas URLs
Uma URL por linha

Exemplo:

https://zabbix.empresa.com/zabbix.php?action=dashboard.view
https://yduqs.service-now.com/task_list.do?sysparm_query=...

---

## **config.json**

Criado automaticamente na primeira execução
Armazena:

Intervalo de alternância
Perfil do Edge
Opções por link (scroll, F5, etc.)

⚠️ Recomenda-se editar apenas através da GUI.

---

**## 🔄 Fluxo de Funcionamento**

O .bat executa python main.py
A GUI é exibida
O Edge é inicializado com about:blank
Cada URL abre em uma janela independente
O loop de alternância inicia
Ao ativar uma janela:

Primeira ativação → navegação forçada
Zabbix → TAB + seta ↓


Hotkeys ficam ativas globalmente

---

## **📌 Conclusão**
Este projeto foi desenvolvido com foco em:

Estabilidade
Simplicidade
Compatibilidade corporativa
Uso real em ambientes de NOC

A decisão de utilizar Python + arquivo .bat é intencional e evita problemas comuns de empacotamento.
