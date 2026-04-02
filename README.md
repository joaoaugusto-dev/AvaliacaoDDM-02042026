# Avaliação DDM — Projeto Flutter (Splash, Login, Cadastro e Home)

## 1) Identificação do grupo

- Disciplina: Desenvolvimento para Dispositivos Móveis (DDM)
- Atividade: Projeto Flutter com dados mockados em memória
- Integrantes:
  - 25001227 - Isadora Cabral dos Santos
  - 25000019 - João Augusto de Freitas
  - 25000795 - Kauan Leander Leandrini

## 2) Link de entrega

- Repositório público no GitHub: https://github.com/joaoaugusto-dev/AvaliacaoDDM-02042026

## 3) Objetivo do projeto

Aplicativo desenvolvido para demonstrar os conceitos da disciplina:

- organização arquitetural (views, viewmodels, models)
- navegação entre telas
- formulários com validação
- autenticação simulada
- uso de dados mockados em memória com Model + List

## 4) Arquitetura adotada

Estrutura atual utilizada no projeto:

```text
lib/
├── main.dart
├── app/
│   ├── app_widget.dart
│   ├── core/
│   └── routes/
├── features/
│   ├── auth/
│   │   ├── data/
│   │   │   ├── user_mock_store.dart
│   │   │   └── user_repository.dart
│   │   ├── model/
│   │   │   └── user_model.dart
│   │   ├── view/
│   │   │   ├── splash_page.dart
│   │   │   ├── login_page.dart
│   │   │   └── register_page.dart
│   │   └── viewmodel/
│   │       ├── splash_viewmodel.dart
│   │       ├── login_viewmodel.dart
│   │       └── register_viewmodel.dart
│   └── home/
│       └── view/
│           └── home_page.dart
```

Resumo da organização:

- View: interface e widgets das telas
- ViewModel: validações e regras de fluxo
- Model: estrutura de dados do usuário
- Data: repositório e store mockado em memória

## 5) Fluxo da aplicação

1. App inicia na SplashScreen.
2. Splash aguarda alguns segundos e redireciona para Login.
3. Usuário pode entrar com credenciais válidas. (Se forem inválidas, retorna um feedback ao usuário por SnackBar)
4. Se não tiver conta, abre Cadastro.
5. Cadastro salva usuário em memória.
6. Usuário retorna ao Login.
7. Login correto abre Home.

## 6) Critérios obrigatórios (critério a critério)

### 6.1 Estrutura arquitetural


- Evidências:
  - Separação por camadas: view / viewmodel / model / data.
  - Lógica de autenticação/cadastro fora da interface.
  - Repositório dedicado para acesso aos dados mockados.
- Arquivos de referência:
  - lib/features/auth/view/
  - lib/features/auth/viewmodel/
  - lib/features/auth/model/user_model.dart
  - lib/features/auth/data/user_repository.dart

Arquitetura de pastas no VS Code:

<img width="306" height="754" alt="image" src="https://github.com/user-attachments/assets/b07f3040-c299-479a-860d-9ccfa74b35c5" />

---

### 6.2 Tela Splash


- Evidências:
  - É a primeira rota definida em `initialRoute`.
  - Usa widgets básicos e layout com Container, Column, Row, alinhamento e espaços.
  - Navega para Login após tempo de espera.
- Arquivos de referência:
  - lib/app/app_widget.dart
  - lib/features/auth/view/splash_page.dart
  - lib/features/auth/viewmodel/splash_viewmodel.dart

Splash:

<img width="300" alt="Screenshot_1775147883" src="https://github.com/user-attachments/assets/31335619-2f68-4418-abf5-ee119bd63f65" />

### 6.3 Tela de Login


- Evidências:
  - Campo de e-mail.
  - Campo de senha.
  - Botão Entrar.
  - Botão/texto para ir ao cadastro.
  - Validação básica dos campos.
  - Busca de usuário na estrutura mockada em memória.
  - Login só autorizado com credenciais corretas.
- Arquivos de referência:
  - lib/features/auth/view/login_page.dart
  - lib/features/auth/viewmodel/login_viewmodel.dart
  - lib/features/auth/data/user_repository.dart

Tela de login:

<img width="300" alt="Screenshot_1775147886" src="https://github.com/user-attachments/assets/4842b50e-8333-4e50-bdd0-6568a2a23f43" />


Validação/erro de login inválido:

<img width="300" alt="Screenshot_1775148037" src="https://github.com/user-attachments/assets/fe201f38-f572-4255-9a02-8639d12e038e" />


---

### 6.4 Tela de Cadastro


- Evidências:
  - Campos para nome, e-mail, senha e confirmação.
  - Validação de formulário.
  - Botão para salvar cadastro.
  - Dados adicionados em lista mockada em memória com Model.
