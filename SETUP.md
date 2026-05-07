# 🚀 Guia de Setup — SuperSistema

## ⚡ Quick Start (30 segundos)

```bash
# 1. Extrair
unzip javasistema.zip
cd javasistema

# 2. Compilar
./compile.sh

# 3. Executar
./run.sh
```

**Credenciais para teste:**
- Usuário: `savir` | Senha: `1234`
- Usuário: `admin` | Senha: `admin`

---

## 🔧 Instalação Passo a Passo

### Passo 1: Verificar Java
```bash
java -version
javac -version
```
Saída esperada: Java 8 ou superior (recomendado Java 11+)

**Se não tiver Java:**
- Windows: https://www.oracle.com/java/technologies/downloads/
- Linux (Ubuntu/Debian): `sudo apt install default-jdk`
- macOS: `brew install java`

### Passo 2: Extrair o Projeto
```bash
unzip javasistema.zip
cd javasistema
```

### Passo 3: Baixar Driver MySQL (se necessário)
```bash
# Ubuntu/Debian
sudo apt install libmysql-java

# Ou baixar manualmente
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-8.0.33.jar
```

### Passo 4: Compilar
```bash
chmod +x compile.sh
./compile.sh
```

Saída esperada:
```
================================
Compilando SuperSistema...
================================
✓ Compilação concluída com sucesso!
```

### Passo 5: Executar
```bash
chmod +x run.sh
./run.sh
```

---

## 🧪 Testando o Sistema Completo

### 1. Login
1. Clique em **Sistema > Logar**
2. Selecione uma empresa/filial
3. Informe: `savir` / `1234`
4. Clique **Entrar**
5. ✓ Mensagem de boas-vindas deve aparecer

### 2. Listagem de Usuários
1. Clique em **Segurança > Usuários**
2. ✓ Grid abre com os usuários cadastrados

### 3. Incluir Usuário
1. Na tela de usuários, clique em **INCLUIR**
2. Preencha: Nome, Login, Senha (obrigatórios) e E-mail (opcional)
3. Clique em **SALVAR**
4. ✓ Novo usuário aparece na lista automaticamente

### 4. Editar Usuário
1. Selecione um usuário na lista
2. Clique em **EDITAR** (ou dê duplo clique na linha)
3. Altere os dados desejados
4. Clique em **SALVAR**
5. ✓ Lista atualizada com os novos dados

### 5. Excluir Usuário
1. Selecione um usuário na lista
2. Clique em **EXCLUIR**
3. Confirme na caixa de diálogo
4. ✓ Usuário removido e lista recarregada

---

## 📋 Troubleshooting

| Problema | Solução |
|----------|---------|
| `javac: command not found` | Instale JDK (não apenas JRE) |
| Driver não encontrado | Instale `libmysql-java` ou baixe o `.jar` |
| Sem conexão com banco | Verifique Internet + porta 3306 |
| Erro de compilação | `find . -name "*.class" -delete && ./compile.sh` |
| Login falha | Use `savir`/`1234` ou `admin`/`admin` |
| Menu Segurança não aparece | Faça login primeiro |
| "Login já está em uso" | Escolha um login diferente (campo UNIQUE) |

---

## ✓ Checklist Final

- [ ] Java instalado (`java -version`)
- [ ] Projeto compilado sem erros (`./compile.sh`)
- [ ] Login funciona com `savir` / `1234`
- [ ] **Segurança > Usuários** abre o grid
- [ ] Botão **INCLUIR** abre formulário e salva no banco
- [ ] Botão **EDITAR** / duplo clique abre formulário com dados preenchidos
- [ ] Botão **EXCLUIR** remove após confirmação
- [ ] Botão **ATUALIZAR** recarrega a lista

---

**Versão:** 4.0 — CRUD completo de Usuários
**Data:** 2026-05-07
**Autor:** JavaSavir System
