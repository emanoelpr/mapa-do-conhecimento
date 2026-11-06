# Mapa do Conhecimento

Projeto em desenvolvimento para organizar conhecimentos escolares por disciplina, etapa e ano escolar, permitindo relacioná-los à estrutura curricular da Base Nacional Comum Curricular (BNCC).

O banco de dados diferencia os conteúdos organizados pelo projeto dos registros curriculares oficiais. Essa separação permite estruturar os conhecimentos do projeto sem alterar os títulos e identificadores das referências da BNCC.

## Objetivos

- Organizar conhecimentos por área, disciplina, etapa e ano escolar.
- Registrar descrições, objetos de estudo, tags e pré-requisitos dos conhecimentos do projeto.
- Armazenar habilidades, competências, unidades temáticas e objetos de conhecimento da BNCC.
- Relacionar os conhecimentos do projeto às referências curriculares oficiais.
- Apoiar a organização e a consulta de conteúdos escolares.
- Preparar a estrutura de dados para futuras funcionalidades da aplicação.

## Organização do banco de dados

O banco possui tabelas organizadas em diferentes grupos:

| Grupo | Tabelas principais | Finalidade |
|---|---|---|
| Estrutura escolar | `areas_conhecimento`, `disciplinas`, `etapas`, `anos_escolares` | Organizar áreas, componentes curriculares, etapas e anos/séries. |
| Conhecimentos do projeto | `conhecimentos`, `objetos_conhecimento`, `unidades_tematicas`, `conhecimento_anos_escolares` | Armazenar os conteúdos próprios do projeto e sua organização. |
| Dados da BNCC | `habilidades_bncc`, `bncc_objetos_conhecimento`, `bncc_unidades_tematicas`, `competencias` | Manter os registros curriculares oficiais utilizados pelo projeto. |
| Relacionamentos curriculares | `conhecimento_habilidades`, `bncc_habilidade_objetos`, `bncc_habilidade_anos`, `competencia_habilidades` | Representar relações entre conhecimentos, habilidades, objetos e competências. |
| Sugestões de associação | `conhecimento_habilidade_sugestoes`, `conhecimento_ano_sugestoes`, `conhecimento_bncc_objeto_sugestoes` | Armazenar sugestões de possíveis relações para análise. |
| Organização complementar | `tags`, `conhecimento_tags`, `conhecimento_prerequisitos`, `referencias_escolares` | Classificar conteúdos, indicar pré-requisitos e registrar referências. |
| Usuários | `usuarios`, `usuario_conhecimentos` | Estruturas para contas e acompanhamento individual de aprendizagem. |
| Importação de dados | `stg_bncc_ef`, `stg_bncc_em` | Apoiar a preparação e importação dos dados de origem da BNCC. |

O esquema também contém tabelas auxiliares de relacionamento e visualizações (`VIEW`) para consultas.

## Tecnologias

- MySQL 8.0 ou versão compatível com os recursos utilizados no dump.
- InnoDB para armazenamento e integridade referencial.
- `utf8mb4` para suporte a caracteres e acentuação.
- MySQL Workbench ou outro cliente compatível para administração do banco.

## Estrutura do repositório

```text
mapa-do-conhecimento/
├── README.md
├── .gitignore
└── database/
    └── mapa_do_conhecimento.sql
```

- `database/mapa_do_conhecimento.sql`: estrutura e dados-base do banco de dados.

## Como importar o banco de dados

> **Atenção:** o dump contém comandos `DROP TABLE` e `DROP VIEW`. Faça a importação somente em um ambiente local de desenvolvimento ou em uma base de testes. Não importe sobre um banco que contenha dados que você deseja preservar.

### Pelo terminal

Na pasta do repositório, execute:

```bash
mysql -u SEU_USUARIO -p < database/mapa_do_conhecimento.sql
```

O próprio arquivo SQL cria o banco `mapa_do_conhecimento` e seleciona essa base antes de criar as tabelas.

### Pelo MySQL Workbench

1. Abra o MySQL Workbench e conecte-se ao servidor local.
2. Acesse **Server → Data Import** ou abra o arquivo `.sql` no editor.
3. Se utilizar o editor, carregue `database/mapa_do_conhecimento.sql`.
4. Execute o script e confira se as tabelas foram criadas.

## Privacidade e segurança

O dump incluído neste repositório foi preparado para compartilhamento público. Ele preserva as estruturas das tabelas `usuarios` e `usuario_conhecimentos`, mas não inclui os registros dessas tabelas.

Antes de publicar novas versões ou exportações do banco, verifique se não há:

- nomes, e-mails, telefones ou outros dados pessoais;
- hashes de senha ou credenciais;
- dados individuais de aprendizagem;
- arquivos `.env`, chaves de API ou senhas de conexão.

Não publique dumps de ambientes reais sem revisão e anonimização. Utilize dados fictícios para exemplos e testes públicos.

## Fonte dos dados curriculares

Os registros curriculares do banco identificam a BNCC como fonte documental. A presença de um registro no banco não substitui a consulta aos documentos oficiais, especialmente quando a informação for utilizada para decisões pedagógicas ou curriculares.

## Situação do projeto

O Mapa do Conhecimento está em desenvolvimento. Este repositório reúne, nesta etapa, a documentação inicial e a estrutura do banco de dados. Novas partes da aplicação e documentação poderão ser adicionadas conforme o desenvolvimento avançar.

---

Autor do **Mapa do Conhecimento**: Emanoel do Prado.