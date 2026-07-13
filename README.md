# Desafio DevSecOps — Gerenciador de Tarefas

## Sobre o Projeto
Este repositório faz parte do desafio prático do módulo de DevSecOps da ADA Tech.
Você receberá este projeto com vulnerabilidades propositais e uma pipeline incompleta.
Seu objetivo é **implementar a pipeline de segurança** e **corrigir as vulnerabilidades**.

## Estado atual
A pipeline está **incompleta**. Os steps de segurança precisam ser implementados por você.

## Sua missão
1. Implementar os steps de segurança no `pipeline.yml`
2. Fazer a pipeline **quebrar** ao detectar os problemas
3. Corrigir as vulnerabilidades encontradas
4. Fazer a pipeline **passar** com tudo verde ✅
5. Documentar o funcionamento da pipeline neste README

## O que implementar
- [ ] Secrets Scanning com **Gitleaks**
- [ ] SAST com **Semgrep**
- [ ] SCA com **Trivy**
- [ ] SCA com **Grype**
- [ ] Deploy com **GitHub Pages**

## Como a pipeline funciona
A pipeline executa uma sequência de verificações de segurança antes de publicar no GitHub Pages.

- **Checkout do Código**: baixa todo o histórico do repositório com `fetch-depth: 0`, garantindo que ferramentas como Gitleaks possam analisar commits antigos e rodar corretamente.
- **Build**: valida a existência dos arquivos em `src/` antes de avançar. Este passo confirma que a aplicação está pronta para as verificações de segurança.
- **Secrets Scanning com Gitleaks**: procura por segredos expostos em código e histórico de commits. Isso evita o vazamento de senhas, chaves e tokens sensíveis.
- **SAST com Semgrep**: aplica regras de análise estática para encontrar vulnerabilidades no código, como injeção de SQL, segredos e problemas do OWASP Top Ten.
- **SCA com Trivy**: escaneia o sistema de arquivos do repositório em busca de vulnerabilidades de alto e crítico em dependências e componentes, bloqueando o deploy se houver risco.
- **SCA com Grype**: escaneia dependências e artefatos para identificar vulnerabilidades conhecidas em bibliotecas utilizadas no projeto (supply chain).
- **Deploy com GitHub Pages**: somente após todas as verificações de segurança passarem, o site é publicado com segurança.

Cada step bloqueia o fluxo se detectar um problema (fail-fast), garantindo que a aplicação só seja disponibilizada em produção quando estiver segura.

## Vulnerabilidades encontradas e ações tomadas
- Removido 2 variáveis com secrets expostos
- Removido dependências com vulnerabilidades
- Removido input com possibilidade de injection

## URL de Produção
> https://viniciusevans.github.io/projeto-devsecop-desafio/