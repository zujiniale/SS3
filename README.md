# SuperSistema — Aplicação Java com Login e Banco de Dados

## 📋 Descrição
Sistema de login em Java com interface gráfica Swing que se conecta a um banco de dados MySQL em nuvem para validar credenciais de usuários em tempo real. Após o login, disponibiliza o módulo completo de **Gestão de Usuários** com listagem, inclusão, edição e exclusão.

## ✨ Funcionalidades
- ✓ Interface gráfica moderna com Swing
- ✓ Login com validação em banco de dados MySQL
- ✓ Seleção de empresa/filial no login
- ✓ Menu dinâmico que aparece apenas após login
- ✓ Logout com confirmação
- ✓ Exibição do nome do usuário logado
- ✓ Logo como fundo da aplicação
- ✓ **Menu Usuários** — módulo separado de gestão de usuários (Usuários > Gestão de Usuários)
- ✓ **Listagem de Usuários** em grid com busca e atualização
- ✓ **Inclusão de Usuários** via formulário modal
- ✓ **Edição de Usuários** — botão EDITAR ou duplo clique na linha
- ✓ **Exclusão de Usuários** com confirmação antes de deletar
- ✓ **Atualizar listagem** sem fechar a tela
- ✓ **Menu Segurança** — módulo separado com funcionalidades de segurança
- ✓ **Log de Auditoria** (Segurança > Log de Auditoria) — registro em arquivo de todos os logins e logouts
- ✓ Validação de campos obrigatórios em todos os formulários
- ✓ Detecção de login duplicado com mensagem específica
- ✓ Tratamento de erros e exceções em todas as operações

## 🔧 Requisitos do Sistema

### Software
- **Java 8 ou superior** (recomendado Java 11+)
- **MySQL Driver JDBC** (`mysql-connector-java-8.0.33.jar` ou superior)
- **Conexão com Internet** para acessar o banco de dados em nuvem

### Verificar Java Instalado
```bash
java -version
```

Se Java não está instalado, baixe em: https://www.oracle.com/java/technologies/downloads/

## 📁 Estrutura do Projeto

```
javasistema/
├── src/
│   └── javasistema/
│       ├── FormPrincipal.java        # Janela principal com menu
│       ├── LoginDialog.java          # Diálogo de login
│       ├── FormUsuariosListar.java   # Tela de listagem de usuários
│       ├── FormUsuarioEditar.java    # Formulário de inclusão/edição
│       ├── FormLogAuditoria.java     # Tela de visualização do log de auditoria
│       ├── AuditoriaUtil.java        # Utilitário de registro de auditoria
│       ├── Conexao.java              # Gerenciador de conexão DB
│       └── logo.jpg                  # Logo da aplicação
├── compile.sh                        # Script para compilar
├── run.sh                            # Script para executar
├── SQL_SCRIPT.sql                    # Script de banco de dados
├── SETUP.md                          # Guia de instalação passo a passo
└── README.md                         # Este arquivo
```

## 🗄️ Configuração do Banco de Dados

### Dados de Conexão (Já Configurados)
- **Host:** bd_savir.mysql.dbaas.com.br
- **Porta:** 3306
- **Banco:** bd_savir
- **Usuário:** bd_savir
- **Senha:** B@nc0D@d0s
- **Timezone:** America/Fortaleza

