# Guia Madrid por bairros

Mapa estático para a viagem de **13/11/2026 a 16/11/2026**, com regiões coloridas e pontos de interesse em espanhol.

## Abrir no computador

Abra `index.html` no Firefox ou em outro navegador. É necessário acesso à internet para carregar a biblioteca do mapa e o fundo do OpenFreeMap.

Para conferir alterações, atualize a página com **Ctrl + F5**.

Se preferir um endereço local, execute nesta pasta:

```powershell
python -m http.server 8000 --bind 127.0.0.1
```

Depois abra <http://localhost:8000/>. Para encerrar o servidor, pressione **Ctrl + C** no terminal.

## Estrutura

```text
madrid/
├── index.html                 # Página, estilos, código e dados do mapa
├── assets/maps/barrios-madrid.kml # Cópia do mapa desenhado no Google My Maps
├── .github/workflows/pages.yml # Publicação automática no GitHub Pages
├── .nojekyll                  # Publicação dos arquivos estáticos sem Jekyll
├── .gitattributes             # Padronização dos arquivos de texto
├── .gitignore
└── README.md
```

Não há instalação de pacotes nem etapa de compilação. As regiões e os locais ficam no bloco `map-data` do `index.html`.

Os contornos atuais vêm do arquivo `Barrios Madrid.kmz`, enviado pelo usuário. Os 13 polígonos foram incorporados ao HTML sem simplificar suas coordenadas; a cópia do KML está em `assets/maps/barrios-madrid.kml`. O navegador usa os dados incorporados, por isso o HTML continua abrindo diretamente como arquivo local.

As sobreposições do desenho original foram preservadas, inclusive entre Lavapiés e Embajadores. `Palace` e `Ambassadors` aparecem no guia como `Palacio` e `Embajadores`. Os nomes originais permanecem no campo `sourceName` de cada região. As regiões `Las Literras` e `Las Letras` permanecem separadas, com os nomes e contornos do arquivo recebido, conforme confirmado pelo usuário.

## Publicar depois no GitHub Pages

A estrutura está preparada; nenhum repositório remoto ou site foi criado por esta configuração.

1. Crie um repositório no GitHub, por exemplo `madrid`. Para usar o GitHub Pages com o plano gratuito, use um repositório público.
2. Envie os arquivos desta pasta para a branch `main`, incluindo `.github/workflows/pages.yml` e `.nojekyll`. Isso pode ser feito pelo GitHub Desktop ou por Git.
3. No repositório, abra **Settings → Pages → Build and deployment → Source** e selecione **GitHub Actions**.
4. Em **Actions → Publicar no GitHub Pages**, use **Run workflow** na branch `main` para a primeira publicação, caso o envio inicial tenha ocorrido antes da configuração do Pages.
5. Aguarde o fluxo terminar. O endereço publicado aparece em **Settings → Pages** e no resultado da execução.

O endereço de um repositório chamado `madrid` normalmente será:

```text
https://SEU-USUARIO.github.io/madrid/
```

Depois da configuração inicial, alterações em `index.html`, `assets/`, `.nojekyll` ou no próprio workflow enviadas para `main` publicam uma nova versão automaticamente. Também é possível publicar manualmente pela aba **Actions**.

O workflow publica somente `index.html`, `.nojekyll` e a pasta `assets/`. Ao adicionar arquivos ao site, use caminhos relativos, como `assets/arquivo.json`, para funcionar também no subdiretório `/madrid/`.

Os arquivos incorporados ao HTML ou colocados em `assets/` fazem parte do conteúdo público publicado. Para futuras listas do Google Maps, separe a exportação original dos dados que você decidir incluir no guia.

## Mapa e fontes

- Biblioteca: [MapLibre GL JS](https://maplibre.org/).
- Fundo: [OpenFreeMap](https://openfreemap.org/), com dados do OpenStreetMap e OpenMapTiles. As atribuições aparecem no mapa.
- Contornos: mapa pessoal `Barrios Madrid`, desenhado pelo usuário no Google My Maps. Os desenhos pessoais substituíram as aproximações anteriores e não são apresentados como limites administrativos oficiais.

Referência da configuração de publicação: [documentação do GitHub Pages com GitHub Actions](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).
