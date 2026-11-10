# dsh-plugin-index

Índice de plugins (formato 1) do **DeepSeek Harness**: lista bundles que eu publico, para instalar direto pela aba **Discover** do DSH.

```text
https://raw.githubusercontent.com/lcf2212dev/dsh-plugin-index/main/index.json
```

## Como adicionar no DSH

1. Abra **Plugins** na barra lateral.
2. Em **Experimental plugins**, ligue **Custom plugin indexes** — a página passa a ter as abas **Installed** e **Discover**.
3. Abra **Discover** e clique em **Add index source**.
4. Cole a URL acima e confirme.

O DSH busca e valida o índice; a busca, os filtros e o botão **Install** aparecem em seguida. A instalação usa o spec exato da versão (Git com commit fixado), com o diálogo de confiança normal do DSH.

## O que está no índice

| Pacote | Versão | Repositório |
|---|---|---|
| `@dsh-burn-plugins/dsh-bots` (Bits) | 0.4.0 | [dsh-bits](https://github.com/lcf2212dev/dsh-bits) |
| `@dsh-burn-plugins/dsh-claude-delegate` | 0.1.0 | [dsh-claude-delegate](https://github.com/lcf2212dev/dsh-claude-delegate) |
| `@dsh-burn-plugins/dsh-figma-mcp-oauth` | 0.1.0 | [dsh-figma-mcp-oauth](https://github.com/lcf2212dev/dsh-figma-mcp-oauth) |

## Como atualizar uma entrada

O índice fixa o commit que foi publicado. Para soltar uma versão nova:

1. Publique a versão no repositório do plugin e pegue o SHA completo de 40 caracteres do commit.
2. Em `index.json`, adicione um objeto em `versions` com o `version` do `package.json`, o `commit` novo e um `publishTimestamp` (Unix, em segundos).
3. Valide e faça commit/push. O DSH relê o índice (cache de 10 minutos; há botão de refresh no Discover).

O validador é o mesmo do DSH: `parseMarketIndex` de `@deepseek-ai/dsh-plugin-market-index`.

## Formato

[Formato 1](https://github.com/deepseek-ai/deepseek-harness): `format`, `title`, `description`, `metadata` (categorias, labels, sort keys) e `plugins[]`; cada plugin tem `name`, textos localizados, `icon`, `author`, `homepage`, `repository` e `versions[]` com `version`, `publishTimestamp`, `source` (`npm` ou `git` + commit) e `engines.dsh`.

## Licença

[MIT](LICENSE).