### Tabela de Usuários (`tb_usuarios`)
```sql
CREATE TABLE tb_usuarios (
    usuario_id  INT PRIMARY KEY AUTO_INCREMENT,
    nome        VARCHAR(100) NOT NULL,
    login       VARCHAR(50)  NOT NULL UNIQUE,
    senha       VARCHAR(50)  NOT NULL,
    email       VARCHAR(100),
    created_at  TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at  TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Usuários de Teste (Já Inseridos)
| Login | Senha | Nome               |
|-------|-------|--------------------|
| savir | 1234  | Hiran Savir Junior |
| admin | admin | Admin System       |

## 🚀 Instruções de Uso

### 1. Extrair o Projeto
```bash
unzip javasistema.zip
cd javasistema
```

### 2. Compilar
```bash
chmod +x compile.sh
./compile.sh
```

### 3. Executar
```bash
chmod +x run.sh
./run.sh
```

## 🔑 Fluxo Completo de Uso

### Login
1. Clique em **Sistema > Logar**
2. Selecione uma empresa/filial
3. Informe as credenciais: `savir` / `1234` ou `admin` / `admin`
4. Clique em **Entrar**

### Gestão de Usuários
Após o login, acesse **Segurança > Usuários**:

| Ação | Como fazer |
|------|-----------|
| **Listar** | A tela abre com todos os usuários carregados automaticamente |
| **Incluir** | Clique em **INCLUIR**, preencha o formulário e clique em **SALVAR** |
| **Editar** | Selecione uma linha e clique em **EDITAR**, ou dê **duplo clique** na linha |
| **Excluir** | Selecione uma linha e clique em **EXCLUIR** — confirmação obrigatória |
| **Atualizar** | Clique em **ATUALIZAR** para recarregar a lista do banco |
| **Sair** | Clique em **SAIR** para fechar a tela de listagem |

## 🛠️ Estrutura do Código

### `Conexao.java`
- Gerencia a conexão com MySQL via JDBC
- `getConnection()` — retorna uma conexão ativa
- `testarConexao()` — verifica disponibilidade do banco

### `LoginDialog.java`
- Interface de login com Swing (modal)
- Validação de campos obrigatórios
- Autenticação via `PreparedStatement` contra o banco

### `FormPrincipal.java`
- Janela principal (maximizada)
- Menu dinâmico: **Sistema** sempre visível; **Segurança** aparece apenas logado
- Logout com confirmação

### `FormUsuariosListar.java`
- Janela de listagem (1000×600 px, centralizada)
- `JTable` somente leitura com 5 colunas: ID, Nome, Login, E-mail, Criado em
- Botões: INCLUIR, EDITAR, EXCLUIR, ATUALIZAR, SAIR
- Duplo clique na linha abre edição diretamente
- `carregarUsuarios()` — SELECT ordenado por nome
- `abrirFormInclusao()` — instancia `FormUsuarioEditar` com ID 0
- `abrirFormEdicao()` — instancia `FormUsuarioEditar` com ID da linha selecionada
- `excluirUsuarioSelecionado()` — DELETE com confirmação prévia

### `FormUsuarioEditar.java`
- Diálogo modal de inclusão e edição
- Campos: Nome, Login, Senha, E-mail (opcional)
- Modo inclusão (`usuarioId == 0`): executa INSERT
- Modo edição (`usuarioId > 0`): pré-carrega dados e executa UPDATE
- Valida campos obrigatórios (Nome, Login, Senha)
- Detecta erro de login duplicado (`Duplicate entry`) com mensagem específica
- `isSalvo()` — retorna `true` se o salvamento foi concluído com sucesso

## 🐛 Troubleshooting

### Erro: "Driver MySQL não encontrado"
1. Baixe o driver em: https://dev.mysql.com/downloads/connector/j/
2. Coloque o `.jar` na raiz do projeto ou em `/usr/share/java/`

### Erro: "Não foi possível conectar ao banco de dados"
- Verifique sua conexão com a Internet
- Teste: `ping bd_savir.mysql.dbaas.com.br`
- Porta **3306** deve estar desbloqueada no firewall

### Erro: "Usuário ou senha inválidos"
- Use: `savir` / `1234` ou `admin` / `admin` (sem espaços extras)

### "Login já está em uso"
- O campo `login` é UNIQUE no banco — escolha um login diferente

### Tela não abre / botões não funcionam
- Confirme que está **logado** (menu Segurança só aparece após login)
- Recompile: `./compile.sh`

### Erro de compilação "cannot find symbol"
```bash
find . -name "*.class" -delete
./compile.sh
```

## 📝 Notas Importantes

### Segurança
⚠️ **Este é um exemplo educacional. Em produção:**
- Nunca armazene senhas em texto plano — use `bcrypt`, `PBKDF2` ou `Argon2`
- Implemente HTTPS para todas as conexões
- Adicione rate limiting contra força bruta
- Use tokens JWT ou sessões seguras

### Performance
- Conexão é aberta e fechada por operação (adequado para fins educacionais)
- Em produção, use connection pooling: **HikariCP**, **C3P0** ou **DBCP2**

## 📄 Licença
Exemplo educacional — uso livre para fins de aprendizado.

---

**Versão:** 4.0 — CRUD completo de Usuários
**Data:** 2026-05-07
**Autor:** JavaSavir System
**Status:** ✓ Funcional e Testado
