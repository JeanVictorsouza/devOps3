# Olá Mundo DevOps — Exemplo de Pipeline de CI

Aplicação Node.js (Express) simples, usada como exemplo prático de
Integração Contínua (CI) com GitHub Actions e Docker, conforme a aula
"Integração Contínua (CI)".

## Estrutura do projeto

```
ola-devops/
├── app.js                     # Lógica da aplicação (rota /)
├── server.js                  # Inicialização do servidor
├── app.test.js                # Teste automatizado (jest + supertest)
├── package.json
├── Dockerfile                 # Build multi-stage da imagem
├── .dockerignore
├── .gitignore
└── .github/
    └── workflows/
        └── ci.yml             # Pipeline de CI (GitHub Actions)
```

## Como rodar localmente

```bash
npm install
npm start
```

Acesse http://localhost:3000 — deve aparecer "Olá Mundo DevOps!".

## Como rodar os testes

```bash
npm test
```

## Como rodar com Docker

```bash
docker build -t ola-devops .
docker run -p 3000:3000 -d ola-devops
```

## Como subir para o GitHub e acionar o pipeline de CI

```bash
git init
git add .
git commit -m "Commit inicial do projeto Olá Mundo DevOps"
git remote add origin <URL_DO_SEU_REPOSITORIO.git>
git branch -M main
git push -u origin main
```

Assim que o push for feito, o workflow `.github/workflows/ci.yml` roda
automaticamente na aba **Actions** do repositório, executando: checkout
do código, instalação de dependências, testes (jest) e build da imagem
Docker.

## Em quais situações essa abordagem com CI pode ser útil dentro de uma empresa

A Integração Contínua é útil em praticamente qualquer empresa que
mantenha software em produção com mais de um desenvolvedor envolvido.
Em times pequenos, evita que mudanças de diferentes pessoas quebrem o
código sem que ninguém perceba, já que cada push é testado
automaticamente antes de ser aceito na branch principal. Em times
maiores, é ainda mais crítica: como muitas alterações chegam por dia,
seria inviável testar tudo manualmente, e o CI garante feedback rápido
para quem introduziu um erro, permitindo corrigi-lo enquanto o contexto
da mudança ainda está fresco. Também é essencial antes de lançamentos
(releases), pois assegura que a branch principal esteja sempre estável
e pronta para ser implantada, e serve de base para pipelines de Entrega
Contínua (CD), que automatizam o deploy em produção. Por fim, reduz o
retrabalho e o risco de erro humano em tarefas repetitivas como rodar
testes e gerar builds, liberando a equipe para focar no desenvolvimento
de funcionalidades.
