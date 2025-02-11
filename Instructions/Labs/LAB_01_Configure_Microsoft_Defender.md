---
lab:
  title: Configurar o Microsoft Defender
  module: Configure the Microsoft Defender XDR environment
---
Você é um analista de operações de segurança que trabalha em uma empresa que está implantando o Microsoft Defender XDR. Sua função é orientar a equipe de TI da empresa quanto à defesa contra ameaças cibernéticas com o Microsoft Defender (XDR). Os executivos se preocupam muito com que todas as diretrizes sejam seguidas, e com que todos os requisitos sejam atendidos quando você faz as atividades no ambiente deles.

# Configurar o ambiente do Microsoft Defender XDR

Neste exercício, você provisionará o ambiente do Microsoft Defender XDR, integrará estações de trabalho do cliente no Defender para Ponto de Extremidade e executará um cenário de ataque simulado em uma estação de trabalho do cliente.

Este exercício deve levar aproximadamente **10-15** minutos para ser concluído.

>**Importante:** você precisará ter acesso a um Locatário do Microsoft 365 E5 com uma licença P2 do Microsoft Defender para Ponto de Extremidade para fazer os exercícios a seguir. Você também precisará ter estações de trabalho de cliente do Microsoft Windows 10 ou 11 para integrar e executar ataques simulados.

## Tarefa 1 – Preparar o workspace do Microsoft Defender XDR

