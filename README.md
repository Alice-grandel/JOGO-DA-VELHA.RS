# 🕹️ Jogo da Velha em Rust

Este é um jogo da velha (tic-tac-toe) feito em **Rust**, rodando inteiramente no terminal. Dois jogadores se revezam jogando, inserindo as coordenadas da linha e coluna para marcar `X` ou `O` em um tabuleiro 3x3.

## 💡 Funcionalidades

- ✅ Interface de texto simples no terminal
- ✅ Validação de jogadas (evita sobrescrever posições)
- ✅ Verificação automática de vitória e empate
- ✅ Alternância automática entre os jogadores `X` e `O`

## 📷 Exemplo de uso

```bash
  0 1 2
0 _ _ _
1 _ _ _
2 _ _ _

Vez do jogador 'X'
Digite a linha e coluna (ex: 0 1): 1 1
```
# CODIGO 🦀:
```
use std::io;

fn main() {
    let mut board = [[' '; 3]; 3];
    let mut current_player = 'X';

    loop {
        print_board(&board);
        println!("Vez do jogador '{}'", current_player);
        
        let (row, col) = get_move();
        
        if board[row][col] != ' ' {
            println!("Posição já ocupada! Tente novamente.");
            continue;
        }

        board[row][col] = current_player;

        if check_winner(&board, current_player) {
            print_board(&board);
            println!("Jogador '{}' venceu!", current_player);
            break;
        }

        if board_full(&board) {
            print_board(&board);
            println!("Empate!");
            break;
        }

        // Alterna o jogador
        current_player = if current_player == 'X' { 'O' } else { 'X' };
    }
}

fn print_board(board: &[[char; 3]; 3]) {
    println!("\n 0 1 2");
     for (i, row) in board.iter().enumerate() {
        print!("{}", i);
     for &cell in row.iter() {
        print!("{}", cell);
     }
    println!();
     }
    println!();
}

fn get_move() -> (usize, usize) {
    loop {
        println!("Digite uma linha e coluna (Ex: 0 1): ");
         let mut input = String::new();
          io::stdin().read_line(&mut input).expect("Erro");

        let parts: Vec<&str> = input.trim().split_whitespace().collect();
         if parts.len() != 2 {
            println!("Entrada invalida!");
             continue;
        }

        let row: usize = match parts[0].parse() {
            Ok(num) if num < 3 => num,
             _ => {
            println!("Linha invalida!");
             continue;
             }
        }; 
        
        let col: usize = match parts[1].parse() {
            Ok(num) if num < 3 => num,
             _ => {
            println!("Valor invalido!");
             continue;
             }
        };

             return(row, col);
    }
}

fn check_winner(board: &[[char; 3]; 3], player: char) -> bool {
 for i in 0..3 {
      if (board[i][0] == player && board[i][1] == player && board[i][2] == player) || 
         (board[0][i] == player && board[1][i] == player && board[2][i] == player) {
            return true;
         }   
   }  

      if (board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
         (board[0][2] == player && board[1][1] == player && board[2][0] == player) {
            return true;
         }
}

fn board_full(board: &[[char; 3]; 3]) -> bool {
    for row in board {
       for cell in row {
         if *cell == ' ' {
            return false;
         }
       }
    }
     true
}
```
