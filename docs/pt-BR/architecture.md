# Arquitetura do Noctty

[Português (Brasil)](architecture.md) · [English](../architecture.md)

## Camadas

```text
Interface do aplicativo
  janela · preferências · atalhos · abas/painéis · tema

Adaptador de terminal
  ciclo de vida · entrada · resize · clipboard · grade · dados de renderização

Núcleo de emulação de terminal
  parser VT · estado da tela · Unicode · tela alternativa · seleção · scrollback

Integração com o sistema operacional
  PTY · processo filho · sinais · ambiente · diretório de trabalho
```

A interface controla a apresentação e o comportamento visível para a pessoa usuária. O adaptador controla o limite que permite trocar o núcleo de emulação sem reescrever o aplicativo.

## Contrato do adaptador

O adaptador deve expor comportamento observável para:

- criar e fechar uma sessão baseada em PTY;
- ler a saída do terminal e enviar entrada codificada;
- redimensionar linhas e colunas;
- encaminhar sinais e informar a saída do processo;
- ler mudanças da tela/grade para renderização;
- copiar e colar texto selecionado;
- tratar tela alternativa sem perder o estado da tela principal.

O contrato não deve vazar tipos específicos de uma biblioteca para a camada do aplicativo.

## Avaliação do núcleo

Os candidatos são avaliados com:

- shells interativos e autocompletar;
- `vim`, `less`, `tmux` e SSH;
- largura Unicode, marcas combinantes e métodos de entrada;
- transições para a tela alternativa;
- seleção e scrollback extenso;
- redimensionamentos e encerramentos repetidos;
- uso de memória em sessões longas.

O núcleo escolhido é registrado com versão, licença, entradas de build e resultados de compatibilidade.

## Restrições do aplicativo

Noctty não deve exigir privilégios elevados. A configuração segue os caminhos XDG. A integração opcional com o Noctalia é carregada de forma defensiva e não pode impedir a inicialização do terminal.
