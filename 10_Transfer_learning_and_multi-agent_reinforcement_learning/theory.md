# 1. Mokymasis perkėlimu stiprinimo mokyme (Transfer Learning in Reinforcement Learning)

## 1.1 Apibrėžimas ir motyvacija

Mokymasis perkėlimu (angl. *transfer learning*) – tai metodas, kai agentas panaudoja žinias, įgytas vienoje užduotyje ar aplinkoje, tam, kad greičiau ir efektyviau mokytųsi kitoje, susijusioje, bet ne identiškoje užduotyje.

Mokymasis nuo nulio (angl. *tabula rasa*) dažnai neefektyvus, ypač kai:

* Treniruotė užima daug laiko ir skaičiavimo resursų.
* Yra mažai duomenų ar sąveikų su aplinka.
* Aplinka kinta, bet turi bendrų bruožų su ankstesne.

| Perkėlimo rūšis                | Aprašymas                                            | Pavyzdys                                        |
| ------------------------------ | ---------------------------------------------------- | ----------------------------------------------- |
| Horizontalus (užduočių)        | Žinios perkeliamos iš vienos užduoties į kitą.       | Nuo CartPole prie MountainCar                   |
| Vertikalus (duomenų, funkcijų) | Išmokti reprezentacijų ar parametrų perkėlimas.      | CNN svoriai iš vienos aplinkos į kitą           |
| Intra-task                     | Žinių perkėlimas tarp epizodų toje pačioje užduotyje | Mokymasis nuo ankstesnių epizodų                |
| Inter-task                     | Žinių perkėlimas tarp skirtingų užduočių             | Nuo labirinto navigacijos prie objektų suradimo |

## 1.2 Tipiniai pavyzdžiai

* Agentas, kuris išmoko valdyti automobilį simuliatoriuje, perkelia įgūdžius į realaus pasaulio valdymą.
* Robotas, išmokęs vaikščioti plokščiu paviršiumi, turi prisitaikyti prie nelygaus reljefo.

## 1.3 Transfer learning strategijos RL

### Politikos perkėlimas (*policy transfer*)

* Perkeliama tiesiogiai išmokta politika į naują aplinką.
* Dažnai naudojama kaip pradinė būsena naujam mokymui (*fine-tuning*).

### Reikšmės funkcijos perkėlimas (*value transfer*)

* Vietoj politikos, perduodamos apytikslės Q-funkcijos arba vertės funkcijos.
* Gali padėti greičiau konverguoti vertės iteracijai.

### Funkcijų bendrinimas (*feature sharing*)

* Apmokomi bendri reprezentaciniai sluoksniai (pvz., CNN vaizdams), kurie naudojami skirtingoms RL užduotims.

### Modelio perkėlimas

* Jeigu turime modelį aplinkos dinamikai (*transition model*), jį galima perkelti.

### Multi-task ir meta-learning

* Agentas treniruojamas per kelias užduotis, kad vėliau gebėtų greitai prisitaikyti prie naujų (pvz., MAML – *Model-Agnostic Meta Learning*).

| Sritis                    | Perkėlimo taikymas                                           |
| ------------------------- | ------------------------------------------------------------ |
| Robotika                  | Iš simuliacijos į realybę ("sim2real")                       |
| Žaidimai                  | Išmokta politika Pong'e panaudojama Breakout                 |
| Pramonė                   | Gamybos linijos robotai pritaikomi naujiems produktams       |
| Autonominiai automobiliai | Mokymasis įvairiomis sąlygomis (lietus, sniegas, naktis)     |
| Finansai                  | Mokymasis iš istorinių duomenų, perkeliant į realias sąlygas |

## 1.4 Iššūkiai

* *Negative transfer* – kai perkeltos žinios trukdo mokymuisi (pvz., labai skirtingos dinamikos).
* Panašumo tarp užduočių įvertinimas – reikia apibrėžti, ar užduotys pakankamai susijusios.
* Aplinka gali būti *ne-stacionari* – keičiasi laike.

# 2. Kelių agentų stiprinimo mokymasis (Multi-Agent Reinforcement Learning, MARL)

## 2.1 Apibrėžimas

MARL – tai RL išplėtimas, kai ne vienas, o keli agentai mokosi ir sąveikauja bendroje aplinkoje. Agentai gali:

* Bendradarbiauti (pvz., komandinis darbas),
* Konkuruoti (pvz., žaidimai ar resursų varžybos),
* Veikti mišriomis sąlygomis (kai kurios sąveikos bendradarbiaujančios, kitos – konkurencinės).

## 2.2 Aplinkos formalizavimas

MARL dažniausiai modeliuojamas per Markovo žaidimus (*Markov Games*):

* Turi agentų aibę $N$,
* Kiekvienas agentas turi savo politiką $\pi_i(a_i\mid s)$,
* Aplinka turi bendrą būseną $s$, kuri kinta priklausomai nuo visų agentų veiksmų $a_1, a_2, ..., a_N$,
* Kiekvienas agentas gauna individualų atlygį $r_i$.

## 2.3 MARL scenarijų klasifikacija

### Bendradarbiaujantys agentai

* Visi siekia bendro tikslo.
* Pvz., dronai, padedantys vieni kitiems surasti paieškos taikinius.

### Konkuruojantys agentai

* Agentų tikslai prieštaringi, dažnai nulinės sumos žaidimai.
* Pvz., „Pong“, „šachmatai“, strateginiai žaidimai.

### Mišrūs scenarijai

* Kai kurie agentai bendradarbiauja, kiti – konkuruoja.
* Pvz., robotų komandos futbolo varžybose.

## 2.4 MARL metodai

* **Independent Q-Learning** – kiekvienas agentas mokosi atskirai, laikydamas kitus fiksuotais.
* **MADDPG (Multi-Agent Deep Deterministic Policy Gradient)** – agentai treniruojami centralizuotai su kitų agentų veiksmais kaip įėjimais, bet veikia decentralizuotai.
* **QMIX** – Q-funkcijos kombinuojamos taip, kad išlaikytų monotoniškumą, leidžiant decentralizuotą politikos vykdymą.
* **Self-Play** – agentas treniruojasi žaisdamas prieš savo kopiją (naudinga konkurenciniuose scenarijuose).
* **Parameter Sharing** – keli agentai dalinasi tą pačią politiką, kai jų veikimo struktūra yra identiška.

## 2.5 MARL iššūkiai

* *Ne-stacionari aplinka* – kai agentai mokosi tuo pačiu metu, kintančios politikos trukdo stabilumui.
* Koreliacija tarp agentų veiksmų – sudėtinga koordinacija.
* Sproginantis būsenų/veiksmų skaičius – augant agentų skaičiui.

| Sritis                             | Aprašymas                                      |
| ---------------------------------- | ---------------------------------------------- |
| Robotų komandos                    | Pvz., dronų spiečius, robotų futbolas          |
| Autonominiai transporto sprendimai | Automobilių koordinacija sankryžose            |
| Ekonomika ir prekyba               | Derybų agentai, rinkos modeliavimas            |
| Kompiuteriniai žaidimai            | Pvz., AlphaStar, OpenAI Five                   |
| Karinės simuliacijos               | Strateginis planavimas kelių vienetų kontekste |
