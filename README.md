# BackupAutomaticoSQLEXPRESS

O SQL Server na versão Express não possui o "SQL Server Agent",que é o responsável pela automação do SQL Server, trabalhando em cima de processamento de tarefas, executar jobs agendados e alertas.Para configurar o backup automático de suas bases de dados sem esta ferramenta,é necessário configurar alguns arquivos .bat e scripts além de usar o agendador de tarefas do windows para que excutà-los.
# Baixando scripts
Baixe o arquivo Scripts.zipe e descompacte no C: do servidor.O script "SP_DatabaseBackup.sql" também está disponível no site https://ola.hallengren.com/  que é um repositório de scripts para Sql Server.

# Criando a Stored Procedure na instância
Edite o arquivo "SP_DatabaseBackup.sql".<br>
Nele, altere a linha "SET @BackupDirectory = N'C:\Backup_BD'" colocando o diretório onde deseja salvar os backups dos Bancos de dados de sua instância.

# Ajustando os arquivos .bat
Acesse a pasta bat e ajuste os arquivos Backup_Full.bat,Backup_Diff.bat e Backup_Log.bat. Na linha<br>
sqlcmd -S DESKTOP-MGNKM48\SQLEXPRESS -E -i "C:\Scripts\sql\Backup_Full.sql" -o "C:\Scripts\log\Backup_Full.log"<br>
altere para <br>
sqlcmd -S NOMESERVIDOR\NOMEINSTANCIa -E -i "C:\Scripts\sql\Backup_Full.sql" -o "C:\Scripts\log\Backup_Full.log"

# Ajuste os arquivos de backup
Acesse a pasta sql e ajuste os arquivos Backup_Full.sql,Backup_Diff.sql e Backup_Log.sql e altere <br>
@Directory = 'C:\Backup_BD'<br>
para<br>
@Directory = 'DiretorioDoSeuBackup'

# Criando tarefas no Agendados de Tarefas do Windows
Siga o tutorial contido no link abaixo:<br>
https://www.profissionaisti.com.br/2016/08/usando-o-agendador-de-tarefas-do-windows/

# OBS:
Você deve configurar o Agendador de tarefas para executar os arquivos .bat.
