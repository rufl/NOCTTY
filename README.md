# Noctty

[Português (Brasil)](README.md) · [English](README.en.md)

Noctty é o terminal da família DINX: uma interface própria em Zig sobre um núcleo comprovado de emulação de terminal.

O repositório é privado e está em alpha. O foco inicial é correção de PTY e compatibilidade com shells, SSH, `vim`, `less`, `tmux` e outras TUIs antes de abas, transparência ou efeitos visuais.

## Objetivos

- iniciar shells e processos filhos com ciclo de vida correto;
- redimensionar PTYs, enviar sinais e limpar processos sem vazamentos;
- suportar sequências VT, Unicode, cursor, cores, tela alternativa e scrollback;
- copiar, colar e selecionar texto de forma previsível;
- permanecer compatível com aplicações interativas de terminal;
- integrar-se ao `$TERMINAL`, arquivos `.desktop`, caminhos XDG e Noctalia;
- funcionar também fora da distribuição DINX.

## Arquitetura

```text
Interface Noctty em Zig
  janela · preferências · atalhos · abas/painéis · tema

Adaptador de terminal
  entrada · resize · clipboard · grade · renderização · ciclo de vida

Núcleo de emulação comprovado
  VT · Unicode · tela alternativa · seleção · scrollback

Integração do sistema
  PTY · shell · processos · sinais · ambiente · diretório de trabalho
```

A implementação não deve reimplementar a semântica de terminal sem antes comparar um núcleo existente. Os candidatos iniciais são libvterm, libtsm e componentes incorporáveis do Ghostty, sujeitos a API pública, requisitos de build e licença.

## Integração com Noctalia

- descoberta e inicialização por `$TERMINAL`;
- argumentos de shell, diretório de trabalho e perfil;
- entrada `.desktop` válida;
- importação de tema por contrato documentado;
- IPC e plugins opcionais, sem tornar o Noctalia uma dependência de inicialização.

## Roadmap inicial

1. PTY, processo filho e janela mínima.
2. Renderização, entrada, resize, Unicode e scrollback.
3. Testes com shells, TUIs, SSH e `tmux`.
4. Integração `$TERMINAL`, `.desktop` e tema.
5. Preferências, abas e painéis.

## Documentação

- [Arquitetura](docs/pt-BR/architecture.md)
- [Compatibilidade](docs/pt-BR/compatibility.md)

Versões em inglês:

- [Architecture](docs/architecture.md)
- [Compatibility](docs/compatibility.md)

DINX: [rufl/dinx-alpha](https://github.com/rufl/dinx-alpha)
