# Compatibilidade do Noctty

[Português (Brasil)](compatibility.md) · [English](../compatibility.md)

## Contrato do desktop

- fornecer uma entrada `.desktop` válida;
- ser descoberto como terminal por meio de `$TERMINAL`;
- aceitar um argumento de diretório de trabalho quando suportado;
- preservar abertura normal pelo desktop e navegação por teclado;
- usar locais XDG para configuração e cache.

## Contrato com o Noctalia

A integração com o Noctalia é aditiva:

1. **Descoberta:** o Noctalia consegue localizar e iniciar o Noctty.
2. **Invocação:** argumentos de shell, diretório e perfil têm comportamento determinístico.
3. **Tema:** um adaptador documentado do Dinx Theme mapeia cores semânticas e cores ANSI do terminal.
4. **IPC opcional:** IPC indisponível ou malformado nunca bloqueia a inicialização.

O Noctty deve continuar funcional quando o Noctalia não estiver instalado.

## Matriz de compatibilidade do terminal

| Área | Critério de aceitação |
| --- | --- |
| Shell | shell interativo inicia e termina corretamente |
| PTY | resize e entrega de sinais atualizam o processo filho |
| TUI | `vim`, `less` e `tmux` renderizam e aceitam entrada |
| SSH | shell remoto e resize funcionam por SSH |
| Unicode | largura, marcas combinantes e texto do clipboard permanecem corretos |
| Scrollback | seleção e navegação preservam o texto esperado |
| Tela alternativa | aplicativos retornam à tela principal sem corrupção |
| Falha | falha do processo filho é visível e não deixa sessão obsoleta |
