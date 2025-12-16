# Hands-On — Populando o Banco de Dados do PATRI-TECH via `/admin`

## Visão Geral

Este hands-on demonstra **como funciona o processo de cadastro inicial de dados** no sistema **PATRI-TECH**, utilizando o **painel administrativo do Django**. Esses cadastros são fundamentais para que a API funcione corretamente e para que o inventário patrimonial mantenha **padronização, rastreabilidade e consistência**.

O fluxo apresentado segue uma **ordem lógica de dependência entre entidades**, evitando erros de relacionamento e garantindo que os bens possam ser corretamente associados.

---

## Objetivo do Hands-On

Ao final deste procedimento, você será capaz de:

* Acessar o painel administrativo do Django
* Criar os registros básicos do sistema
* Aplicar regras de padronização patrimonial
* Validar os dados via API REST
* Conferir a documentação interativa no Swagger

---

## 1. Acesso ao Painel Administrativo

O painel administrativo é a interface padrão do Django para **gerenciamento direto do banco de dados**.

**Endereço:**

```
http://127.0.0.1:8000/admin/
```

**Acesso:**

* Utilize o usuário administrador criado previamente com:

  ```bash
  python manage.py createsuperuser
  ```
* Este comando é apenas uma referência; o login deve ser feito pela interface web.

---

## 2. Ordem Correta de Cadastro (Regra de Dependência)

A ordem de cadastro é essencial porque algumas entidades **dependem de outras**:

1. Categorias
2. Status
3. Unidades
4. Salas
5. Bens

➡️ Exemplo: um **Bem** depende de Categoria, Status, Unidade e Sala já existentes.

---

## 3. Cadastro de Categorias

### O que é uma Categoria?

Define o **grupo patrimonial** ao qual um bem pertence.

### Exemplos

* Informática – Equipamentos de TI
* Mobiliário – Mesas, cadeiras, armários
* Eletrodomésticos – Geladeiras, micro-ondas
* Veículos – Carros, motos
* Ferramentas – Equipamentos de manutenção

### Lei de Formação

* Nome no **singular**
* Representa um **grupo**, não um item específico
* Fácil entendimento para usuários e relatórios

➡️ A categoria será reutilizada em diversos bens.

---

## 4. Cadastro de Status

### O que é Status?

Indica a **situação atual do bem** no inventário.

### Exemplos

* Em uso – Bem ativo
* Em manutenção – Aguardando reparo
* Baixado – Retirado do patrimônio
* Extraviado – Não localizado
* Novo – Recém adquirido

### Lei de Formação

* Estado claro e objetivo
* Preferencialmente iniciado por ação ou condição

➡️ O status permite controle operacional e relatórios gerenciais.

---

## 5. Cadastro de Unidades

### O que é uma Unidade?

Representa uma **localização organizacional ou física** da instituição.

### Exemplos

* Sede – SED-001 – Rua Central, 100
* Anexo – ANX-002 – Rua B, 222
* Polo Regional 1 – PR1-003 – Bairro Norte
* Almoxarifado Central – ALM-004 – Avenida Sul

### Lei de Formação

* Nome curto e identificável
* Código no formato `ABC-123`
* Código **único** por unidade

➡️ O código da unidade será usado na formação do **tombo patrimonial**.

---

## 6. Cadastro de Salas

### O que é uma Sala?

Indica o **local específico dentro de uma unidade** onde o bem está alocado.

### Exemplos

* Sala 101 – Sede – Atendimento
* Sala 102 – Sede – Reuniões
* TI – Suporte – Sede – Área de TI
* Almoxarifado – Anexo – Estoque
* Administrativo – Polo Regional 1

### Lei de Formação

* Usar "Sala XXX" para ambientes numerados
* Nome funcional para setores específicos

➡️ As salas facilitam o controle físico e auditorias patrimoniais.

---

## 7. Cadastro de Bens

### O que é um Bem?

É o **item patrimonial individual**, controlado e rastreado pelo sistema.

### Exemplo 1 — Notebook

* Nome: Notebook Dell Latitude 5400
* Tombo: NB-SED-001
* Categoria: Informática
* Status: Em uso
* Unidade: Sede
* Sala: Sala 101
* Valor estimado: 4800.00

### Exemplo 2 — Mesa

* Nome: Mesa de Escritório
* Tombo: MOB-ANX-014
* Categoria: Mobiliário
* Status: Em uso
* Unidade: Anexo
* Sala: Almoxarifado

### Exemplo 3 — Geladeira

* Nome: Geladeira Consul FrostFree
* Tombo: ELT-PR1-007
* Categoria: Eletrodomésticos
* Status: Em manutenção
* Unidade: Polo Regional 1
* Sala: Administrativo

---

## 8. Lei de Formação do Tombo Patrimonial

### Formato Padrão

```
TIPO-UNIDADE-NÚMERO
```

### Exemplos

* NB-SED-001
* MOB-ANX-014
* ELT-PR1-007

➡️ Esse padrão garante:

* Identificação rápida do tipo de bem
* Associação direta à unidade
* Numeração sequencial controlada

---

## 9. Validação dos Dados na API

Após os cadastros, valide se a API está retornando corretamente:

```
/api/categorias/
/api/status/
/api/unidades/
/api/salas/
/api/bens/
```

➡️ Todas as rotas devem retornar listas JSON com os dados cadastrados.

---

## 10. Validação no Swagger

Acesse a documentação interativa:

```
http://127.0.0.1:8000/docs/
```

No Swagger é possível:

* Visualizar todos os endpoints
* Testar requisições GET, POST, PUT e DELETE
* Confirmar relacionamentos entre entidades

---

## Checklist Final

* Categorias criadas
* Status cadastrados
* Unidades com código único
* Salas associadas corretamente
* Bens registrados com tombo válido
* API retornando dados
* Swagger funcionando corretamente

✅ Com isso, o banco de dados do PATRI-TECH estará corretamente populado e pronto para uso.
