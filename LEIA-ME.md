# Vistorias · Alto do Jerivá — App

Ferramenta de **Gestão à Vista** para controle de vistorias, no padrão visual da Construtora Engertal / Alto Mangueiral. Funciona como site (desktop e celular) e pode ser empacotada como **aplicativo iOS/Android** com o Capacitor.

## O que tem

- **Aba Vistoria · Obra** — liberação **por apartamento**. Selecione a frente de serviço (Acabamento, Instalações, Qualidade, Assistência Técnica) e toque em cada apartamento para registrar o status. O fluxo é: Acabamento + Instalações liberam → Qualidade → Assistência Técnica.
- **Aba Vistoria · Cliente** — mapa de aprovação por apartamento (Não liberado, Agendado, Aprovado, Reprovado), com Resumo Geral e Percentual de Aprovação.
- **Toque no apartamento → menu de opções** (igual nas duas abas).
- **Layout mobile** com barra de navegação inferior e visualização por bloco (formato de aplicativo).
- **Google Sheets** — botão de engrenagem no topo para conectar a planilha (ler e gravar em tempo real).
- **Exportar / Importar** — JSON e CSV para backup.

## Usar como site (rápido)

Abra `www/index.html` no navegador, ou hospede a pasta `www/` em qualquer servidor (Google Sites, GitHub Pages, Netlify, etc.). A conexão com o Google Sheets só funciona quando hospedado/aberto num navegador real (não dentro de pré-visualizações).

## Empacotar como app (Capacitor)

Pré-requisitos: Node.js LTS. Para Android: Android Studio. Para iOS: Mac com Xcode.

```bash
# 1) na pasta do projeto
npm install

# 2) inicializar o Capacitor (só na primeira vez)
npx cap init "Vistorias Jeriva" br.com.engertal.vistorias --web-dir=www

# 3) adicionar as plataformas
npx cap add android
npx cap add ios        # somente no Mac

# 4) sempre que alterar o app (www/index.html), sincronize
npx cap sync

# 5) abrir no Android Studio / Xcode para rodar ou gerar o APK/IPA
npx cap open android
npx cap open ios
```

Gerar o APK: no Android Studio → *Build ▸ Build Bundle(s)/APK(s) ▸ Build APK(s)*.

## Conectar ao Google Sheets

1. Abra a planilha → **Extensões ▸ Apps Script**.
2. Cole o código que aparece no próprio app (botão de engrenagem ▸ "Copiar código") e salve.
3. **Implantar ▸ Nova implantação ▸ App da Web**, acesso **Qualquer pessoa**.
4. Copie a URL `.../exec` e cole no app (engrenagem ▸ campo URL ▸ Conectar).

O app cria/atualiza duas abas na planilha: **OBRA** (bloco, pav, apto, acabamento, instalações, qualidade, assistência) e **CLIENTE** (bloco, pav, apto, status).

## Observação sobre fontes offline

O app usa a fonte **Urbanist** via Google Fonts. Para uso 100% offline no celular, baixe os arquivos da fonte e referencie localmente em `www/` (opcional — sem internet ele usa a fonte padrão do sistema).
