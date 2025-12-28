# Gerador de Escadas "Multidirecional" (Minecraft Bedrock e Java)

Este sistema avançado permite criar escadas em **8 direções diferentes** (4 Diagonais + 4 Retas), controlando a altura e o material.
---

## Instalação

### 1. Preparação
Execute estes dois comandos no chat para criar os objetivos:
```mcfunction
/scoreboard objectives add sc_gen_stairs dummy
/scoreboard objectives add sc_stairs_dir dummy
```

### 2. O Loop Principal 
Você precisará de uma fileira com **11 Command Blocks** (1 Repetição + 10 Cadeia).
*Todos devem ser "Always Active" (Sempre Ativo) e apontar uns para os outros.*

1.  **[Repetição]** `execute at @e[tag=stair_builder] run setblock ~ ~ ~ orange_concrete`
2.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=0}] at @s run tp @s ~1 ~1 ~1`
3.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=1}] at @s run tp @s ~1 ~1 ~-1`
4.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=2}] at @s run tp @s ~-1 ~1 ~-1`
5.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=3}] at @s run tp @s ~-1 ~1 ~1`
6.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=4}] at @s run tp @s ~1 ~1 ~`
7.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=5}] at @s run tp @s ~-1 ~1 ~`
8.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=6}] at @s run tp @s ~ ~1 ~1`
9.  **[Cadeia]** `execute as @e[tag=stair_builder,scores={sc_stairs_dir=7}] at @s run tp @s ~ ~1 ~-1`
10. **[Cadeia]** `scoreboard players remove @e[tag=stair_builder] sc_gen_stairs 1`
11. **[Cadeia]** `kill @e[tag=stair_builder,scores={sc_gen_stairs=..0}]`

---

## Como Usar e Escolher a Direção

Para gerar a escada, use a estrutura de gatilho (Impulso + 4 Cadeias) descrita abaixo. O segredo é mudar o número no **último comando**.

### O Gatilho
1.  `/summon armor_stand ~ ~ ~`
2.  `/tag @e[type=armor_stand,c=1,r=2] add stair_builder`
3.  `/effect @e[tag=stair_builder] invisibility 100 1 true`
4.  `/scoreboard players set @e[tag=stair_builder] sc_gen_stairs 20` (Define Altura)
5.  `/scoreboard players set @e[tag=stair_builder] sc_stairs_dir 0` (**Define Direção**)

### Tabela de Direções (IDs)
Mude o valor `0` no comando 5 para escolher a direção (baseado nas coordenadas padrão do Minecraft: Norte = -Z, Leste = +X).

| ID | Direção | Eixos |
| :--- | :--- | :--- |
| **0** | **Sudeste (Diagonal)** | +X +Z |
| **1** | **Nordeste (Diagonal)** | +X -Z |
| **2** | **Noroeste (Diagonal)** | -X -Z |
| **3** | **Sudoeste (Diagonal)** | -X +Z |
| **4** | Leste (Reta) | +X |
| **5** | Oeste (Reta) | -X |
| **6** | Sul (Reta) | +Z |
| **7** | Norte (Reta) | -Z |

---

## Dica: Como fazer escadas largas?
O sistema gera uma linha de blocos. Para fazer uma escada larga (ex: 3 blocos de largura), você precisa invocar 3 construtores lado a lado.

**Exemplo Manual:**
1.  Fique na posição 1, aperte o botão.
2.  Dê um passo para o lado.
3.  Aperte o botão de novo.
4.  Dê mais um passo.
5.  Aperte de novo.
*As três escadas crescerão juntas!*
