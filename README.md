# reset_anydesk.cmd
@echo off & setlocal enableextensions
title AnyDesk Reset

reg query HKEY_USERS\S-1-5-19 >NUL || (
    echo Executar como administrador.
    pause >NUL
    exit
)

chcp 437

call :stop_any

del /f "%ALLUSERSPROFILE%\AnyDesk\service.conf"
del /f "%APPDATA%\AnyDesk\service.conf"

copy /y "%APPDATA%\AnyDesk\user.conf" "%temp%\"

rd /s /q "%temp%\thumbnails" 2>NUL

xcopy /c /e /h /r /y /i /k "%APPDATA%\AnyDesk\thumbnails" "%temp%\thumbnails"

del /f /a /q "%ALLUSERSPROFILE%\AnyDesk\*"
del /f /a /q "%APPDATA%\AnyDesk\*"

call :start_any

:lic
type "%ALLUSERSPROFILE%\AnyDesk\system.conf" | find "ad.anynet.id=" || goto lic

call :stop_any
move /y "%temp%\user.conf" "%APPDATA%\AnyDesk\user.conf"
xcopy /c /e /h /r /y /i /k "%temp%\thumbnails" "%APPDATA%\AnyDesk\thumbnails"
rd /s /q "%temp%\thumbnails"

call :start_any

echo *********
echo Concluído.
echo(
goto :eof

:start_any
sc start AnyDesk
sc start AnyDesk
if %errorlevel% neq 1056 goto start_any

set AnyDesk1=%SystemDrive%\Program Files (x86)\AnyDesk\AnyDesk.exe
set AnyDesk2=%SystemDrive%\Program Files\AnyDesk\AnyDesk.exe
if exist "%AnyDesk1%" start "" "%AnyDesk1%"
if exist "%AnyDesk2%" start "" "%AnyDesk2%"
exit /b

:stop_any
sc stop AnyDesk
sc stop AnyDesk
if %errorlevel% neq 1062 goto stop_any
taskkill /f /im "AnyDesk.exe"
exit /b


# README.md
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

# README.md

# AnyDesk Reset – Script Automático (Windows)

Este repositório contém um script para redefinir configurações do **AnyDesk**, incluindo limpeza de cache, remoção de arquivos de configuração e reinicialização do serviço.

## 🔧 Como funciona
- Verifica privilégios de administrador
- Encerra o serviço AnyDesk
- Faz backup temporário do user.conf e miniaturas
- Limpa diretórios de configuração
- Reinicia o AnyDesk para regenerar system.conf
- Restaura arquivos do usuário
- Inicia o AnyDesk novamente e finaliza

## 🚀 Uso
1. Baixe o arquivo `.cmd`
2. Execute como administrador
3. Aguarde a finalização automática

## ⚠️ Aviso
Este script remove configurações locais do AnyDesk. Use com cautela em ambientes corporativos.
