# PadoCard
### Aqui eu vou explicar o que tem no bot e o que pode ser feito em cada âmbito. Não estou mais responsável pela manutenção do bot.

# Tecnologias
- Go 1.22^
- Python 3.12^
- Qualquer distro linux com o ambiente configurado para rodar o python e a API
- PostgreSQL 14^

# Como rodar
- É necessário apenas trocar as informações sensíveis (token do bot, token do livepix), inicializar o binário (jogue em background) e inicializar o bot com o comando do python (também deixe em background).
- Para deixar em background use nohup ou ferramentas do gênero. Pode até também transformar em um daemon configurando ele para iniciar no systemd sempre que reiniciar e etc.
- Infelizmente não há uma instalação ou inicialização automática. Um .sh deve funcionar a curto prazo, pois se a ideia for adicionar cada vez mais coisas, fica inviável deixar o desenvolvimento engessado ao ponto de ter algo tão simples como inicialização de uma forma que precise de intervenção manual constante.

# A API 
- Escrita em Go, a API é composta por um simples servidor HTTP (porém, performático) de baixo consumo de recursos.
- A API receberá chamadas locais do bot, onde cada chamada é feita dentro do localhost. Não há autenticação para realizar as chamadas da API, pois somente o bot fará isso e nenhum serviço externo terá acesso a não ser o livepix, pois é necessário para que ele receba as atualizações via webhook das doações.
- Não há muito o que se mexer na API, somente usá-la, pois caso precise criar comandos especiais que façam coisas específicas, pode combinar chamadas (criar usuario, criar admin, criar obra, carta, etc) para formar novos comandos com o bot em python.
- Existe o serviço HTTP do banco de dados onde o bot acessa as informações e o serviço de webhook, onde recebe as atualizações do livepix como supracitado.
- O deploy do binário é simples, quase não vai sentir trabalho com o bixo, apenas preocupe-se em usá-lo.

# O bot em Python
- O bot em python é separado por camadas:
  1. Inicialização com os comandos.
  2. Classes dos paths, onde cada classe terá os métodos para utilizar da API (não é necessário fazer mais nada, pois, somente precisa-se chamar os métodos e passar os parâmetros pedidos para que a operação seja realizada).
  3. utilidades extras, onde são métodos simples que fazem coisas específicas, por exemplo, formatar o texto para ser mostrado no telegram, formatar botões para que fiquem alinhados e relacionados, etc).
