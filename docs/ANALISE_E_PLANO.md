# Análise e plano de compatibilidade

Data da análise: 2026-08-01. Minecraft Forge 1.20.1.

## Limites e integridade

Os JARs foram lidos como ZIP, sem extração ou alteração. Não há datapack existente
no repositório e nenhum arquivo de mod foi sobrescrito. A compatibilidade de
hidratação entre `legendarysurvivaloverhaul` e `chovys_apocalypse_mod` fica fora do
escopo e não será alterada.

### Mod IDs confirmados

| Mod | JAR | mod ID |
| --- | --- | --- |
| Chovy's Apocalypse | `chovys_apocalypse_mod-1.9.jar` | `chovys_apocalypse_mod` |
| Zombie Survival Kit | `Zombie Survival Kit-1.20.1-forge-2.1.8.jar` | `zombiekit` |
| Legendary Survival Overhaul | `legendarysurvivaloverhaul-1.20.1-2.4.6.jar` | `legendarysurvivaloverhaul` |
| Fallout Gunpack | `tacz_fallout-0.1.0.jar` | `tacz_fallout` |

O gunpack Fallout declara `tacz` como dependência obrigatória (`[1.1.4,)`), mas
**nenhum JAR com `modId = "tacz"` está presente neste projeto**. Portanto, não há
como confirmar no material fornecido o item-base e o formato NBT/componentes que o
TACZ usa para materializar armas e munições. Não é seguro inventá-los.

## Loot tables encontradas

### Chovy's Apocalypse

- `chovys_apocalypse_mod:blocks/cargobox`
- `chovys_apocalypse_mod:blocks/foodcrate`
- `chovys_apocalypse_mod:blocks/weaponcrate`
- `minecraft:chests/village/village_butcher` (override fornecido pelo mod)
- `minecraft:chests/village/village_fisher` (override fornecido pelo mod)
- `minecraft:chests/village/village_toolsmith` (override fornecido pelo mod)
- `minecraft:chests/village/village_weaponsmith` (override fornecido pelo mod)
- `minecraft:entities/zombie` (override fornecido pelo mod)

### Zombie Survival Kit

- `zombiekit:chests/agriculture`
- `zombiekit:chests/blueprint`
- `zombiekit:chests/building`
- `zombiekit:chests/food`
- `zombiekit:chests/gear`
- `zombiekit:chests/lighting`
- `zombiekit:chests/material`
- `zombiekit:chests/meat`
- `zombiekit:chests/medical`
- `zombiekit:chests/monster`
- `zombiekit:chests/ore`
- `zombiekit:chests/projectile`
- `zombiekit:chests/scarasol_kyoko`
- `zombiekit:chests/tomb`
- `zombiekit:chests/tool`
- `zombiekit:chests/treasure`
- `zombiekit:chests/treasure_without_bonus`
- `zombiekit:chests/weapon`
- `zombiekit:grant_book_on_first_join`
- `minecraft:blocks/basalt` (override fornecido pelo mod)
- `minecraft:blocks/smooth_basalt` (override fornecido pelo mod)
- `minecraft:entities/bat` (override fornecido pelo mod)

### Legendary Survival Overhaul

São 22 tabelas: `blocks/cooler`, `blocks/heater`, `blocks/heater_top`,
`blocks/ice_fern_crop`, `blocks/ice_fern_gold`, `blocks/sewing_table`,
`blocks/sun_fern_crop`, `blocks/sun_fern_gold`, `blocks/water_plant_crop` e as
injeções `chests/abandoned_mineshaft`, `bastion_bridge`, `bastion_hoglin_stable`,
`bastion_other`, `bastion_treasure`, `buried_treasure`, `desert_pyramid`,
`jungle_temple`, `nether_bridge`, `pillager_outpost`, `entities/drowned`,
`gameplay/fishing/treasure`, `gameplay/piglin_bartering`.

O JAR `tacz_fallout` não contém loot tables. Ele contém um gunpack embutido.

## Itens catalogados

### Alimentos

- Chovy: `cannedbeef`, `cannedmutton`, `cannedpatato`, `cannedsalmon`,
  `cannedtuna`, `cheese`, `chocolate`, `cookedanchovy`, `corn`, `croissan`,
  `donut`, `flour`, `lettuce`, `milkbottle`, `mre`, `banana`, `onion`, `pepper`,
  `proteinbar`, `rawanchovy`, `soda`, `tomato`.
