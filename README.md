# Loba — PWA de Treino da Lana

App mobile-first para acompanhar o protocolo de treino "Team PG / Pedro Gouveia", com
cronômetro de descanso, modo foco tela-a-tela, histórico e evolução de carga.
Feito em React + Vite, funciona 100% offline depois do primeiro acesso, e não
precisa de conta nem backend — todos os dados ficam salvos no próprio celular
(`localStorage`).

## 1. Ver o app rodando agora (sem instalar nada)

A forma mais rápida, direto do celular ou computador:

1. Acesse **https://stackblitz.com**.
2. Clique em **"Create new project" → "Import from ZIP"** (ou arraste a pasta
   descompactada deste projeto para dentro do StackBlitz).
3. O StackBlitz instala tudo sozinho e abre uma prévia ao vivo em segundos.

## 2. Publicar gratuitamente e gerar um link

Depois que o projeto abrir no StackBlitz:

1. No canto superior, clique no botão **"Deploy"**.
2. Escolha **Netlify** (não precisa criar conta separada — pode entrar com o GitHub/Google).
3. Aguarde a publicação. Você vai receber um link do tipo
   `https://loba-treino.netlify.app`.

Esse link já é o seu app publicado — pode compartilhar com você mesma, é só isso.

### Alternativa (se preferir usar o computador com terminal)

```bash
npm install
npm run build
```

Isso gera a pasta `dist/`. Depois:

- Crie uma conta gratuita em **netlify.com** ou **vercel.com**.
- Arraste a pasta `dist/` para o painel do Netlify ("Deploy manually" / "Drag and drop"),
  ou rode `npx vercel` dentro da pasta do projeto e siga as instruções na tela.
- Em segundos você recebe o link público.

## 3. Abrir o link no celular

1. Copie o link recebido (ex: `https://loba-treino.netlify.app`).
2. No celular, abra o **Google Chrome** (Android) ou **Safari** (iPhone).
3. Cole o link na barra de endereço e acesse.

## 4. Adicionar o app à tela inicial

**No Android (Chrome):**
1. Com o site aberto, toque nos **três pontinhos** (menu) no canto superior direito.
2. Toque em **"Adicionar à tela inicial"** (ou vai aparecer um banner automático
   sugerindo instalar — pode tocar em **"Instalar"** direto).
3. Confirme o nome e toque em **"Adicionar"**.

**No iPhone (Safari):**
1. Com o site aberto, toque no ícone de **compartilhar** (o quadrado com seta para cima).
2. Role e toque em **"Adicionar à Tela de Início"**.
3. Toque em **"Adicionar"** no canto superior direito.

Pronto — o ícone "Loba" aparece na tela inicial e abre em tela cheia,
com aparência de aplicativo (sem barra de endereço do navegador).

## 5. Usar offline

Depois do primeiro acesso (com internet), o app salva os arquivos no celular.
Nas próximas vezes, ele abre e funciona mesmo sem internet ou com sinal fraco
na academia — só a primeira vez precisa de conexão.

## 6. Atualizar o app no futuro sem perder o histórico

Seu histórico de treinos, pesos e sequência ficam salvos no **armazenamento do
navegador (localStorage) daquele link específico** — não dependem dos arquivos
do app. Ou seja:

- Se você (ou eu) mudar o código e publicar de novo **no mesmo link/domínio**
  (ex: mesmo projeto no Netlify), o app atualiza sozinho na próxima vez que
  você abrir (o `service worker` busca a versão nova automaticamente) e o
  histórico continua intacto.
- **Evite gerar um link novo** para atualizações — sempre publique por cima do
  mesmo projeto/domínio. Se precisar mesmo trocar de link, seus dados antigos
  ficam presos no link antigo (não é possível "levar" localStorage de um
  domínio para outro).

## Estrutura do projeto

```
src/
  data/workouts.js       → toda a ficha de treino (fiel à imagem original)
  lib/storage.js         → salvar/ler histórico e sessão ativa (localStorage)
  lib/format.js          → formatação de tempo e datas
  context/AppContext.jsx → estado global (navegação, sessão de treino)
  components/            → BottomNav, WorkoutCard, ExerciseCard, RestTimer
  screens/                → Home, WorkoutsList, WorkoutDetail, FocusMode,
                            Completed, History, Progress
public/icons/            → ícones do PWA (192px e 512px)
vite.config.js           → configuração do PWA (manifest.json + service worker)
```

## Observação sobre a categoria "Abdominal" e "Panturrilha"

Na ficha original, esses dois grupos aparecem apenas como orientação de
frequência ("dia sim e dia não"), sem exercícios numerados — os exercícios de
panturrilha já estão dentro dos treinos de Posterior e Glúteo. Por isso, no
app essas duas categorias aparecem como abas informativas, sem inventar
exercícios que não estavam na imagem.
