# WebFiction

Jakub Dančo

5ZYI36

## Stručný opis projektu
WebFiction je webová aplikácia určená na zdieľanie krátkych fiktívnych alebo nefiktívnych príbehov, fanfikcií a básní. Aplikácia reaguje na skutočnosť, že mnohé existujúce platformy sa zameriavajú najmä na dlhšie literárne diela, zatiaľ čo kratšie texty majú menší priestor.

Hlavným účelom aplikácie je vytvoriť jednoduché a prehľadné prostredie, v ktorom môžu noví aj skúsení autori publikovať svoju tvorbu a získavať čitateľov. Používatelia budú môcť príbehy čítať, vyhľadávať a filtrovať podľa autora, názvu alebo tagov a registrovaní používatelia budú môcť vytvárať vlastné príbehy, komentovať ich a hodnotiť.


## Role v projekte

### Návštevník
Návštevník je používateľ, ktorý nie je prihlásený do aplikácie. Môže si prezerať dostupné príbehy a vyhľadávať alebo filtrovať obsah. Pre vytváranie príbehov a pridávanie komentárov musí použiť registráciu alebo prihlásenie.

### Používateľ
Registrovaný používateľ môže vytvárať vlastné príbehy a pracovať s ich obsahom. Môže pridávať tagy, publikovať príbehy alebo ich uložiť ako návrh. Zároveň môže čítať príbehy ostatných používateľov, komentovať ich a hodnotiť ich.

### Administrátor
Administrátor je používateľ zodpovedný za správu aplikácie a dohľad nad jej obsahom. Má oprávnenie spravovať používateľov a odstraňovať nevhodné príbehy alebo komentáre.


## Prípady použitia podľa rolí

### Návštevník
- návštevník si prezrie zoznam najnovších alebo najpopulárnejších príbehov,
- návštevník vyhľadá príbeh podľa názvu alebo autora,
- návštevník filtruje príbehy podľa tagov,
- návštevník si otvorí detail príbehu a prečíta jeho obsah,
- návštevník sa zaregistruje alebo prihlási.

### Registrovaný používateľ
- používateľ si vytvorí nový príbeh,
- používateľ zadá názov, text a tagy príbehu,
- používateľ publikuje príbeh,
- používateľ uloží príbeh ako návrh,
- používateľ si prečíta príbehy ostatných autorov,
- používateľ pridá komentár k príbehu,
- používateľ ohodnotí príbeh,
- používateľ si zobrazí a upraví svoj profil,
- používateľ si zobrazí svoje príbehy a obľúbené príbehy.

### Administrátor
- administrátor spravuje registrovaných používateľov,
- administrátor odstráni nevhodný príbeh,
- administrátor odstráni nevhodný komentár.


## Plánované entity

### User
Reprezentuje registrovaného používateľa aplikácie, ktorý môže vytvárať a hodnotiť príbehy.

**Najdôležitejšie atribúty:**
- `id` – primárny kľúč,
- `username` – jedinečné meno používateľa,
- `email` – jedinečná e-mailová adresa,
- `password_hash` – hashované heslo,
- `created_at` – dátum registrácie.

**Vzťahy:**
- `User` - `Story` 1:N
- `User` - `Like` N:M
- `User` - `Comment` N:M

### Story
Reprezentuje krátky príbeh vytvorený používateľom.

**Najdôležitejšie atribúty:**
- `id` – primárny kľúč,
- `title` – názov príbehu,
- `content` – text príbehu,
- `author_id` – cudzí kľúč na používateľa,
- `created_at` – dátum vytvorenia,
- `likes` – počet hodnotení.

**Vzťahy:**
- `Story` - `User` N:1
- `Story` - `Like` 1:N
- `Story` - `Comment` 1:N
- `Story` - `Tag` N:M

### Comment
Reprezentuje komentár používateľa k príbehu.

**Najdôležitejšie atribúty:**
- `id` – primárny kľúč,
- `content` – text komentára,
- `story_id` – cudzí kľúč na príbeh,
- `user_id` – cudzí kľúč na používateľa,
- `created_at` – dátum vytvorenia.

**Vzťahy:**
- `Comment` - `User` M:N
- `Comment` - `Story` N:1

### Like
Reprezentuje hodnotenie príbehu používateľom.

Najdôležitejšie atribúty:
- `story_id` – súčasť primárneho kľúča a odkaz na príbeh,
- `user_id` – súčasť primárneho kľúča a odkaz na používateľa.

**Vzťahy:**
- `Like` - `User` M:N
- `Like` - `Story` N:1

### Tag
Reprezentuje označenie kategórie alebo žánru príbehu.

Najdôležitejší atribút:
- `name` – názov tagu a primárny kľúč.

**Vzťahy:**
- `Tag` - `Story` M:N


## Vzťahy medzi entitami
- **User – Story: 1:N** – jeden používateľ môže vytvoriť viac príbehov, pričom každý príbeh má jedného autora.
- **Story – Comment: 1:N** – jeden príbeh môže obsahovať viac komentárov.
- **User – Like: N:M** – používateľ môže hodnotiť viac príbehov a jeden príbeh môže byť hodnotený viacerými používateľmi.
- **Story – Tag: N:M** – jeden príbeh môže mať viac tagov a jeden tag môže byť priradený viacerým príbehom.


## Hlavné stránky aplikácie

### 1. Domovská stránka
Zobrazuje zoznam najnovších alebo najpopulárnejších príbehov. Každý príbeh je prezentovaný ako karta s názvom, úryvkom textu, menom autora, dátumom publikovania a počtom lajkov. Stránka obsahuje vyhľadávanie, zoznam príbehov a tlačidlo na pridanie príbehu pre prihlásených používateľov.

### 2. Stránka príbehu
Zobrazuje celý text vybraného príbehu, jeho názov, autora, dátum publikovania, počet zobrazení a hodnotení. Súčasťou stránky je sekcia komentárov a možnosti interakcie s príbehom.

### 3. Stránka „Napíš príbeh“
Slúži na vytvorenie nového príbehu. Obsahuje formulár s poľami pre názov, text a tagy. Používateľ môže príbeh publikovať alebo uložiť ako návrh.

### 4. Používateľský profil
Zobrazuje základné informácie o autorovi, jeho príbehy a obľúbené príbehy. Používateľ môže upraviť svoj profil a profilový obrázok.

### 5. Registrácia a prihlásenie
Slúži na vytvorenie používateľského účtu a prihlásenie registrovaného používateľa. Po prihlásení používateľ získava možnosť vytvárať príbehy a pridávať komentáre a hodnotenia.


## Rozdelenie funkcionality

### Základné funkcie
Základ predstavuje funkcionalitu potrebnú na splnenie hlavného účelu aplikácie:

- registrácia a prihlásenie používateľa,
- zobrazenie zoznamu príbehov,
- zobrazenie detailu príbehu,
- vyhľadávanie a filtrovanie príbehov podľa autora, názvu alebo tagov,
- vytvorenie nového príbehu,
- zadanie názvu, textu a tagov príbehu,
- publikovanie príbehu,
- uloženie príbehu ako návrhu,
- komentovanie príbehov,
- hodnotenie príbehov,
- zobrazenie používateľského profilu a jeho príbehov.

### Rozširujúce funkcie
Ako rozšírenie základnej funkcionality je možné podľa časových možností doplniť napríklad rozšírené možnosti práce s profilom, obľúbenými príbehmi alebo ďalšie možnosti filtrovania a kategorizácie obsahu.
