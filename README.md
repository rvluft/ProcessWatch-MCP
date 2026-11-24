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

O ProcessWatch que alguém cria no ChatGPT fica só na conta de quem criou:
outra pessoa não o acha procurando. Por isso há dois caminhos.

**A empresa já publicou** (só existe em conta de empresa do ChatGPT: Business,
Enterprise ou Edu): nos plugins, abra a aba com o nome da empresa, procure
ProcessWatch, instale, entre com a conta do ProcessWatch e clique em **Aprovar
a conexão**.

**Conta Plus ou Pro, ou a empresa não publicou**: cada pessoa cria a sua.

1. abrir os plugins do ChatGPT, em <https://chatgpt.com/plugins>;
2. desligar o treino: **Settings** > **Data controls** > **Improve the model for
   everyone** (nos planos Free, Plus e Pro a OpenAI treina com as conversas,
   inclusive com o que o ProcessWatch responder, se isso estiver ligado);
3. clicar em **Add** e escolher **Add custom MCP server**;
4. em **Icon**, enviar o ícone do ProcessWatch (`docs/icone-processwatch.png`,
   ou o botão de baixar no guia; depois de criado, o ChatGPT não oferece
   trocar), preencher `ProcessWatch` em **Name**, o endereço
   `https://app.processwatch.com.br/api/mcp` em **Server URL** (na parte
   **Connection**) e **OAuth** em **Authentication**;
5. marcar **I understand and want to continue** e clicar em **Create as a plugin**;
6. entrar com a conta do ProcessWatch e clicar em **Aprovar a conexão**.

Conferido na tela do ChatGPT em 19/11/2026, numa conta Plus.

## Para quem administra o ChatGPT da empresa

Isto se faz uma vez, por um administrador do espaço de trabalho. Há dois
caminhos.

### Opção 1: criar e publicar pelo ChatGPT

É a opção para a equipe usar no navegador. Pela documentação da OpenAI, criar
a ligação existe nas contas Business, Enterprise e Edu (no Business, só
administradores e donos criam e publicam) e na conta Pro; em 19/11/2026 ela
apareceu também numa conta Plus. Para publicar à empresa, a conta precisa das
permissões **Create plugins with MCPs** e **Publish plugins to workspace**.

1. Crie a ligação pelos passos de "Para quem vai usar", até **Create as a plugin**
   (o **Add custom MCP server** fica no botão **Add** de <https://chatgpt.com/plugins>).
2. Na aba **Personal**, abra os três pontos do ProcessWatch, escolha **Publish**
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
ProcessWatch. Quem libera é o suporte do ProcessWatch, pelo e-mail
<suporte@processwatch.com.br>. Sem isso, a tela de aprovar avisa que nada foi
liberado.

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
docs/icone-processwatch.png          o mesmo ícone, para baixar pelo guia
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
- Os botões do caminho de quem vai usar foram conferidos na tela do ChatGPT em
  19/11/2026 (conta Plus); os do administrador vêm da documentação da OpenAI de
  17/11/2026. Se a tela mudar, o guia e este arquivo mudam juntos.
