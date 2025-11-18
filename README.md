# Resetar AnyDesk – Script Automático (Windows)

Este repositório contém um script para redefinir configurações do **AnyDesk**, incluindo limpeza de cache, remoção de arquivos de configuração e reinicialização do serviço.

O objetivo é resolver problemas comuns, como:
- AnyDesk travando
- ID corrompido
- Configurações quebradas
- Miniaturas que não carregam
- Conflitos após atualização

---

## 🔧 Como funciona

O script executa:

1. Verificação de execução como administrador
2. Encerramento do serviço e do processo AnyDesk
3. Backup temporário do `user.conf` e `thumbnails`
4. Limpeza completa:
   - `%ALLUSERSPROFILE%\\AnyDesk`
   - `%APPDATA%\\AnyDesk`  
5. Recriação dos arquivos essenciais
6. Aguarda a regeneração do arquivo `system.conf`
7. Restaura arquivos personalizados do usuário
8. Reinicia o AnyDesk automaticamente
9. Exibe mensagem final de conclusão

---

## 📜 Código completo

Conteúdo disponível no arquivo `Anydesk-Reset.cmd` deste repositório.

---

## 🚀 Como usar

1. Baixe o arquivo `.cmd`  
2. Clique com o botão direito → **Executar como administrador**  
3. Aguarde o processo  
4. O AnyDesk será reiniciado automaticamente

---

## ⚠️ Aviso

Esse script redefinirá configurações locais do AnyDesk.  
Use com cautela em ambientes corporativos.
