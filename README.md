<p align="center">
  <img src="../assets/araru-banner.png" width="100%" alt="Araru — seu acervo digital sob seu controle">
</p>

<p align="center">
  <strong>Seu acervo digital, sob seu controle.</strong>
</p>

<p align="center">
  Open source · Self-hosted · Privacidade por design · Feito no Brasil 🇧🇷
</p>

<p align="center">
  <a href="https://github.com/Araru-OSS/araru">Conheça o projeto</a>
  ·
  <a href="https://github.com/Araru-OSS/araru/tree/main/docs">Documentação</a>
  ·
  <a href="https://github.com/Araru-OSS/araru/blob/main/CONTRIBUTING.md">Contribua</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-em%20desenvolvimento-2d8a4e?style=flat-square" alt="Status: em desenvolvimento">
  <img src="https://img.shields.io/badge/Node.js-%3E%3D22.5-339933?style=flat-square&logo=node.js&logoColor=white" alt="Node.js 22.5 ou superior">
  <img src="https://img.shields.io/badge/React-Vite-61DAFB?style=flat-square&logo=react&logoColor=20232a" alt="React e Vite">
  <img src="https://img.shields.io/badge/Docker-ready-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker ready">
</p>

---

## 📚 O que é o Araru?

O **Araru** é um servidor de biblioteca digital open source e self-hosted para organizar, pesquisar, preservar e ler o seu próprio acervo.

Você mantém o controle dos seus arquivos, metadados, histórico de leitura e infraestrutura — com uma experiência web responsiva para desktop, tablet e celular.

> **Sua biblioteca. Seu servidor. Seus dados.**

### Feito para acervos de verdade

- 📖 Livros e ebooks
- 💬 HQs e mangás
- 📰 Revistas
- 📄 Documentos

## ✨ Recursos atuais

- Catálogo local com integração opcional ao Google Drive
- Categorias hierárquicas baseadas em pastas
- Pesquisa full-text, filtros, favoritos e séries
- Metadados, capas, revisão e identificação de duplicidades
- Progresso de leitura, continuar de onde parou e estatísticas
- Leitores internos para **PDF, EPUB, MOBI, CBZ e CBR**
- PWA e download offline explícito
- Backup, verificação de integridade e jobs operacionais
- Arquitetura preparada para múltiplos clientes

## 🧩 Como funciona

O Araru separa o servidor — responsável pela biblioteca e pelos dados — dos clientes que oferecem a experiência de uso:

```text
                         ┌────────────────────┐
                         │    Araru Server    │
                         │ API · Auth · Dados │
                         │ Storage · Metadata │
                         └──────────┬─────────┘
                                    │ HTTP
                         ┌──────────▼─────────┐
                         │      Araru Web     │
                         │    React · Vite    │
                         │        PWA         │
                         └────────────────────┘
```

O servidor conversa com PostgreSQL, Redis, filesystem/cache e provedores opcionais de armazenamento. Clientes não acessam diretamente o banco ou o storage.

## 🛠️ Stack

`Node.js` · `Express` · `React` · `Vite` · `PWA` · `PostgreSQL` · `Redis` · `Docker`

## 🚧 Status do projeto

O Araru está em **desenvolvimento ativo**. A base atual já contempla o servidor e o cliente web; APIs, funcionalidades e arquitetura ainda podem evoluir antes de uma primeira versão estável.

Entre as próximas direções estão clientes mobile e desktop, audiobooks, API versionada, expansão de multiusuário e evolução da camada de storage. Consulte o [roadmap](https://github.com/Araru-OSS/araru/tree/main/docs/roadmap) para acompanhar o que está sendo considerado.

## 🤝 Construído em público

Contribuições são bem-vindas — código, testes, documentação, acessibilidade, UX, traduções e boas ideias. Antes de abrir uma issue ou pull request, leia as [orientações para contribuição](https://github.com/Araru-OSS/araru/blob/main/CONTRIBUTING.md).

Se você encontrar uma vulnerabilidade de segurança, siga as instruções privadas do projeto em vez de abrir uma issue pública.

## 🔗 Links

- [Repositório do Araru](https://github.com/Araru-OSS/araru)
- [Documentação técnica](https://github.com/Araru-OSS/araru/tree/main/docs)
- [Arquitetura](https://github.com/Araru-OSS/araru/blob/main/docs/architecture/overview.md)
- [Guia de início](https://github.com/Araru-OSS/araru/tree/main/docs/getting-started)
- [Roadmap](https://github.com/Araru-OSS/araru/tree/main/docs/roadmap)
- [Organização Araru OSS](https://github.com/Araru-OSS)

<p align="center">
  <br>
  <img src="../assets/araru-logo.png" width="260" alt="Araru OSS">
  <br><br>
  <em>Leia. Organize. Preserve.</em>
</p>
