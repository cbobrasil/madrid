# Editar os textos do guia

Você pode escrever seus próprios textos sem editar o HTML:

- **bairros.json**: nomes, subtítulos e conteúdo das fichas dos 13 bairros.
- **locais.json**: nomes, tipos e conteúdo dos 173 locais, inclusive os das suas listas.

Abra o arquivo em um editor de texto, como VS Code. Procure o nome do bairro ou do local. Altere seus textos e salve em UTF-8. Mantenha o `id`: ele liga o texto ao contorno ou ponto correspondente no mapa. Esses arquivos não alteram coordenadas, listas ou cores, nem criam novos pontos.

## Exemplo de bairro

```json
{
  "versao": 1,
  "tipo": "bairros",
  "itens": [
    {
      "id": "lavapies",
      "nome": "Lavapiés",
      "subtitulo": "Meu passeio pelo bairro",
      "secoes": [
        {
          "texto": "Aqui escrevo minha apresentação do bairro."
        },
        {
          "titulo": "O que quero conhecer",
          "itens": [
            "Primeira parada",
            "Segunda parada"
          ]
        },
        {
          "titulo": "Minhas dicas",
          "texto": "Meu texto, do jeito que quero que apareça.\nUma segunda linha."
        }
      ],
      "links": [
        {
          "texto": "Abrir o mapa",
          "url": "https://www.google.com/maps/search/?api=1&query=Lavapies+Madrid"
        }
      ]
    }
  ]
}
```

Você pode adicionar, remover e reordenar as seções. `titulo` é opcional. `texto` cria um parágrafo; `itens` cria uma lista. A ordem das seções e dos itens é a ordem exibida na ficha. Use `\n` dentro do texto para quebrar uma linha.

O arquivo já contém os outros bairros: edite cada item sem apagar os demais. Um arquivo parcial também é aceito; bairros omitidos usam os textos padrão do HTML.

## Exemplo de local

```json
{
  "versao": 1,
  "tipo": "locais",
  "itens": [
    {
      "id": "reference-1",
      "nome": "Puerta del Sol",
      "tipo": "Praça",
      "secoes": [
        {
          "titulo": "Meu plano",
          "texto": "Usar como ponto de encontro antes do passeio."
        },
        {
          "titulo": "Lembrar",
          "itens": [
            "Escolher o próximo destino antes de sair da praça."
          ]
        }
      ],
      "links": []
    }
  ]
}
```

`nome` e `tipo` aparecem ao tocar no ponto. As seções adicionais aparecem abaixo, dentro do mesmo cartão. Os locais começam com `secoes: []`, preservando a apresentação simples de nome e tipo até você adicionar seus textos.

Para editar outro local, encontre seu item no arquivo existente e mantenha o respectivo `id`, inclusive quando ele começar com `google-`.

## Ver suas edições

**Com servidor local ou no GitHub Pages:** o HTML lê os dois JSONs automaticamente a cada abertura ou atualização. Para usar no seu computador, execute na pasta `madrid`:

```powershell
python -m http.server 8000 --bind 127.0.0.1
```

Abra <http://localhost:8000/>. Depois de salvar os JSONs, atualize a página.

**Abrindo `index.html` com dois cliques:** o navegador restringe a leitura automática de arquivos JSON vizinhos. Na parte inferior da lista, abra **Meus textos → Carregar textos JSON** e selecione `bairros.json`, `locais.json` ou os dois juntos. Faça isso novamente depois de editar ou reabrir a página. A importação aplica os textos à página aberta; não grava alterações nos seus arquivos.

Sem arquivos externos carregados, o guia continua mostrando os textos padrão incorporados ao HTML. Um erro de leitura ou de formato é informado em **Meus textos**.

## Formato

- `versao` deve continuar como `1`; o `tipo` principal deve continuar como `bairros` ou `locais`.
- JSON usa aspas duplas e não aceita comentários nem vírgula depois do último item.
- Escreva parágrafos normais. Markdown e HTML dentro de `texto` aparecem como texto, sem formatação especial.
- Para remover o conteúdo de uma ficha, mantenha seu item e use `secoes: []` e `links: []`.
- Links usam `texto` e `url`; use endereços HTTP ou HTTPS completos.
- Os textos desses arquivos fazem parte do site quando ele for publicado.
