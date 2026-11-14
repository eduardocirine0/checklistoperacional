# Checklist de Visitas Operacionais — Ambipar

Formulário de visita operacional que roda inteiro no navegador e gera o
relatório em PDF e o e-mail para a diretoria. Publicado como site estático
no GitHub Pages: https://eduardocambipar.github.io/checklistvisitas/

## Arquivos do repositório

Todos ficam na **raiz**, na mesma pasta. Nenhum pode ser renomeado.

| Arquivo | Para que serve |
|---|---|
| `index.html` | O formulário inteiro: perguntas, rascunho automático, gerador de PDF e montagem do e-mail. Único arquivo que muda a cada atualização. |
| `sw.js` | Faz o formulário abrir e funcionar sem sinal, em pátio e galpão. |
| `manifest.webmanifest` | Nome e ícone do atalho na tela de início do celular. |
| `apple-touch-icon.png` | Ícone do atalho no iPhone e iPad (180 px). |
| `icon-192.png` / `icon-512.png` | Ícones do atalho no Android. |
| `favicon-32.png` | Ícone da aba do navegador. |
| `teste.html` | Página de diagnóstico da exportação. Abra em `/teste.html` no celular que dá problema para descobrir por que o Outlook não aparece. Não é usada pelo formulário e pode ficar fora da publicação final. |

## Antes de publicar: preencher os e-mails

No `index.html`, por volta da linha 1239, está o bloco de configuração:

```js
var CONFIG = {
  emailPara: '',   // e-mails da diretoria, separados por vírgula
  emailCc: ''      // seu e-mail (alimenta a planilha de controle)
};
```

Com os campos vazios, o e-mail abre sem destinatário e a planilha de
controle não recebe os registros.

Se o repositório for público, esses endereços ficam visíveis para quem
abrir o código. Para não expor, deixe em branco e digite os destinatários
no Outlook, ou mantenha o repositório privado.

## Regra importante a cada atualização

Sempre que subir um `index.html` novo, **troque o número da versão do
cache** no `sw.js`, na linha:

```js
var CACHE = 'checklist-v10';
```

Passe para `checklist-v11`, `v12` e assim por diante. Sem isso, quem já
abriu o formulário continua vendo a versão antiga guardada no aparelho,
mesmo depois da publicação.

## Como atualizar pelo navegador

1. Abrir o repositório no GitHub.
2. Clicar em **Add file → Upload files**.
3. Arrastar o `index.html` e o `sw.js` (ou todos, se for a primeira vez).
4. Confirmar em **Commit changes**.
5. Esperar um ou dois minutos até o GitHub Pages publicar.
6. No celular, abrir o formulário e puxar a tela para baixo para recarregar.

## O que o formulário faz sem internet

As bibliotecas que geram o PDF e a fonte Neo Sans vão embutidas no
`index.html`. O formulário abre, preenche, salva o rascunho e gera o PDF
mesmo sem sinal. Só o envio do e-mail precisa de rede.

A única função que ainda busca algo na internet é o botão "Baixar Excel".
Sem rede, ele baixa a planilha em CSV, que o Excel abre do mesmo jeito.

## Onde ficam os dados

Nada é enviado a servidor externo. O rascunho fica no próprio aparelho de
quem preenche e é apagado ao clicar em "Limpar formulário" ou depois de 7
dias sem uso. Os relatórios saem como arquivo e seguem pelo Outlook da
empresa.

## Ambiente de testes

Se publicar uma cópia em outro repositório ou pasta para testar antes,
troque o nome do cache no `sw.js` da cópia:

```js
var CACHE = 'checklist-teste-1';
```

Os dois endereços ficam no mesmo domínio `eduardocambipar.github.io` e
dividem o mesmo armazenamento de cache do navegador. Com nomes diferentes,
limpar o cache do teste não apaga o da versão que a equipe usa.
