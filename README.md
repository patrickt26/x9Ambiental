# X9 Ambiental

> Projeto de TCC desenvolvido em 2019 na faculdade.
> O código está preservado como registro desse trabalho e não recebe manutenção desde então.

O **X9 Ambiental** é um aplicativo para denunciar crimes ambientais. A pessoa abre o app, vê no mapa as denúncias feitas perto dela e registra uma nova: escolhe o tipo de crime, o tipo de área, marca o local no mapa e descreve o que viu.

## Funcionalidades

- Cadastro e login de usuários, com autenticação por token (JWT)
- Mapa com a localização atual e as denúncias registradas por perto
- Nova denúncia em etapas: tipo de crime, tipo de área, local no mapa e confirmação
- Endereço obtido automaticamente a partir das coordenadas (geocodificação reversa)
- Feed com as denúncias e tela de detalhe de cada uma
- Perfil do usuário

Tipos de crime cadastrados: queimada, desmatamento, despejo inadequado de lixo e maus-tratos com animais.
Tipos de área: mata, área urbana e corpos d'água (lagos, rios etc.).

<!-- Prints do app: adicionar aqui, se houver -->

## Estrutura do repositório

```
x9Ambiental/
├── backend/   API REST em Node.js
└── mobile/    App em React Native
```

Os dois projetos viviam em repositórios separados (`x9Ambiental-backend` e `x9Ambiental-mobile`) e foram reunidos aqui com o histórico de commits preservado.

## Stack

**Backend** (`backend/`)
- Node.js e Express
- PostgreSQL com Sequelize (migrations e seeds)
- Autenticação com JWT e senhas com bcrypt
- Validação com Yup
- ESLint (Airbnb) e Prettier

**Mobile** (`mobile/`)
- React Native 0.61
- React Navigation (pilha e abas)
- Redux, Redux Saga e Redux Persist
- react-native-maps, geolocalização e geocodificação com a API do Google
- Styled Components
- Axios

## API

| Método | Rota | Descrição |
|---|---|---|
| POST | `/users` | Cria usuário |
| POST | `/sessions` | Login (retorna o token) |
| PUT | `/users/:id` | Atualiza usuário |
| GET / POST | `/reports` | Lista e cria denúncias |
| PUT / DELETE | `/reports/:id` | Atualiza e remove denúncia |
| GET / POST | `/crimeTypes` | Tipos de crime |
| PUT | `/crimeTypes/:id` | Atualiza tipo de crime |
| GET / POST | `/crimeZones` | Tipos de área |
| PUT | `/crimeZones/:id` | Atualiza tipo de área |

Todas as rotas, exceto cadastro e login, exigem o cabeçalho `Authorization: Bearer <token>`.

## Como rodar

As dependências são de 2019, então o projeto pode precisar de ajustes para rodar em ferramentas atuais (Node 10 a 12, React Native 0.61).

**Backend**

```bash
cd backend
cp .env.example .env    # preencha APP_SECRET e os dados do Postgres
yarn
yarn sequelize db:migrate
yarn sequelize db:seed:all
yarn dev
```

**Mobile**

```bash
cd mobile
cp .env.example .env    # informe GOOGLE_API_KEY
yarn
yarn android
```

A chave do Google também precisa ir em `android/app/src/main/AndroidManifest.xml` (`com.google.android.geo.API_KEY`), e o endereço da API fica em `src/services/api.js`.

## Autor

Patrick Thomaz ([@patrickt26](https://github.com/patrickt26))