- Arquivos de referência:
  - lib/features/auth/view/register_page.dart
  - lib/features/auth/viewmodel/register_viewmodel.dart
  - lib/features/auth/data/user_mock_store.dart

Tela de cadastro:

<img width="300" alt="Screenshot_1775147889" src="https://github.com/user-attachments/assets/e3b921d4-4f1e-439b-a858-f6c34ea1d826" />


Cadastro realizado com sucesso:

<img width="300" alt="Screenshot_1775147921" src="https://github.com/user-attachments/assets/bae9c724-5eff-478a-b296-95cd95a5d57e" />

---

### 6.5 Uso de Model


- Evidências:
  - Model `UserModel` com os dados do usuário.
  - Campos: id, name, email, password.
- Arquivo de referência:
  - lib/features/auth/model/user_model.dart

Código do model:

<img width="547" height="829" alt="image" src="https://github.com/user-attachments/assets/0e680178-d082-4fd3-8002-c1f6feb94adf" />


---

### 6.6 Uso de dados mockados


- Evidências:
  - Armazenamento somente em memória.
  - Uso de `List<UserModel>` no store mockado.
  - Sem banco de dados, sem API externa e sem Firebase.
- Arquivo de referência:
  - lib/features/auth/data/user_mock_store.dart

Lista mockada de usuários:

<img width="588" height="425" alt="image" src="https://github.com/user-attachments/assets/522ca22b-177a-4f6f-b22c-7f261ce2caba" />


---

### 6.7 Compartilhamento dos dados entre telas


- Evidências:
  - `UserMockStore` com instância singleton (`instance`).
  - Cadastro adiciona usuário no store.
  - Login consulta o mesmo store via repositório.
- Arquivos de referência:
  - lib/features/auth/data/user_mock_store.dart
  - lib/features/auth/data/user_repository.dart

Store/repositório compartilhado:

<img width="580" height="36" alt="image" src="https://github.com/user-attachments/assets/6a502410-758a-44df-b75d-f1502456cad6" />

<img width="520" height="341" alt="image" src="https://github.com/user-attachments/assets/bff281bb-3287-4fd4-b9c7-e7ebefdcebd0" />

<img width="695" height="396" alt="image" src="https://github.com/user-attachments/assets/ca7819d5-9d30-4cf5-a329-b2a5387fa875" />

<img width="791" height="91" alt="image" src="https://github.com/user-attachments/assets/099b4efd-a14a-4d73-9513-d678e2489d5a" />

<img width="379" height="93" alt="image" src="https://github.com/user-attachments/assets/14861651-b37c-476b-9c4f-9b12a64ac19f" />


---

### 6.8 Tela Home


- Evidências:
  - Exibe ícone centralizado.
  - Exibe texto centralizado "Bem-vindo à Home".
  - Exibe saudação com nome do usuário.
- Arquivo de referência:
  - lib/features/home/view/home_page.dart

Home após login:

<img width="300" alt="Screenshot_1775147904" src="https://github.com/user-attachments/assets/c83efc12-a963-4229-9099-b40df1f1dba6" />

## 7) Requisitos técnicos esperados

### 7.1 Uso de StatelessWidget e/ou StatefulWidget


- Evidências:
  - Stateless: HomePage
  - Stateful: SplashPage, LoginPage, RegisterPage

<img width="541" height="92" alt="image" src="https://github.com/user-attachments/assets/4ce1081b-8333-4e13-a9d2-009f35618268" />

<img width="541" height="92" alt="image" src="https://github.com/user-attachments/assets/775dcaa2-8e67-4985-bb64-0d875edde479" />


### 7.2 Navegação por rotas


- Evidências:
  - Rotas nomeadas em AppRoutes.
  - Geração de páginas via AppPages.

<img width="503" height="200" alt="image" src="https://github.com/user-attachments/assets/85282581-d6a6-4568-9444-e88026613f69" />

<img width="612" height="200" alt="image" src="https://github.com/user-attachments/assets/584b752f-0220-4953-a170-28fc7bcd5776" />

### 7.3 Formulários com TextFormField


- Evidências:
  - Login e Cadastro usam TextFormField.

ESPAÇO PARA PRINT:

<img width="788" height="440" alt="image" src="https://github.com/user-attachments/assets/47a3d4c6-c790-4e58-a616-2a39eda4dcd1" />

### 7.4 Validação de formulário


- Evidências:
  - Validações de e-mail, senha, nome e confirmação de senha.

<img width="300" alt="Screenshot_1775149986" src="https://github.com/user-attachments/assets/6f2d98f0-cb75-4b4a-b976-1e05208d44fa" />

<img width="300" alt="Screenshot_1775149978" src="https://github.com/user-attachments/assets/c39a4b16-db4d-4ee3-9cdf-7dd26f4d28e3" />

