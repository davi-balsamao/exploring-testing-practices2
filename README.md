# Explorando Práticas de Teste

Neste exercício, vamos explorar práticas de teste em sistemas reais utilizando a ferramenta [TestMiner](https://andrehora.github.io/testminer).

O TestMiner permite visualizar e analisar testes de software em repositórios do GitHub, fornecendo dados sobre como os projetos organizam seus testes, como eles evoluem entre versões e quais bibliotecas de teste são utilizadas.
Explore a ferramenta antes de começar para se familiarizar com seu funcionamento.

Mais detalhes no GitHub da ferramenta: <https://github.com/andrehora/testminer>.

---

## Passo 1: Selecionar DOIS repositórios

Escolha dois repositórios reais que possuam testes de software.

## Passo 2: Explorar os repositórios selecionados

Busque os repositórios escolhidos no [TestMiner](https://andrehora.github.io/testminer) e analise os dados de teste gerados pela ferramenta.

## Passo 3: Explicar as prática de teste

Para cada repositório, escolha uma prática ou dado de teste relevante e explique com suas próprias palavras.

---

## Instruções de entrega

1. Faça um `fork` deste repositório.
2. Responda às questões abaixo diretamente neste arquivo `README.md` do seu fork. Pode adicionar imagens para enriquecer sua explicação.
3. No Moodle, submeta apenas a URL do seu fork.

---

## Respostas

### Repositório 1

Repositório: `https://github.com/fastapi/fastapi`

URL TestMiner: `https://andrehora.github.io/testminer/#fastapi/fastapi`

Explicação: O dado mais revelador do FastAPI no TestMiner é a estrutura dos nomes dos
arquivos de teste: a ferramenta mostra os testes agrupados em `tutorial001` (54),
`tutorial002` (24), `tutorial003` (27), etc. Isso expõe uma prática deliberada do
projeto — os exemplos de código da própria documentação são testados automaticamente.
Cada trecho do tutorial oficial tem um arquivo de teste correspondente que executa
aquele exemplo e verifica a resposta esperada. Isso se confirma na seção *Test Location*:
além da pasta `tests` (383 arquivos), o TestMiner encontra testes em `docs_src` (32) e
`docs` (58). Ou seja, o código que aparece na documentação mora no repositório como
fonte executável e é coberto por testes. A consequência prática é que a documentação
nunca fica desatualizada em silêncio: se um exemplo do tutorial quebrar numa nova
versão, a suíte de testes falha. É uma forma de *documentation-as-tests*. Vale notar
a proporção: 1805 arquivos-fonte para 370 testes e 95 *test helpers* — um volume alto
de testes, coerente com um framework que precisa garantir estabilidade para milhares
de aplicações em produção.

### Repositório 2

Repositório: `https://github.com/expressjs/express`

URL TestMiner: `https://andrehora.github.io/testminer/#expressjs/express`

Explicação: O dado que escolhi é a seção *Test Dependencies*, que lista três
bibliotecas npm: `mocha`, `nyc` e `supertest`. Esse trio descreve com precisão a
estratégia de teste do Express: o `mocha` é o *test runner* (executa e organiza os
testes); o `nyc` (Istanbul) mede a cobertura de código; e o `supertest` — a peça mais
característica — permite subir uma instância real do app Express e disparar requisições
HTTP de verdade contra ela, verificando status, headers e corpo da resposta. Isso mostra
que o Express não testa suas funções de forma isolada (unitária pura), e sim via testes
de integração de ponta a ponta no nível HTTP — exatamente o comportamento que importa
para um framework web: dado um request, a rota/middleware certo responde corretamente.
Esse foco também aparece na classificação do TestMiner: dos arquivos de teste, a
ferramenta identifica 91 *test helpers* e 18 *fixtures*, contra 106 arquivos-fonte. A
quantidade alta de helpers e fixtures indica forte reaproveitamento de setup — apps e
requisições de exemplo montados uma vez e reutilizados em muitos testes, padrão típico
de quem testa cenários HTTP repetidamente.
