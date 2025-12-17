# 🏛️ PATRI-TECH — Backend Profissional com Django e DRF

Este **estudo dirigido** tem como objetivo **fixar o processo inicial de criação e configuração de um backend profissional**, utilizando **Python, Django, Django REST Framework, Git e GitFlow**.

Ao final deste estudo, você será capaz de **iniciar qualquer projeto backend** aplicando **boas práticas reais de engenharia de software**, desde a estruturação do projeto até a validação da API e documentação.

---

## 🚀 Criação do Servidor Django

Esta seção descreve **como criar e executar o servidor Django desde o zero**, seguindo boas práticas de backend profissional.

---

### 1️⃣ Pré-requisitos

Certifique-se de ter instalado:

* Python 3.10+
* pip (gerenciador de pacotes do Python)
* Git
* Ambiente virtual (venv)

Verifique as versões:

```bash
python --version
pip --version
git --version
```

---

### 2️⃣ Criação do Ambiente Virtual

Crie e ative um ambiente virtual para isolar as dependências do projeto:

```bash
python -m venv venv
```

Ativação:

**Windows**

```bash
venv\Scripts\activate
```

**Linux / macOS**

```bash
source venv/bin/activate
```

---

### 3️⃣ Instalação das Dependências

Com o ambiente virtual ativado, instale os principais pacotes:

```bash
pip install django djangorestframework
```

(Opcional, mas recomendado)

```bash
pip install drf-spectacular
```

---

### 4️⃣ Criação do Projeto Django

Crie o projeto principal:

```bash
django-admin startproject patri_tech
cd patri_tech
```

Estrutura inicial:

```text
patri_tech/
├── manage.py
└── patri_tech/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

---

### 5️⃣ Criação da Aplicação (App)

Crie a aplicação responsável pelo domínio do sistema:

```bash
python manage.py startapp core
```

Adicione o app em `settings.py`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'rest_framework',
    'core',
]
```

---

### 6️⃣ Migrações Iniciais

Crie e aplique as migrações do banco de dados:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

### 7️⃣ Criação do Usuário Administrador

Crie o superusuário para acesso ao Django Admin:

```bash
python manage.py createsuperuser
```

---

### 8️⃣ Executando o Servidor

Inicie o servidor de desenvolvimento:

```bash
python manage.py runserver
```

Acesse no navegador:

* Admin Django: `http://127.0.0.1:8000/admin/`
* API (futuro): `http://127.0.0.1:8000/api/`

---

### 9️⃣ Boas Práticas Adotadas

* Uso de ambiente virtual
* Separação por apps
* Dependências versionadas
* Estrutura preparada para API REST

---

## 📦 População Inicial do Banco de Dados

Este repositório documenta o **processo oficial de população inicial do banco de dados** do sistema **PATRI-TECH**, utilizando o **painel administrativo do Django** (`/admin`).

Este procedimento é essencial para garantir o correto funcionamento da **API REST**, a **padronização do inventário patrimonial** e a **consistência dos dados**.

---

## 📌 Objetivo

Ao seguir este guia, você será capaz de:

* Acessar o painel administrativo do Django
* Cadastrar os dados essenciais do sistema
* Aplicar regras de padronização patrimonial
* Validar os dados via API
* Conferir os endpoints no Swagger

---

## 🔐 Acesso ao Painel Administrativo

O Django Admin é utilizado para o gerenciamento direto das entidades do sistema.

```bash
http://127.0.0.1:8000/admin/
```

> 🔎 **Observação:**
> O usuário administrador deve ser criado previamente com:
>
> ```bash
> python manage.py createsuperuser
> ```
>
> (Comando apenas como referência.)

---

## 🔗 Ordem Correta de Cadastro

A ordem de cadastro deve ser seguida rigorosamente, pois existem **dependências entre as entidades**:

1. Categorias
2. Status
3. Unidades
4. Salas
5. Bens

➡️ Um **Bem** depende da existência de Categoria, Status, Unidade e Sala.

---

## 🗂️ Cadastro de Categorias

As categorias representam os **grupos patrimoniais**.

### Exemplos

* Informática
* Mobiliário
* Eletrodomésticos
* Veículos
* Ferramentas

### Regra de Padronização

* Nome no singular
* Representa um grupo, não um item
* Fácil entendimento

---

## 🔄 Cadastro de Status

O status indica a **situação atual do bem**.

### Exemplos

* Em uso
* Em manutenção
* Baixado
* Extraviado
* Novo

### Regra de Padronização

* Estado claro e objetivo
* Fácil interpretação em relatórios

---

## 🏢 Cadastro de Unidades

As unidades representam **locais físicos ou organizacionais**.

### Exemplos

* Sede — `SED-001`
* Anexo — `ANX-002`
* Polo Regional 1 — `PR1-003`
* Almoxarifado Central — `ALM-004`

### Regra de Padronização

* Nome curto
* Código único no formato `ABC-123`

---

## 🚪 Cadastro de Salas

As salas indicam a **localização específica do bem dentro da unidade**.

### Exemplos

* Sala 101 — Atendimento
* Sala 102 — Reuniões
* TI — Área de Tecnologia
* Almoxarifado — Estoque
* Administrativo

### Regra de Padronização

* Utilizar "Sala XXX" para ambientes numerados
* Nomes funcionais para setores

---

## 💻 Cadastro de Bens

Os bens são os **itens patrimoniais individualizados**.

### Exemplo — Notebook

* **Nome:** Notebook Dell Latitude 5400
* **Tombo:** `NB-SED-001`
* **Categoria:** Informática
* **Status:** Em uso
* **Unidade:** Sede
* **Sala:** Sala 101
* **Valor estimado:** 4800.00

### Exemplo — Mesa

* **Nome:** Mesa de Escritório
* **Tombo:** `MOB-ANX-014`
* **Categoria:** Mobiliário
* **Status:** Em uso
* **Unidade:** Anexo
* **Sala:** Almoxarifado

---

## 🏷️ Padrão de Tombo Patrimonial

Formato obrigatório:

```text
TIPO-UNIDADE-NÚMERO
```

### Exemplos

* `NB-SED-001`
* `MOB-ANX-014`
* `ELT-PR1-007`

Esse padrão garante rastreabilidade e organização do inventário.

---

## 🔌 Validação da API

Após o cadastro, valide os endpoints:

```text
/api/categorias/
/api/status/
/api/unidades/
/api/salas/
/api/bens/
```

Todos devem retornar dados em formato JSON.

---

## 📖 Documentação Swagger

A documentação interativa da API pode ser acessada em:

```bash
http://127.0.0.1:8000/docs/
```

No Swagger é possível:

* Visualizar os endpoints
* Testar requisições
* Validar relacionamentos

---

## ✅ Checklist Final

* [x] Categorias cadastradas
* [x] Status cadastrados
* [x] Unidades com código único
* [x] Salas associadas corretamente
* [x] Bens cadastrados
* [x] API retornando dados
* [x] Swagger funcionando

---

📌 **Conclusão**

Com este processo concluído, o **PATRI-TECH** estará com o banco de dados corretamente populado e pronto para uso em ambiente de desenvolvimento ou demonstração.

