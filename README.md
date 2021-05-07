<p align="center">
  <img src="https://i.imgur.com/ZznEDCJ.jpg" height="260" width="300">
</p>

<h1>🕵️‍♀️ Mara Detetive</h1>
<p><strong>Este repositório contém arquivos e códigos que foram criados no prazo de alguns dias apenas para fins de validação e testes da nossa ideia. Em nenhum momento nos preocupamos com a arquitetura por trás para obtermos um sistema mais robusto. Caso a ideia vá pra frente, tudo isso será refeito e reestruturado.</strong></p></br>



<h2>📯 Introdução</h2>
<p>A Mara Detetive nasceu com o propósito de se tornar um assistente virtual capaz de não só, identificar a veracidade de uma notícia como também auxiliar na disseminação de informações. Com o avanço das redes sociais e principalmente dos aplicativos de envio de mensagens, também tivemos um avanço da disseminação de notícias falsas, uma vez que as pessoas estão conseguindo obter informações (nem sempre verdadeiras) de forma mais acelerada.</p>

<p>Podemos perceber que esse problema é causado muitas vezes pela preguiça de ir atrás da notícia em fontes confiáveis ou também pela auto confiança de que aquilo é realmente verdade. Além disso, as pessoas sentem cada vez mais necessidade de conseguir informações de maneira fácil e rápida para problemas reais do seu dia da dia.</p></br>



<h2>💡 A ideia</h2>
<p>Diante desse cenário e da dificuldade em controlar a velocidade que uma notícia falsa pode se propagar, imaginamos um cenário onde o usuário antes de encaminhar uma notícia que recebeu pelo Whatsapp à algum amigo ou grupo específico, ele possa encaminhar essa mensagem para um Bot que consiga extrair aquela notícia e através de um modelo pré-treinado com notícias falsas e verdadeiras, consiga saber se aquela notícia é verdadeira ou não. Não só isso como também, a pessoa poderá procurar por um determinado restaurante ou farmácia visto que com a quarentena muitos estabelecimentos estão fechados.</p></br>



<h2>❓ Como fazer isso</h2>
<p>Para colocar essa ideia em prática utilizaremos algumas ferramentas já disponíveis no mercado que agilizam muito no processo de desenvolvimento:</p></br>

### [Twilio - Whatsapp:]("https://www.twilio.com/whatsapp")
<p>Serviço que possibilita a troca de mensagens através do Whatsapp. No projeto utilizamos para fazer a troca de mensagem entre o Assistant e o usuário.</p></br>

### [Twilio - SMS:]("https://www.twilio.com/sms")
<p>Serviço que possibilita o envio de SMS para algum usuário. No projeto usamos para simular o envio de uma notificação quando o usuário não encontra a notícia que ele procurou. Nesse caso, o número de algum responsável fica cadastrado no sistema e assim quando ele receber essa notificação, ele pode ir atrás das informações necessárias para treinar o modelo.</p></br>

### [IBM Watson Discovery:]("https://www.ibm.com/br-pt/cloud/watson-discovery")
<p>Serviço que ajuda na criação  de aplicativos relacionados a dados, contando com exploração cognitiva e Inteligência Artificial. Utilizamos ele para criar modelos e treiná-los com notícias falsas e verdadeiras. Além de inserir as notícias, podemos treinar a relevância dos resultados para tornar as respostas mais assertivas. Conforme os usuários usam o serviço, podemos capturar as mensagens que eles estão enviando e usar isso para o treinamento.</p></br>

### [IBM Watson Assistant:]("https://www.ibm.com/cloud/watson-assistant/")
<p>Serviço que auxilia na criação de chatbots. No projeto utilizamos para fazer a ponte entre o serviço de envio de mensagens no Whatsapp disponibilizado pela Twilio e o Watson Discovery.</p>
<p>Funciona assim: Assim que o Watson Assistant recebe uma mensagem, ele analisa qual a intenção do usuário ao enviar aquela mensagem(por exemplo, uma saudação, despedida ou um envio de alguma notícia para análise). Enquanto o assistant não entende que o usuário quer analisar uma notícia, ele apenas vai interagindo com a pessoa com as mensagens que ele foi treinado para enviar. A partir do momento que ele entende que a mensagem é uma notícia que deve ser analisada, ele envia essa mensagem para o Watson Discovery para que ele busque por informações sobre a veracidade. Quando o Discovery obtém uma resposta, ele a retorna e a partir daí o Assistant pode confirmar com o usuário se é aquilo que ele estava buscando ou não.</p></br>

