# Estylize — Móveis Sob Medida

Landing page de página única, sem build step: um `index.html` autocontido
(CSS e JS inline, imagens em WebP base64). Publicada na Vercel como site estático.

## Estrutura

```
index.html     página completa (~272 KB)
og.jpg         imagem de compartilhamento 1200×630
robots.txt
sitemap.xml
vercel.json    headers de segurança, cache e clean URLs
```

## Deploy

Qualquer push na branch `main` publica automaticamente na Vercel.
Não há dependências, nem `npm install`, nem etapa de build.

## Seção "Montagem do armário"

As 14 peças do render 3D são posicionadas em porcentagem do canvas 717×983.
As coordenadas vieram de template matching (OpenCV) de cada peça contra o
render final — todas casaram com score 1.0000, então a animação de explosão
remonta exatamente sobre o render.

As portas usam uma homografia resolvida em runtime (eliminação gaussiana 8×8)
que mapeia o plano das portas sobre os 4 cantos do vão medidos no render:
`(176,72) (945,17) (945,1218) (178,1044)`. O resultado vira uma `matrix3d`,
recalculada a cada resize. Se o render for trocado, esses 4 pontos e o
`layout.json` das peças precisam ser refeitos.

## Pontos de manutenção

- **WhatsApp**: constante `WHATS` no script (final do `index.html`) e os links
  `wa.me` no corpo. Hoje: `5547984590669`.
- **Domínio**: `canonical`, Open Graph, `sitemap.xml`, `robots.txt` e o
  `@id`/`sameAs` do JSON-LD apontam para o domínio de produção.
- **Fotos**: as imagens de ambiente vêm do Unsplash via URL. Ao trocar por
  fotos reais dos projetos, hospedar localmente e ajustar o `img-src` da CSP.
