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

---

## Novidades desta versão (v2)

- **Resumo Geral** — nova primeira aba com dashboard consolidado da Obra (progresso por setor e por bloco) e da Cliente (aprovação, revistoria, etc.).
- **Vistoria · Obra — Visão geral** — botão "Visão geral (todos os setores)" mostra as 4 frentes (Acabamento, Instalações, Qualidade, Assist. Técnica) empilhadas na mesma tela, além do modo "Por frente" tradicional.
- **Revistoria na Cliente** — o apartamento do cliente agora tem o status **Revistoria** (laranja), além de Não liberado / Agendado / Aprovado / Reprovado.
- **Acessos & Logs** — tela de login (usuário/senha), níveis **Admin** (edita) e **Visitante** (só visualiza), página de Acessos para o admin cadastrar usuários, e registro de **logs** (data/hora, usuário e alteração feita).

### Planilha — novas abas (criadas automaticamente pelo Apps Script)

- **ACESSOS** — colunas: `usuario`, `senha`, `nivel` (admin/visitante), `nome`, `ativo`. Já vem com um usuário inicial `admin` / senha `admin` (troque depois).
- **LOGS** — colunas: `data`, `usuario`, `detalhe`. Preenchida automaticamente a cada login e alteração de status.

Basta atualizar o código do Apps Script (engrenagem ▸ Copiar código) e reimplantar. As abas OBRA e CLIENTE continuam funcionando igual.

> Observação de segurança: o controle de acesso é básico (senhas em texto na planilha), adequado para uso interno da equipe — não use senhas importantes.