### [IBM Cloud Functions:]("https://developer.ibm.com/api/view/cloudfunctions-prod:cloud-functions#Overview")
<p>Para unir todos esses serviços criamos um script em NodeJS (index.js) e hospedamos na Cloud Functions da IBM. Link do serviço: 
https://us-south.functions.cloud.ibm.com/api/v1/web/joedunicamp%40gmail.com_dev/default/whatsapp-two</p></br>

## 🔨 Como testar o serviço:
- Enviar uma mensagem com o código **join topic-ready** para o número +1 415 523 8886. A partir daí você poderá interagir com o assistente.
Ex:
<p align="center">
  <img src="https://i.imgur.com/qIzPuU1.jpg" height="260" width="300">
</p>

<p>As imagens abaixo, mostram os possíveis cenários de interação. Por se tratar de um ambiente de testes, ainda não foi coberto todos os possíveis cenários e erros podem vir a acontecer.</p>

<p>Ex: Fake News sobre o áudio enviado pelo ministro da saúde. Fonte: https://www.saude.gov.br/fakenews/46588-ministro-da-saude-pede-para-compartilhar-audio-com-informacoes-do-coronavirus-e-fake-news</p>

<p align="center">
  <img src="https://i.imgur.com/BLAEasB.jpg" height="550" width="280">
  <img src="https://i.imgur.com/oTXOWpJ.jpg" height="550" width="280"> 
</p>

<p>No exemplo abaixo, é solicitada a análise de uma notícia na qual o modelo ainda não foi treinado. Nesse caso, ele busca algo no qual ele acha que pode ser o que o usuário está pedindo. Quando o usuário informa que aquela informação não é o que ele solicitou, enviamos um SMS notificando algum responsável que existe uma possível nova fake news se espalhando e, com isso, ele pode ir analisá-la. Essa busca que o usuário faz, poderia ficar salva em um banco e ser exibida em uma página web (Ainda não foi implementada) e quando o responsável receber a notificação, ele pode ir nesse site obter mais informações sobre a nova possível Fake News.</p>

<p>Ex: Rússia anuncia cura para coronavírus. Fonte: https://www.saude.gov.br/fakenews/46653-russia-anuncia-cura-para-coronavirus-e-fake-news (No momento, é uma fake news - 03/04/2020)</p>

<p align="center">
  <img src="https://i.imgur.com/psQL0hO.jpg" height="550" width="280">
  <img src="https://i.imgur.com/LX2TREY.jpg" height="550" width="280">
</p>

<p>As notícias utilizadas para treinar o modelo foram tiradas do site: https://www.saude.gov.br/fakenews</p>