1. No navegador Microsoft Edge, acesse o portal do Microsoft Defender em (<https://security.microsoft.com>).
1. No portal **Microsoft Defender**, no menu de navegação, selecione **Configurações** à esquerda.

    >**Observação:** talvez seja necessário rolar até o topo do menu.

1. Role para baixo os itens de menu para **Ativos** e selecione **Dispositivos**.

1. O processo para implantar o workspace do Defender XDR deve ser iniciado e você deverá ver mensagens informando que *carregar e inicializar* será exibida brevemente na parte superior da página e, em seguida, você verá uma imagem de uma caneca de café e uma mensagem que diz: **Espere um pouco. Estamos preparando novos espaços para seus dados e conectando-os.** O laboratório leva cerca de cinco minutos para ser concluído. *Deixe a página aberta e certifique-se de que ela seja concluída, pois ela é necessária para o próximo Laboratório.*

    >**Observação:** Desconsidere as mensagens de erro pop-up informando que *Alguns de seus dados não podem ser recuperados*. Se a mensagem "Espere! Estamos preparando novos espaços para seus dados e conectando-os" não aparece ou a página "Configurações > Microsoft Defender XDR > Conta" é aberta, mas você vê a mensagem *Falha ao carregar o local de armazenamento de dados. Tente novamente mais tarde*, selecione "Configurações de serviço de alerta" no menu "Geral".

1. Quando a inicialização do novo workspace for concluída, a página do portal **Página Inicial** exibirá um banner **Tenha o SIEM e o XDR em um só lugar**. E, em **Configurações**, as configurações gerais do Microsoft Defender XDR para Conta, Notificações por email, **Recursos de visualização**, Configurações do serviço de alerta, Permissões e funções e API de streaming agora estão ativadas.

### Tarefa 2: aplicar políticas de segurança predefinidas no Microsoft Defender para Office 365

Nesta tarefa, você atribuirá políticas de segurança predefinidas para a EOP (Proteção do Exchange Online) e o Microsoft Defender para Office 365 no portal de segurança do Microsoft 365.

1. Faça logon na máquina virtual WIN1 como Administrador com a senha: **Pa55w.rd**.  

1. Inicie o navegador Microsoft Edge.

1. No navegador Microsoft Edge, acesse o portal do Microsoft Defender XDR em (<https://security.microsoft.com>).

1. Na caixa de diálogo **Entrar**, copie e cole a conta de email do locatário referente ao nome de usuário do administrador fornecido pelo provedor de hospedagem do laboratório e selecione **Avançar**.

1. Na caixa de diálogo **Inserir senha**, copie e cole a senha de locatário do administrador fornecida pelo provedor de hospedagem do laboratório e selecione **Entrar**.

    >**Observação:** se você receber uma mensagem "A operação não pôde ser concluída. Tente novamente mais tarde. Se o problema persistir, contate o Suporte da Microsoft.", clique em **OK** para continuar.  

1. Se mostrada, feche a janela pop-up do tour rápido do Microsoft Defender XDR. **Dica:** Posteriormente nesse laboratório, você precisará aguardar até que o workspace do Defender seja provisionado. Você pode aproveitar esse tempo para navegar pelos passeios guiados para saber mais sobre o Microsoft Defender XDR.

1. No menu de navegação, na *área Email e colaboração*, selecione **Políticas e regras**.

1. No painel *Política e regras*, selecione **Políticas de ameaça**.

1. No painel *Políticas de ameaça*, selecione **Políticas de segurança predefinidas**.

    >**Observação:** se você receber a mensagem *"Erro do cliente – Erro ao obter a regra bip"*, selecione **OK** para continuar. O erro se deve ao status de hidratação de seu locatário no Office 365, que não está habilitado por padrão.

    >**Observação:** se você receber a mensagem *"Erro do cliente – Ocorreu um erro ao recuperar as políticas de segurança predefinidas. Tente novamente mais tarde."*, selecione **OK** para continuar. Atualize seu navegador usando **Ctrl+F5**.

1. Na página *pop-out* **Saiba mais sobre políticas de segurança predefinidas**, selecione **Fechar**.

1. Em *Proteção padrão*, selecione **Gerenciar configurações de proteção**. **Dica:** se você vir essa opção esmaecida, atualize seu navegador usando **Ctrl+F5**.

1. Na seção *Aplicar Proteção do Exchange Online*, selecione **Destinatários específicos** e, em **Domínios**, comece a escrever o nome de domínio do locatário, selecione-o e clique em **Avançar**.

    >**Dica:** O nome de domínio do locatário é o mesmo nome que você tem para sua conta de administrador, pode ser algo como *WWLx######.onmicrosoft.com*. Observe que essa configuração aplica políticas para antispam, filtro de spam de saída, antimalware e antiphishing.

1. Na seção *Aplicar proteção do Defender para Office 365*, aplique a mesma configuração da etapa anterior e clique em **Avançar**. Observe que essa configuração aplica políticas para antiphishing, anexos seguros e links seguros.

1. Na seção *Proteção de representação*, clique em **Avançar** quatro vezes (4x) para continuar.

1. Na seção *Modo de política*, verifique se o botão de opção **Ativar a política depois da conclusão** está selecionado e clique em **Avançar**.

1. Leia o conteúdo em *Revisar e confirmar suas alterações* e clique em **Confirmar** para aplicar as alterações. Depois, clique em **Concluído** para concluir.

    >**Observação:** se você receber a mensagem *"O URI ''<https://outlook.office365.com/psws/service.svc/AntiPhishPolicy>" não é válido para a operação PUT. O URI deve apontar para um único recurso para operações PUT."*, Selecione **OK** e, em seguida, selecione **Cancelar** para retornar à página principal. Você verá que a opção *Proteção padrão está ativada* está habilitada.

1. Em *Proteção estrita*, selecione **Gerenciar configurações de proteção**. **Dica:** a *Proteção restrita* é encontrada em "Email e colaboração – Políticas e regras – Políticas de ameaça – Políticas de segurança predefinidas".

1. Em *Aplicar Proteção do Exchange Online*, selecione **Destinatários específicos** e, em **Grupos**, comece a escrever **Liderança**, selecione o termo e clique em **Avançar**. Observe que essa configuração aplica políticas para antispam, filtro de spam de saída, antimalware e antiphishing.

1. Na seção *Aplicar proteção do Defender para Office 365*, aplique a mesma configuração da etapa anterior e clique em **Avançar**. Observe que essa configuração aplica políticas para antiphishing, anexos seguros e links seguros.

1. Na seção *Proteção de representação*, clique em **Avançar** quatro vezes (4x) para continuar.

1. Na seção *Modo de política*, verifique se o botão de opção **Ativar a política depois da conclusão** está selecionado e clique em **Avançar**.

1. Leia o conteúdo em *Revisar e confirmar suas alterações* e clique em **Confirmar** para aplicar as alterações. Depois, clique em **Concluído** para concluir.

    >**Observação:** se você receber a mensagem *"O URI ''<https://outlook.office365.com/psws/service.svc/AntiPhishPolicy>" não é válido para a operação PUT. O URI deve apontar para um único recurso para operações PUT."*, Selecione **OK** e, em seguida, selecione **Cancelar** para retornar à página principal. Você verá que a opção *Proteção estrita está ativada* está habilitada.

## Você concluiu o laboratório
