========================================================
EDGE NOC AUTOMATION — ESTRUTURA OFICIAL PARA GITHUB
========================================================

OBJETIVO
--------
Este documento define:
- A estrutura correta do repositório
- Quais arquivos entram no GitHub
- Quais arquivos NÃO entram
- Como organizar pastas
- Como preparar para uso em outra máquina
- Padrão profissional para NOC / ambiente corporativo


========================================================
1) ESTRUTURA FINAL DO REPOSITÓRIO
========================================================

A estrutura abaixo é a que DEVE existir no GitHub:

edge-noc-automation/
│
├── app/
│   └── edge_noc_automation/
│       ├── main.py               # Aplicação principal (GUI + lógica)
│       ├── edge_controller.py    # Controle de janelas do Edge
│       ├── winapi.py             # WinAPI (teclado, mouse, hotkeys)
│       ├── config_store.py       # Persistência (config.json + links.txt)
│
├── scripts/
│   └── iniciar_edge_noc.bat      # Launcher por duplo clique
│
├── .gitignore                    # Arquivos ignorados pelo Git
├── README.md                     # Documentação completa
└── LICENSE                       # Licença do projeto (opcional)


========================================================
2) O QUE ENTRA NO GITHUB
========================================================

✅ DEVE ENTRAR NO REPOSITÓRIO:

- main.py
- edge_controller.py
- winapi.py
- config_store.py
- iniciar_edge_noc.bat
- README.md
- .gitignore
- LICENSE (se desejar)

✅ Esses arquivos são:
- Código-fonte
- Scripts de inicialização
- Documentação
- Configuração de versionamento


========================================================
3) O QUE NÃO ENTRA NO GITHUB
========================================================

❌ NUNCA versionar:

- config.json
- links.txt
- __pycache__/
- *.log
- *.exe
- dist/
- build/
- .venv/
- .idea/
- .vscode/

Esses arquivos são:
- Gerados em runtime
- Dependentes da máquina
- Dados operacionais do NOC


========================================================
4) CONTEÚDO DO .gitignore (COPIAR E COLAR)
========================================================

Criar o arquivo `.gitignore` na raiz do projeto com o conteúdo:

--------------------------------------------------------
__pycache__/
*.pyc
*.pyo

config.json
links.txt

build/
dist/

*.exe
*.log

.venv/
env/

.vscode/
.idea/

.DS_Store
Thumbs.db
--------------------------------------------------------


========================================================
5) CONTEÚDO DO ARQUIVO .BAT (PADRÃO OFICIAL)
========================================================

Local: scripts/iniciar_edge_noc.bat

--------------------------------------------------------
@echo off
REM ==========================================
REM Edge NOC Automation - Inicializador Oficial
REM ==========================================

REM Caminho relativo ao repositório
set PROJECT_DIR=%~dp0..\app\edge_noc_automation

REM Comando do Python (ajuste se necessário)
set PYTHON_CMD=python

cd /d "%PROJECT_DIR%"

%PYTHON_CMD% main.py

pause
--------------------------------------------------------

✅ Esse .bat:
- Funciona em qualquer máquina após clone
- Não depende de caminho fixo (C:\Tools, etc.)
- É portátil
- Ideal para GitHub


========================================================
6) COMO OUTRA MÁQUINA VAI USAR (PASSO A PASSO)
========================================================

1️⃣ Clonar o repositório:

git clone https://github.com/SEU_USUARIO/edge-noc-automation.git

2️⃣ Instalar Python (se não tiver):

winget install -e --id Python.Python.3.11

3️⃣ Entrar na pasta:

cd edge-noc-automation

4️⃣ Executar o launcher:

scripts\iniciar_edge_noc.bat

✅ Na primeira execução, o sistema criará:
- app/edge_noc_automation/config.json
- app/edge_noc_automation/links.txt


========================================================
7) ONDE FICAM OS ARQUIVOS DE OPERAÇÃO
========================================================

Após rodar pela primeira vez:

app/edge_noc_automation/
│
├── config.json   # Configurações globais e por link
└── links.txt     # URLs monitoradas

✅ Esses arquivos:
- NÃO entram no Git
- São específicos de cada máquina/NOC
- Podem ser editados via GUI ou manualmente


========================================================
8) BOAS PRÁTICAS PARA REPOSITÓRIO
========================================================

✅ Commits pequenos e descritivos
✅ Não versionar arquivos gerados
✅ README sempre atualizado
✅ Não rodar como administrador
✅ Evitar dependências externas
✅ Manter launcher simples (.bat)


========================================================
9) MOTIVO DESSA ESTRUTURA
========================================================

Essa estrutura foi escolhida porque:

- Facilita clonagem em outra máquina
- Evita conflitos de configuração
- Mantém código limpo
- É compatível com ambientes corporativos
- É padrão para automações NOC
- Não depende de empacotamento (.exe)


========================================================
10) STATUS DO PROJETO
========================================================

✔ Estrutura pronta para GitHub
✔ Documentação completa
✔ Execução via .bat validada
✔ Scroll específico para Zabbix resolvido
✔ Hotkeys globais funcionais
✔ Portável entre máquinas


========================================================
FIM DO DOCUMENTO
========================================================
