# RPG Interativo em TypeScript

## 📖 Sobre o Jogo
Este é um RPG interativo baseado em TypeScript, jogado via terminal. O jogo se passa em uma dungeon misteriosa, onde o jogador deve explorar corredores, enfrentar monstros e coletar itens até alcançar o desafio final. As escolhas feitas ao longo do caminho influenciam a jornada e o desfecho da aventura.

## 🎮 Como Jogar
1. **Execute o jogo no terminal** com `node dist/jogo.js` após compilar o TypeScript (`tsc`).
2. Escolha seu **personagem**: Guerreiro ou Mago.
3. Enfrente inimigos e tome decisões estratégicas:
   - **Atacar**: Causa dano ao inimigo.
   - **Defender**: Reduz ou anula o dano recebido.
   - **Usar item**: Restaura vida com poções coletadas.
   - **Fugir**: Sai da batalha (mas pode ter consequências).
4. **Colete itens** deixados por inimigos derrotados.
5. **Explore** diferentes caminhos e descubra segredos da dungeon.
6. **Sobreviva** até o final e descubra qual destino aguarda seu personagem!

## 🛠 Estrutura do Código

O jogo segue um design baseado em **Programação Orientada a Objetos (POO)** e **Interfaces**. Aqui está a estrutura principal:

```
📂 src/
 ├── 📂 Personagem/       # Classes dos personagens
 │   ├── personagem.ts    # Classe base dos personagens
 │   ├── guerreiro.ts     # Classe específica do Guerreiro
 │   ├── mago.ts          # Classe específica do Mago
 │
 ├── 📂 Monstros/         # Informações e interfaces dos inimigos
 │   ├── monstroInfo.ts   # Interface base dos inimigos
 │   ├── slime.ts         # Classe do Slime
 │   ├── esqueleto.ts     # Classe do Esqueleto
 │   ├── mimic.ts         # Classe do Mimic
 │
 ├── 📂 Itens/            # Sistema de itens e inventário
 │   ├── item.ts         # Classe base dos itens
 │
 ├── luta.ts              # Sistema de combate
 ├── jogo.ts              # Arquivo principal do jogo
```

### **📌 Personagem (Classe Base)**
Cada personagem possui:
- `nome`: Nome do personagem
- `vida`: Vida atual
- `forca`: Ataque do personagem
- `defesa`: Redução de dano
- `inventario`: Lista de itens coletados
- Métodos:
  - `atacar(alvo: Inimigo)`: Ataca um inimigo
  - `defender(ataqueInimigo: number)`: Bloqueia ou reduz dano

### **💀 Inimigos (Interface e Implementações)**
Cada inimigo implementa a interface `Inimigo`:
- `nome`: Nome do monstro
- `vida`: Vida total
- `forca`: Dano causado ao atacar
- `defesa`: Redução de dano ao receber ataque
- `atacar(alvo: Personagem)`: Método para atacar o jogador

### **🛡️ Defesa**
A defesa funciona assim:
- Se a defesa do jogador for maior ou igual ao ataque do inimigo, ele **não toma dano**.
- Se a defesa for menor, ele toma **a diferença entre o ataque do inimigo e sua defesa**.

### **🎁 Itens**
Os inimigos derrotados podem dropar itens, como:
- `Poção de Cura`: Recupera **20 de vida**.

### **⚔️ Sistema de Luta**
A luta segue um sistema de turnos:
1. O jogador escolhe uma ação.
2. O inimigo responde com um ataque (se ainda estiver vivo).
3. O combate continua até um dos dois ser derrotado.
4. O jogador pode coletar itens dos inimigos derrotados.

## 📜 História do Jogo
Você é um aventureiro corajoso que entra em uma **dungeon amaldiçoada** em busca de tesouros e glória. No entanto, criaturas sombrias espreitam os corredores e cada decisão pode ser a diferença entre a vida e a morte.

Ao longo da exploração, você encontrará **monstros misteriosos, baús traiçoeiros e desafios inesperados**. Seu destino dependerá de sua estratégia e coragem!

### Possíveis finais:
- **Final Heroico:** Você derrota todos os monstros e escapa com um grande tesouro.
- **Final Sombrio:** Você é derrotado e se torna mais uma alma presa na dungeon.
- **Final Misterioso:** Você descobre um segredo oculto e toma uma decisão inesperada...

## 🚀 Como Adicionar Novos Personagens ou Itens
### Adicionando um novo personagem
1. Crie um novo arquivo **`novoPersonagem.ts`** na pasta `Personagem/`.
2. Estenda a classe `Personagem` e personalize os atributos:
   ```typescript
   import { Personagem } from "./personagem";
   export class Arqueiro extends Personagem {
       constructor() {
           super("Arqueiro", 80, 15, 7);
       }
   }
   ```
3. No `jogo.ts`, adicione uma opção para escolher esse personagem.

### Adicionando um novo inimigo
1. Crie um novo arquivo **`novoInimigo.ts`** na pasta `Monstros/`.
2. Implemente a interface `Inimigo` e defina atributos personalizados:
   ```typescript
   import { Inimigo } from "./monstroInfo";
   export class Dragao implements Inimigo {
       nome = "Dragão";
       vida = 300;
       forca = 50;
       defesa = 30;
       atacar(alvo: Personagem): void {
           alvo.vida -= Math.max(this.forca - alvo.defesa, 0);
           console.log(`${this.nome} cuspiu fogo em ${alvo.nome}, causando ${this.forca} de dano!`);
       }
   }
   ```
3. Adicione o inimigo ao fluxo do jogo dentro do `jogo.ts`.

### Adicionando um novo item
1. Crie um novo arquivo **`novoItem.ts`** na pasta `Itens/`.
2. Crie um novo item estendendo a classe `Item`:
   ```typescript
   import { Item } from "./item";
   export class EspadaMagica extends Item {
       constructor() {
           super("Espada Mágica", (p) => p.forca += 10);
       }
   }
   ```
3. No `jogo.ts`, adicione esse item como loot de um inimigo.

---

## 🏆 Conclusão
Este projeto é um **RPG minimalista**, mas expansível! Ele foi construído para ser fácil de modificar, permitindo a adição de **novos personagens, inimigos, itens e eventos** sem quebrar o código existente.

Caso tenha sugestões ou queira expandir o jogo, sinta-se livre para contribuir!

**Divirta-se explorando a dungeon! 🏹⚔️🔥**

