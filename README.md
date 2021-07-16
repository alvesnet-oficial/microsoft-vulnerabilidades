# microsoft-vulnerabilidades

# Vulnerabilidade de execução remota de código do Spooler de Impressão do Windows
# CVE-2021-34527

fonte: https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-34527

Vulnerabilidade de Segurança
Lançado: 01/07/2021 Last updated: 15 de jul de 2021

Assigning CNA:
Microsoft
MITRE CVE-2021-34527

CVSS:3.0 8.8 / 8.2

# Sinopse
Existe uma vulnerabilidade de execução remota de código quando o serviço Spooler de impressão do Windows executa incorretamente operações de arquivo com privilégios. Um invasor que conseguir explorar essa vulnerabilidade poderá executar código arbitrário com privilégios do SISTEMA. O invasor poderá instalar programas; exibir, alterar ou excluir dados; ou criar novas contas com direitos totais de usuário.

ATUALIZAÇÃO em 7 de julho de 2021: A atualização de segurança para Windows Server 2012, Windows Server 2016 e Windows 10, Versão 1607 foi lançada. Consulte a tabela Atualizações de Segurança para obter as atualizações aplicáveis a seu sistema. Recomendamos que você instale essas atualizações imediatamente. Se você não conseguir instalar essas atualizações, consulte as seções de Perguntas Frequentes e Solução Alternativa nesta CVE para obter informações sobre como ajudar a proteger seu sistema contra essa vulnerabilidade.

Além de instalar as atualizações, para proteger seu sistema, você deve confirmar se as seguintes configurações do Registro estão definidas como 0 (zero) ou não estão definidas (Observação: essas chaves do Registro não existem por padrão e, portanto, já estão na configuração segura) e também se a configuração de sua Política de Grupo está correta (consulte as Perguntas Frequentes):

HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Printers\PointAndPrint
NoWarningNoElevationOnInstall = 0 (DWORD) ou não definido (configuração padrão)
UpdatePromptSettings = 0 (DWORD) ou não definido (configuração padrão)

# Having NoWarningNoElevationOnInstall definido como 1 torna seu sistema vulnerável por design.

ATUALIZAÇÃO 6 de julho de 2021: A Microsoft concluiu a investigação e lançou atualizações de segurança para corrigir essa vulnerabilidade. Consulte a tabela Atualizações de Segurança para obter as atualizações aplicáveis a seu sistema. Recomendamos que você instale essas atualizações imediatamente. Se você não conseguir instalar essas atualizações, consulte as seções de Perguntas Frequentes e Solução Alternativa nesta CVE para obter informações sobre como ajudar a proteger seu sistema contra essa vulnerabilidade. Consulte também KB5005010: Restringir a instalação de novos drivers de impressora após a aplicação das atualizações de 6 de julho de 2021.

Observe que as atualizações de segurança lançadas em e após 6 de julho de 2021 contêm proteções para a CVE-2021-1675 e a exploração de execução remota de código adicional no serviço Spooler de Impressão do Windows conhecida como “PrintNightmare”, documentada em CVE-2021-34527.

# Soluções alternativas
# Determinar se o serviço Spooler de Impressão está em execução

Execute o seguinte no Windows PowerShell:

Get-Service -Name Spooler

Se o Spooler de Impressão estiver em execução ou se o serviço não estiver definido como desabilitado, selecione uma das seguintes opções para desabilitar o serviço Spooler de Impressão ou Desabilitar a impressão remota de entrada por meio da Política de Grupo:

# Opção 1 — Desabilitar o serviço Spooler de Impressão

Se desabilitar o serviço Spooler de Impressão for apropriado para sua empresa, use os seguintes comandos do PowerShell:

Stop-Service -Name Spooler -Force

Set-Service -Name Spooler -StartupType Disabled

Impacto da solução alternativa Desabilitar o serviço Spooler de Impressão desabilita a capacidade de imprimir local e remotamente.

# Opção 2 — Desabilitar a impressão remota de entrada por meio da Política de Grupo

Você também pode definir as configurações por meio da Política de Grupo da seguinte maneira:

Configuração do Computador/Modelos Administrativos/Impressoras

Desabilite a política “Permitir que o spooler de impressão aceite conexões de cliente:” para bloquear ataques remotos.

Você deve reiniciar o serviço Spooler de Impressão para que a política de grupo tenha efeito.

Impacto da solução alternativa Esta política bloqueará o vetor de ataque remoto evitando operações de impressão remota de entrada. O sistema não funcionará mais como um servidor de impressão, mas a impressão local em um dispositivo conectado diretamente ainda será possível.