#### Alguns exemplos de noticias utilizadas são:
- [Utilizar álcool em gel nas mãos para prevenir coronavírus altera bafômetro nas blitz](https://www.saude.gov.br/fakenews/46467-utilizar-alcool-em-gel-nas-maos-para-prevenir-coronavirus-altera-bafometro-nas-blitz-e-fake-news)
- [Álcool em gel é a mesma coisa que nada](https://www.saude.gov.br/fakenews/46463-alcool-em-gel-e-a-mesma-coisa-que-nada-e-fake-news)
- [Aplicativo Coronavírus-SUS, do Governo do Brasil, é inseguro](https://www.saude.gov.br/fakenews/46586-aplicativo-coronavirus-sus-do-governo-do-brasil-e-inseguro-e-fake-news)
- [Áudio do professor titular de cirurgia torácica da USP/HC/Incor](https://www.saude.gov.br/fakenews/46575-audio-do-professor-titular-de-cirurgia-toracica-da-usp-hc-incor-e-verdade)
- [Ministro da Saúde Luiz Henrique pede para compartilhar áudio](https://www.saude.gov.br/fakenews/46588-ministro-da-saude-pede-para-compartilhar-audio-com-informacoes-do-coronavirus-e-fake-news)
- [Beber muita água e fazer gargarejo com água morna, sal e vinagre previne coronavírus](https://www.saude.gov.br/fakenews/46582-beber-muita-agua-e-fazer-gargarejo-com-agua-morna-sal-e-vinagre-previne-coronavirus-e-fake-news)
- [Chá de erva doce e coronavírus](https://www.saude.gov.br/fakenews/46440-cha-de-erva-doce-e-coronavirus-e-fake-news)
- [Governo do Brasil anuncia vacina do coronavírus](https://www.saude.gov.br/fakenews/46585-governo-do-brasil-anuncia-vacina-do-coronavirus-e-fake-news)
- [Médicos tailandeses curam coronavírus em 48h](https://www.saude.gov.br/fakenews/46367-medicos-tailandeses-curam-coronavirus-em-48h-e-fake-news)
- [Receita de coco que cura coronavírus](https://www.saude.gov.br/fakenews/46479-receita-de-coco-que-cura-coronavirus-e-fake-news)
- [Tribunal chinês para matar 20 mil pacientes com coronavírus](https://www.saude.gov.br/fakenews/46439-tribunal-chines-para-matar-20-mil-pacientes-com-coronavirus-e-fake-news)

</br>

## ♾️ Indo além...
<p>Recentemente a Polícia Federal percorreu por várias rodovias mapeando todos os estabelecimentos que estão abertos durante a quarentena visto que muitos serviços foram fechados. Tudo isso foi feito para ajudar os caminhoneiros a encontrar restaurantes e serviços durante esse período. Para ajudar a disseminar essa informação, também colocamos uma "Intent" que identifica se alguém está em busca de algum restaurante:</p>

<p align="center">
  <img src="https://i.imgur.com/DTv1SeN.jpg" height="550" width="280">
</p>

<p>Junto a esse serviço, também inserimos uma "Intent" que pode ajudar a pessoa a encontrar remédios durante essa crise, também alertando sobre os riscos da hidroxicloroquina:</p>

<p align="center">
  <img src="https://i.imgur.com/b4G9b7c.jpg" height="550" width="280"> 
</p></br>



<h2>🤝 Contribuidores</h2>
<table>
  <tr>
    <td align="center"><a href="https://github.com/JoedSilva18"><img style="border-radius: 50%;" src="https://avatars.githubusercontent.com/u/41526188?v=4" width="100px;" alt="Joed Silva"/><br /><sub><b>Joed Silva</b></sub></a><br /><a href="https://github.com/JoedSilva18" title="Joed Silva">☕</a></td>
  </tr>
</table></br>


<h2>👽 Autor</h2>
<table>
  <tr>
    <td align="center"><a href="https://github.com/Silvio-Ronaldo"><img style="border-radius: 50%;" src="https://avatars.githubusercontent.com/u/48893927?v=4" width="100px;" alt="Silvio Ronaldo"/><br /><sub><b>Silvio Ronaldo</b></sub></a><br /><a href="https://github.com/Silvio-Ronaldo" title="Silvio Ronaldo">🍀</a></td>
  </tr>
</table>

<p>Leave your star, fork the project or open a pull request ❤️</p>
<p>Contact me on social networks: </p>
<p><a href="https://twitter.com/sivirinoo"><img src="https://img.shields.io/twitter/follow/sivirinoo?style=social" alt="Silvio Ronaldo's Twitter" /></a>
<a href="https://br.linkedin.com/in/silvio-ronaldo77"><img src="https://img.shields.io/badge/-Silvio-blue?style=flat&logo=Linkedin&logoColor=white" alt="Silvio Ronaldo's LinkedIn" /></a></p></br>


<h2>⚖️ Licença</h2>
<p><strong>Mara Detetive is MIT licensed, as found in the <a href="./LICENSE">LICENSE file</a>.</strong></p>




