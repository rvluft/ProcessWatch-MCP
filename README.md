# ProcessWatch para o ChatGPT

Este repositório é o plugin que liga o ChatGPT ao ProcessWatch. Com ele
instalado, a pessoa pergunta ao ChatGPT sobre os processos de licenciamento da
empresa ("quais estão parados há mais de 30 dias?") e o ChatGPT consulta o
ProcessWatch na hora.

É somente leitura. O plugin não encerra processo, não muda obra e não pede
verificação.

## Para quem vai usar

Abra o guia, que tem o passo a passo com os botões:
<https://rvluft.github.io/ProcessWatch-MCP/>. É esse o endereço para mandar à
equipe.

Em resumo, são três cliques e uma senha:

1. abrir os plugins do ChatGPT, em <https://chatgpt.com/plugins>;
2. na aba com o nome da empresa, achar **ProcessWatch** e clicar no **+**;
3. entrar com a conta do ProcessWatch e clicar em **Aprovar a conexão**.

## Para quem administra o ChatGPT da empresa

Isto se faz uma vez, por um administrador do espaço de trabalho. Há dois
caminhos.

### Opção 1: criar e publicar pelo ChatGPT

É a opção para a equipe usar no navegador. A conta precisa das permissões
**Create plugins with MCPs** e **Publish plugins to workspace**.

1. Em <https://chatgpt.com/plugins>, clique no **+** e escolha **Add custom MCP server**.
2. Dê o nome `ProcessWatch`. Em **Connection**, ponha em **Server URL** o
   endereço `https://app.processwatch.com.br/api/mcp`. Na autenticação, escolha
   **OAuth**.
3. Clique em **I understand and want to continue** e em **Create as a plugin**.
4. Na aba **Personal**, abra os três pontos do ProcessWatch, escolha **Publish**
   e diga quais perfis da empresa podem usar.

Por este caminho a skill não vai junto. O ChatGPT consulta do mesmo jeito,
guiado pela descrição que o próprio servidor dá de cada consulta.

### Opção 2: importar este repositório

É a opção para a equipe que usa o aplicativo do ChatGPT para computador. Traz
junto a skill, que ensina o ChatGPT a consultar e a mostrar as respostas, e
atualiza sozinho: o ChatGPT confere o repositório todo dia.

1. Abra **Admin** > **Plugins** e escolha **Add** > **Import marketplace**.
2. Em **Source**, cole `https://github.com/rvluft/ProcessWatch-MCP`, só o
   endereço, sem pasta nem branch. Deixe **Path** e **Branch, tag, or commit**
   vazios.
3. Clique em **Import marketplace** e autorize o acesso ao GitHub.
4. Em **Import results**, abra o ProcessWatch e escolha, em **Installation
   policy**, quais perfis podem instalar. A política que está no catálogo deste
   repositório não é aplicada na importação: vale a que você escolher aqui.

Conte com o aviso **Desktop only**. A documentação do ChatGPT diz que o plugin
importado que traz a ligação dentro dele pode receber esse aviso, e este é
desse tipo. Com ele, a pessoa acha o plugin no navegador, mas só instala e usa
pelo aplicativo do ChatGPT para computador, e no celular ele não aparece. Se a
equipe usa o navegador, fique com a opção 1.

### Antes de a equipe usar

A consulta por aplicativo precisa estar liberada para a empresa no
ProcessWatch. Quem libera é o suporte do ProcessWatch. Sem isso, a tela de
aprovar avisa que nada foi liberado.

## O que o ChatGPT vê

Vê o número do protocolo, a obra, a cidade e o portal de cada processo; a
classe e há quantos dias ele está parado; as mudanças detectadas, com tipo,
gravidade e data; e os conectores que não estão lendo.

Não saem do ProcessWatch os campos de proprietário, endereço e inscrição
imobiliária, o nome de servidor da prefeitura, o texto dos andamentos e
despachos, os anexos, e os logins e senhas dos portais.

Cada pessoa liga a própria conta e aprova o acesso numa tela do painel. Para
desligar: painel do ProcessWatch, **Configurações**, **Aplicativos
conectados**, **Desconectar**.

## O que tem aqui

```text
.agents/plugins/marketplace.json     o catálogo que o ChatGPT importa
plugins/processwatch/
  plugin.json                        nome, descrição e ícone do plugin
  mcp.json                           o endereço do ProcessWatch e a forma de login
  skills/processwatch/SKILL.md       como consultar e como responder
  assets/icone.png
docs/index.html                      o guia de quem vai usar
```

O pacote segue o formato Agent Plugins 1.0 e não leva senha, chave nem dado de
cliente. O login é de cada pessoa, feito no próprio ProcessWatch.

## Para quem mantém

- **Não edite nada aqui.** Este repositório é montado a partir do repositório
  principal do ProcessWatch, onde um teste confere a skill contra o servidor e
  o guia contra o painel. Mude lá e monte de novo por cima do clone deste:
  `python3 scripts/montar-plugin.py <pasta deste clone>`.
- **Mudou a skill ou o `plugin.json`?** Suba a versão em `plugin.json`, para
  ficar registrado o que mudou. Quem importou recebe a mudança na sincronização
  diária, ou na hora, em **Admin** > **Plugins** > **Marketplaces** >
  **Sync now**.
- **O guia é servido pelo GitHub Pages**, da branch principal, pasta `/docs`
  (em **Settings** > **Pages**).
- Os nomes dos botões do ChatGPT estão como na documentação da OpenAI de
  17/11/2026. Se a tela mudar, o guia e este arquivo mudam juntos.
