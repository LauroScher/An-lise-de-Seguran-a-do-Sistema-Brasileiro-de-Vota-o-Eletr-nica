# Análise de Segurança do Sistema Brasileiro de Votação Eletrônica 🛡️

Este documento apresenta uma análise de segurança do sistema brasileiro de votação eletrônica, focando em sua perspectiva operacional e arquitetural, a qual é considerada apropriada para a análise de segurança devido à natureza presencial e offline da urna eletrônica, tornando a distribuição e instalação de software, hardware e dados as atividades mais vulneráveis do processo.

## 1\. Visão Geral do Sistema Eleitoral 🗺️

O sistema eleitoral brasileiro, em sua visão de alto nível, descreve o percurso do software, dados e hardware de votação desde sua criação ou armazenamento até o eleitor, e o caminho de retorno dos votos depositados.

![Image](https://github.com/user-attachments/assets/4285a421-895c-4b8f-a204-9100a31890fa)

### 1.1 Descrição dos Passos Operacionais 👣

1.  O código do software da urna eletrônica é desenvolvido no Tribunal Superior Eleitoral (TSE).
2.  Uma versão específica do código é "congelada", transformada em executável e enviada eletronicamente aos Tribunais Regionais Eleitorais (TREs) dias antes da eleição.
3.  No TRE, o pessoal especializado utiliza computadores de mesa para gravar o código executável em "flash de carga" (cartões de instalação) e os dados de candidatos e eleitores em "flash de votação" (cartões de votação).
4.  Esses cartões são então enviados para os depósitos estaduais onde as urnas eletrônicas estão armazenadas.
5.  Pessoal autorizado nos depósitos (cartórios eleitorais) instala o software de votação nas urnas eletrônicas utilizando os flashes de carga.
6.  O flash de votação, contendo dados de candidatos e eleitores, também é instalado fisicamente na urna.
7.  As urnas eletrônicas, com identificação única, são então enviadas para os locais de votação.
8.  Às 8h da manhã, o chefe dos mesários abre a votação digitando um comando no terminal dos mesários.
9.  Eleitores se identificam aos mesários, que inserem a identificação no terminal dos mesários.
10. Em seguida, os eleitores são autorizados a se dirigir à cabine de votação e registrar seu voto na urna eletrônica através do terminal do eleitor.
11. O chefe dos mesários encerra a sessão de votação às 17h, se não houver mais eleitores aguardando.
12. O chefe dos mesários remove o pen drive da urna eletrônica, que contém todos os votos da seção, e utiliza um laptop conectado à Internet para transmitir a lista de votos.
13. O TSE totaliza as listas de votos transmitidas por todas as seções e divulga o resultado das eleições.

*(Observação: A descrição acima omite detalhes não relevantes para o objetivo deste exercício).*

## 2\. Ativos e Objetivos de Segurança 🎯

Os principais ativos que necessitam de proteção e seus objetivos de segurança são:

  * **Segurança no transporte de informações** (TSE para TRE, chefe dos mesários para TSE) 🚚: O objetivo é garantir a confidencialidade, integridade e disponibilidade dos dados transmitidos. Isso é crucial porque a interceptação ou alteração indevida durante o transporte pode comprometer a validade do processo eleitoral.
  * **Confidencialidade dos códigos do software das urnas eletrônicas** 🔒: O objetivo de segurança é garantir que as informações não sejam acessíveis ou descobertas por entidades não autorizadas. A exposição do código pode permitir a identificação de vulnerabilidades ou a criação de softwares maliciosos.
  * **Urnas eletrônicas** 🗳️: Devem estar em ótimo estado de funcionamento e armazenadas em locais de acesso restrito para limitar as possibilidades de adulteração. O acesso deve ser limitado a poucas pessoas com privilégio mínimo de manuseio, garantindo sua disponibilidade durante todo o processo. A adulteração física ou indisponibilidade das urnas pode inviabilizar a votação.
  * **Integridade dos votos** ✅: É um ativo de suma importância, devendo garantir o não-repúdio. Os votos devem ser inalteráveis, com controle de acesso extremamente restrito para garantir a autenticidade das informações registradas nos pen drives usados nas urnas eletrônicas. A alteração ou negação de um voto compromete a legitimidade do resultado.
  * **Políticas aplicadas aos envolvidos** 📜: As políticas são de grande valia no sistema eleitoral, abrangendo responsáveis pelo desenvolvimento de sistemas das urnas, divulgação de resultados e voluntários do processo presencial de votação. O conjunto de regras deve ser estudado e aplicado a cada responsável para mitigar possibilidades de engenharia social. Isso é importante para prevenir manipulações e garantir que todos os envolvidos atuem de forma ética e segura.

## 3\. Ameaças e Adversários 🚨

As principais ameaças que representam ações potenciais de adversários com o intuito de comprometer os ativos previamente identificados devem ser identificadas, juntamente com exemplos de adversários para cada ameaça.

As principais ameaças possíveis são:

  * Vazamentos de informações 📉.
  * Fraudes nos sistemas das urnas eleitorais, ou seja, a alterações indevidas no código executável 🧑‍💻.
  * Violação dos Hardware armazenados 🛠.
  * Engenharia social para obtenção de informações privilegiadas 🎣.
  * Ataques DDoS para interromper o processo de votação e violação dos hardware armazenados 💥.

Os principais adversários para esses contextos são:

  * **Administradores e responsáveis pelo processo eleitoral** (vítimas de engenharia social) 👤.
  * **Hackers externos e funcionários corruptos** (vazamento de informações de propósito e adulteração de dados do sistema ou dispositivos) 👾💼.
  * **Facções criminosas e hackers** (buscam vulnerabilidades nos códigos criptografados e em urnas eletrônicas para causar adulterações, atrasar o processo eleitoral ou coletar informações privilegiadas de maneira ilícita para burlar o sistema) 🕵️‍♀️😈.

## 4\. Potenciais Vulnerabilidades 🩹

As potenciais vulnerabilidades que podem ser exploradas pelos adversários para realizar os ataques identificados devem ser identificadas e justificadas. Para os fins deste exercício, assume-se que as vulnerabilidades apontadas são válidas, mesmo que sua existência real no sistema não seja confirmada, desde que façam sentido em face da descrição do sistema.

As potenciais vulnerabilidades podem estar presentes em:

  * **Falhas de segurança no transporte de informações** 🚚: O agente malicioso pode interceptar os códigos enviados do TSE para o TRE ou o envio dos dados de todos os votos para gerar ataques de negação ou interceptar informações confidenciais.
  * **Falta de segurança no armazenamento das urnas e pen drives** 📦: Ambos os hardwares são distribuídos em diferentes regiões, dificultando a garantia de acesso restrito a todos esses dispositivos. Caso um agente malicioso tenha acesso, ele poderá violar a integridade destes ativos em determinadas regiões.
  * **Ações de hackers externos e funcionários corruptos** 🧑‍💻💼: Podem buscar meios de burlar e prejudicar o sistema de votação para fins de benefícios comuns.
  * **Engenharia social** 🗣️: Pode tornar vítima qualquer um dos envolvidos no processo de votação, sejam eles mesários, administradores, desenvolvedores ou funcionários. Pessoas antiéticas podem tentar usar *phishing* para conseguir informações pessoais e obter acesso a privilégios indevidos, gerando riscos no processo eleitoral.

## 5\. Potenciais Defesas (Controles Físicos, Técnicos ou Administrativos) 🛡️

É preciso descrever as potenciais defesas que o sistema pode utilizar ou já está utilizando para reduzir as vulnerabilidades identificadas. A descrição deve ser exaustiva, assumindo que o sistema não possui nenhum mecanismo de segurança inicial.

As potenciais defesas incluem:

  * **Criptografia avançada de ponta a ponta e assinaturas digitais** 🔐: Para a verificação de integridade das informações.
  * **Hardware sem acesso à internet** 🔌: Que impossibilita a interceptação remota das urnas eletrônicas e dados armazenados.
  * **Políticas de segurança** 📝: Envolvendo todo o processo de votação, como a identificação de Múltiplos Fatores de Autenticação (MFA) exigida para cada eleitor ou responsável pelo processo eleitoral.
  * **Organização para capacitação de administradores e mesários** 🧑‍🏫: Com privilégios mínimos, para evitar possíveis consequências de engenharia social.

## 6\. Avaliação de Riscos 📊

Os riscos associados aos ativos, ameaças e vulnerabilidades potenciais descritos nos itens anteriores devem ser avaliados. É necessário indicar, informalmente, o quão séria é cada combinação ativo-ameaça-vulnerabilidade.

A avaliação de riscos dos ativos é a seguinte:

  * **Transporte de dados** 🚚: Ativo de **alta gravidade** 🔴, pois caso ocorra uma ameaça, afetará a integridade e confidencialidade das informações.
  * **Código do sistema das urnas** 🧑‍💻: Ativo com **alta gravidade de risco** 🔴, pois caso ocorra uma ameaça, afetará todo o processo eleitoral.
  * **Urnas eletrônicas** 🗳️: Ativo com **média gravidade de riscos** 🟠, pois caso ocorra uma ameaça, atrasará o processo eleitoral (que possui um tempo limite) e a urna será substituída por outra.
  * **Integridade de votos** ✅: Ativo de **alta gravidade** 🔴, pois caso ocorra uma ameaça, violará a privacidade e a possibilidade de registros fraudulentos.
  * **Política de segurança** 📝: Ativo de **média gravidade** 🟠, pois caso ocorra uma ameaça, violará as regras aplicadas, mas deixará registrados os responsáveis que responderam por seus atos. Esse método é conhecido como *accountability* e garante o não-repúdio dos registros.

-----
