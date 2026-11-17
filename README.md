# Minishell

A minimal Unix shell written in C, modeled on `bash`. Part of the 42 curriculum.

## Features

- Interactive prompt with history (GNU Readline)
- Lexer → parser pipeline: tokenizing, quote handling (`'` and `"`) and command reassembly
- Environment variable expansion, including `$?` (last exit status)
- Pipes: `cmd1 | cmd2 | cmd3`
- Redirections: `<`, `>`, `>>` and heredoc `<<`
- `PATH` lookup and execution with `fork` / `execve`
- Built-ins: `echo -n`, `cd`, `pwd`, `export`, `unset`, `env`, `exit`
- Signal handling like bash: `Ctrl-C` gives a new prompt, `Ctrl-\` is ignored, `Ctrl-D` exits

## Build & run

Needs `cc`, `make` and the readline development package (`libreadline-dev` on Debian/Ubuntu).

```bash
git clone --recurse-submodules https://github.com/Xr4t0s/Minishell.git
cd Minishell
make
./minishell
```

## Project layout

```
src/
├── main.c, input.c     # prompt loop, signals, input validation
├── parser/
│   ├── disassembler/   # tokenizer: words, operators, syntax checks
│   ├── expansions/     # $VAR and $? expansion
│   ├── reassembler/    # builds the command list from the tokens
│   └── dequote.c       # quote removal
├── io_config/          # redirections and heredoc
├── exec/               # PATH lookup, pipes, fork/execve
│   └── built_in/       # the seven built-ins
└── free/               # memory cleanup
libft/                  # my C library (git submodule)
```

## Stack

C · POSIX (`fork`, `execve`, `pipe`, `dup2`, `waitpid`, signals) · GNU Readline
