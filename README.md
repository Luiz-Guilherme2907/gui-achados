# gui achados

Página "link na bio" com os achados que o Gui testou e aprova: https://guiachados.vercel.app

É HTML, CSS e JS puro em um arquivo só (`index.html`), sem build e sem dependência além do Google Fonts. Fica hospedada na Vercel, que publica sozinha cada push na `main`.

## Como atualizar os produtos

Os produtos vêm de uma planilha do Google. A página lê o CSV publicado, então pra adicionar achado não precisa mexer no código.

1. No Google Sheets: Arquivo > Importar > `modelo-planilha.csv`.
2. Troque os exemplos pelos seus achados, um produto por linha.
3. Arquivo > Compartilhar > Publicar na Web > escolha a aba > formato CSV > Publicar. Copie o link.
4. Cole o link na linha `const PLANILHA = "..."`, no começo do `index.html`, e envie a mudança pro GitHub (commit + push). Em um minuto a Vercel publica.

Depois de editar a planilha, a página pode levar uns 5 minutos pra mostrar a mudança, que é o tempo que o Google leva pra republicar.

## Colunas da planilha

| coluna | exemplo | observação |
|---|---|---|
| numero | 18 | obrigatória. É o número que você fala no vídeo |
| nome | mini processador de alho | obrigatória |
| link | https://s.shopee.com.br/... | obrigatória, começando com https:// |
| loja | shopee | mercadolivre, shopee, amazon, tiktokshop, magalu ou aliexpress. Outra loja aparece do jeito que você escrever |
| categoria | cozinha | vira os chips de filtro |
| preco / precoantigo | 29,90 / 59,90 | com vírgula. Na Amazon, deixe vazio (a política de afiliados exige preço atualizado automaticamente) |
| foto | link da imagem | da loja ou do Google Drive. Sem foto, aparece a capa rabiscada com a frase |
| frase | pica alho em 5 segundos | a sua fala no card |
| porque | carrega no usb; lava na torneira | benefícios do modal, separados por `;` |
| video | link do TikTok | mostra o botão "ver o vídeo" |
| destaque | sim | vira o achado do topo. Se nenhum estiver marcado, vai o mais novo |

Cada produto também tem link próprio: `.../#achado-18` já abre o produto, bom pra colocar nos stories.

## Grupo do WhatsApp

O link do grupo fica na linha `const GRUPO_WHATSAPP = "..."`, logo abaixo da planilha, no começo do `index.html`. Ele vale pro aviso em formato de notificação, pro botão "grupo" da barra fixa e pro rodapé.

O aviso desce do topo quando a pessoa passa do começo da página, ou depois de 9 segundos. Quem fecha só vê de novo em 3 dias, e quem toca em "entrar no grupo" não vê mais por 60 dias. Se o modal de um produto estiver aberto, o aviso espera ele fechar.

## Testar

- Abra `index.html?teste` e procure `testes ok` no console do navegador.
- Pra ver no computador, rode `python -m http.server` na pasta e abra http://localhost:8000. Abrindo o arquivo direto, a página não consegue ler a planilha.