- Zombie Survival Kit: `canned_beans`, `canned_beef_hotpot`, `canned_bread`,
  `canned_fish_in_black_bean_sauce`, `canned_luncheon_meat`,
  `canned_tomatoes`, `canned_yellow_peach`, `chocolate`, `compressed_biscuit`.

### Armas melee e de fogo existentes

- Chovy melee: `aluminiumbat`, `baseballbat`, `baseballbat_2`, `crowbar`,
  `fireaxe`, `ironstick`, `katana`, `machete`, `militaryknife`, `pitchfork`,
  `policabaton`, `sledgehammer`, `wrench`.
- Chovy fogo: `ak_47`, `fiveseven`, `glockgun`, `m_4a_1`, `mac_10`, `mp_5`.
- Zombie Survival Kit melee: `baseball_bat`, `chainsaw`, `crowbar`, `fire_axe`,
  `knife`, `machete`, `rake`, `studded_baseball_bat`, `wrench` (mais variantes
  netherite, que não serão adicionadas ao loot).

### Munições

- Chovy: `pistolbulletitem`, `riflebulletitem`.
- Zombie Survival Kit: `heavy_machine_gun_ammo`, `fire_mortar_shell`,
  `mine_layer_mortar_shell`, `mortar_shell`, `smoke_mortar_shell`.
- Fallout gunpack: `fallout:10mm`, `fallout:2mm_ec`, `fallout:fusion_cell`.

### Armaduras

- Chovy: `policevest_chestplate` (leve) e `riotshield` (escudo, não armadura).
- Zombie Survival Kit leve: conjunto `skiing_*`.
- Zombie Survival Kit média: conjuntos `standard_tactical_*`,
  `forest_tactical_*`, `desert_tactical_*`, `snow_tactical_*`.
- Zombie Survival Kit pesada: conjuntos `standard_riot_*`, `forest_riot_*`,
  `desert_riot_*`, `snow_riot_*`, `bomb_*`, `exo_*`; todos excluídos do loot
  comum. `white_food_chestplate` também fica excluída.

### Armas Fallout disponíveis no gunpack

- Pistolas: `fallout:10mm_pistol`, `fallout:laser_pistol`.
- Rifles: `fallout:assault_rifle`, `fallout:gauss_rifle`,
  `fallout:laser_rifle`.
- Outras/especiais, excluídas da progressão inicial: `fallout:dzj08`,
  `fallout:qlz87`, `fallout:x26`.

## Plano de injeção (aguardando TACZ)

1. Criar tabelas auxiliares próprias, chamadas pelas tabelas-alvo com entradas
   ponderadas que incluam `minecraft:air`; assim nenhum item é garantido.
2. `cargobox` e `zombiekit:chests/building`: só munição e, raramente, armadura
   leve. Sem armas de fogo.
3. `foodcrate` e `zombiekit:chests/food`: somente enlatados, biscoitos e bebida
   já catalogados; sem alimento fresco adicional.
4. `medical`: água/itens médicos existentes apenas; não incluir armas.
5. `weaponcrate` e `zombiekit:chests/weapon`: melee comum, munição mais comum,
   pistola rara, SMG muito rara e rifle extremamente raro.
6. `gear`: armadura leve comum, média rara e pesada ausente do pool regular.
   Equipamento pesado somente poderá ser considerado em `treasure` após teste.
7. Limites de munição: pistola 2–8; SMG 4–12; rifle 2–6; escopeta 1–4. Nenhum
   stack grande.
8. Validar cada JSON com parser e carregar o pack em Forge 1.20.1; então criar
   um commit separado para cada grupo de tabelas.

## Bloqueio para implementação segura

Para materializar os IDs `fallout:*`, o datapack precisa da confirmação, dentro
do JAR TACZ instalado, de:

- item de arma e item de munição usados pelo TACZ;
- formato NBT/componentes que aponta para `fallout:<id>`;
- mecanismo suportado para injetar loot (substituição de tabela, global loot
  modifier ou integração do mod).

Adicione o JAR TACZ que corresponde ao gunpack ao projeto (ou informe seu
caminho). Depois disso, a implementação poderá criar JSONs válidos sem supor IDs.