<img width="300" alt="Screenshot_1775149966" src="https://github.com/user-attachments/assets/b1ab7026-b773-4d76-9207-bd330334a21e" />

<img width="300" alt="Screenshot_1775149954" src="https://github.com/user-attachments/assets/ce2727cd-e7a7-4846-99ad-967becda8603" />

### 7.5 Separação de responsabilidades


- Evidências:
  - Interface separada da lógica de negócio (ViewModel).
  - Persistência simulada isolada em camada data.

<img width="269" height="298" alt="image" src="https://github.com/user-attachments/assets/ad67fe9b-8d2a-4984-9790-09ddbb3565e4" />


### 7.6 Uso de Model


- Evidências:
  - UserModel usado no cadastro, autenticação e store.

<img width="547" height="829" alt="image" src="https://github.com/user-attachments/assets/0e680178-d082-4fd3-8002-c1f6feb94adf" />

### 7.7 Uso de List ou Map


- Evidências:
  - Uso de List<UserModel> no armazenamento em memória.

<img width="682" height="293" alt="image" src="https://github.com/user-attachments/assets/28d68ce0-4152-4e84-a5c7-ca023254c091" />


### 7.8 Organização do projeto em pastas


- Evidências:
  - Estrutura por features e camadas.

<img width="300" alt="Screenshot_1775147883" src="https://github.com/user-attachments/assets/31335619-2f68-4418-abf5-ee119bd63f65" />

### 7.9 Lógica de autenticação simulada


- Evidências:
  - Login compara credenciais com lista mockada.
  - Sessão simulada salva no store.

<img width="580" height="36" alt="image" src="https://github.com/user-attachments/assets/6a502410-758a-44df-b75d-f1502456cad6" />

<img width="520" height="341" alt="image" src="https://github.com/user-attachments/assets/bff281bb-3287-4fd4-b9c7-e7ebefdcebd0" />

<img width="695" height="396" alt="image" src="https://github.com/user-attachments/assets/ca7819d5-9d30-4cf5-a329-b2a5387fa875" />

<img width="791" height="91" alt="image" src="https://github.com/user-attachments/assets/099b4efd-a14a-4d73-9513-d678e2489d5a" />

<img width="379" height="93" alt="image" src="https://github.com/user-attachments/assets/14861651-b37c-476b-9c4f-9b12a64ac19f" />

## 8) Regras da atividade (confirmação)

- [x] Sem Firebase
- [x] Sem banco de dados
- [x] Sem API externa
- [x] Foco em arquitetura, lógica, navegação, formulários e dados em memória
- [X] Todos os integrantes participaram do desenvolvimento

## 9) Entrega e demonstração prática

### 9.1 Itens da entrega

- [X] Link público do código-fonte no GitHub
- [X] Apresentação prática funcionando (Vídeo)
- [x] Explicação breve da arquitetura (neste README)

### 9.2 Demonstração do fluxo solicitado

- [x] Splash
- [x] Login
- [x] Cadastro
- [x] Retorno ao login
- [x] Autenticação correta
- [x] Navegação para home

https://github.com/user-attachments/assets/a1ed310a-f6c1-4298-9238-9671a3b5cfee

## 10) Diferenciais adicionais/opcionais

### 10.1 Mensagem de erro ao login inválido

- Status: [x] Implementado
- Evidência: SnackBar quando credenciais são inválidas.

<img width="300" alt="Screenshot_1775148037" src="https://github.com/user-attachments/assets/5a2efe50-d859-45d7-b6d7-afadef7b930a" />

### 10.2 Mensagem de sucesso ao cadastrar

- Status: [x] Implementado
- Evidência: retorno de mensagem após cadastro e exibição no login.

<img width="300" alt="Screenshot_1775147921" src="https://github.com/user-attachments/assets/2a86da01-54fe-4e21-b16d-feec5c334eed" />

### 10.3 Melhoria visual na Home

- Status: [x] Implementado
- Evidência: layout centralizado com card, ícone, textos e ação de sair.

<img width="300" alt="Screenshot_1775147904" src="https://github.com/user-attachments/assets/8b512ac5-01a1-455d-9c36-a42f8466e8a3" />

### 10.4 Uso organizado de singleton/store mockada

- Status: [x] Implementado
- Evidência: UserMockStore com instância singleton e repositório dedicado.

<img width="588" height="425" alt="image" src="https://github.com/user-attachments/assets/522ca22b-177a-4f6f-b22c-7f261ce2caba" />

## 12) Credenciais para teste rápido

Usuários mockados já existentes:

- Email: marcelo.almeida@unifeob.pro.br
- Senha: unifeob@123

- Email: teste@teste
- Senha: teste@teste

Também é possível criar um novo usuário pela tela de cadastro.

