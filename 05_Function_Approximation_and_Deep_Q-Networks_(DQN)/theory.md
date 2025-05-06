# Q-mokymasis ir SARSA Reinforcement Learning Metodai

## Įžanga

Q-mokymasis yra intuityvi, bet sudėtinga technika, priklausanti sustiprinto mokymosi (reinforcement learning) sričiai, kuri pati yra mašininio mokymosi pogrupis. Įsivaizduokime agentą, kaip smalsų vaiką žaidimų aikštelėje, kuris mokosi aplinkos per bandymus ir klaidas. Kiekvienas veiksmas turi pasekmes, o kiekvienas bandymas atskleidžia daugiau informacijos apie aplinką. Tai yra Q mokymosi esmė: jis įgalina agentą mokytis interaktyvioje aplinkoje, imantis veiksmų, stebint rezultatus ir pritaikant savo strategiją siekiant geresnių rezultatų ateityje.

## Q-mokymosi pagrindai

Šis metodas išsiskiria gebėjimu išmokti optimalius veiksmus be aplinkos modelio, o pasikliaujant atlygio sistema. Tai tarsi mokymasis spręsti labirintą užmerktomis akimis, vadovaujantis tik atsiliepimais iš sienų ir džiaugsmo šūksniais artėjant prie išėjimo. Ši grįžtamojo ryšio kilpa apima Q mokymosi algoritmų mokymosi kelionę.

### Q lentelė

Q-mokymosi esmė yra Q lentelė – kiekvienas įrašas parodo būsenos (s) ir veiksmo (a) derinį.

Pradinė lentelė yra tuščia. Atnaujinimas vyksta naudojant formulę:

```
Q(s,a) ← Q(s,a) + α [R(s,a) + γ max_a Q(s',a) − Q(s,a)]
```

Kur:

- **α** – mokymosi greitis
- **γ** – nuolaidos veiksnys
- **R(s,a)** – atlygis
- **s'** – būsena po veiksmo

### Tyrinėjimas ir išnaudojimas

- **Tyrinėjimas** – naujų veiksmų išbandymas, kaip mokslininko eksperimentas.
- **Išnaudojimas** – turimų žinių panaudojimas geriausiam sprendimui priimti.

### Parametrai:

- **Mokymosi greitis (α):** Kaip greitai agentas atnaujina Q reikšmes. Didelis α – greitesnis mokymasis, mažas – atsargesnis.
- **Nuolaidų faktorius (γ):** Kaip svarbūs būsimi atlygiai. Didelis γ – ilgalaikė strategija, mažas – trumpalaikis pelnas.

Atlygio sistema veikia kaip elgesio psichologijoje – apdovanojimai ir bausmės formuoja elgesį.

## Q-learning vs SARSA

### Q-learning

Q-learning yra off-policy algoritmas, kuris mokosi pagal vertinimą, nepriklausomai nuo agento faktiškai atliktų veiksmų.

#### Formulė:

```
Q(s,a) ← Q(s,a) + α [R(s,a) + γ max_a Q(s',a) − Q(s,a)]
```

#### Ypatybės:

- **Off-policy:** Mokosi pagal vertinimą, nepriklausomai nuo politikos.
- **Naudoja maksimalų Q vertinimą:** Atnaujina pagal optimalią strategiją.
- **Gali pervertinti Q vertes.**

### SARSA

SARSA yra on-policy algoritmas, kuris mokosi pagal dabartinę politiką, naudodamas faktiškai atliktus veiksmus.

#### Formulė:

```
Q(s,a) ← Q(s,a) + α [R(s,a) + γ Q(s',a') − Q(s,a)]
```

#### Ypatybės:

- **On-policy:** Mokosi pagal realią strategiją.
- **Naudoja veiksmą a', kurį agentas tikrai atliko.**
- **Mažesnė rizika pervertinti Q reikšmes.**

### Palyginimas:

| Aspektas               | Q-mokymas (Off-policy)             | SARSA (On-policy)                     |
| ---------------------- | ---------------------------------- | ------------------------------------- |
| Politika               | Nepriklauso nuo politikos          | Remiasi politika                      |
| Atnaujinimas           | Naudoja max Q(s', a)               | Naudoja Q(s', a')                     |
| Tyrinėjimas            | Apsvarsto geriausią veiksmą        | Vadovaujasi faktiniais veiksmais      |
| Konsolidacijos greitis | Greitesnis                         | Lėtesnis                              |
| Stabilumas             | Mažesnis, linkęs į pervertinimą    | Didesnis, stabilesnis                 |
| Tinkamumas             | Agresyvus tyrimas ir optimizavimas | Stabilumas ir politikos suderinamumas |
| Suboptimalumo rizika   | Maža                               | Didesnė                               |

## Funkcijų aproksimacija ir gilieji Q tinklai (DQN)

### Funkcijų aproksimacija

Kai būsenų erdvė yra labai didelė arba begalinė, Q-vertes tampa neįmanoma išlaikyti lentelėje. Funkcijų aproksimacija leidžia naudoti modelį, pvz., neuroninį tinklą, kuris apytiksliai apskaičiuoja Q-vertes.

### DQN (Deep Q-Network)

DQN sujungia gilųjį neuroninį tinklą su Q-mokymusi. Pagrindiniai komponentai:

- **Neuroninis tinklas Q-vertėms:** Vietoje Q lentelės naudojamas tinklas.
- **Atminties atstatymas (Experience Replay):** Agentas saugo ankstesnes patirtis ir jas vėliau naudoja mokymuisi.
- **Tikslinis tinklas (Target Network):** Stabilumui pasiekti, naudojamas atskiras tinklas, kuris atnaujinamas periodiškai.

### Double DQN

- **Problema:** DQN gali pervertinti Q reikšmes.
- **Sprendimas:** Naudojami du tinklai – vienas veiksmo pasirinkimui, kitas vertinimui.

Formulė:

```
Q_double(st, at) = rt+1 + γ * Q_target(st+1, argmax_a' Q(st+1, a'; θ); θ−)
```

### Dueling DQN

- **Problema:** Ne visose būsenose visi veiksmai yra svarbūs.
- **Sprendimas:** Išskaidoma į vertės funkciją V(s) ir advanto funkciją A(s,a).

Formulė:

```
Q(s,a) = V(s) + A(s,a) − max_a' A(s,a')
```

### Apibendrinimas

- DQN leidžia naudoti gilųjį mokymąsi Q-vertėms.
- Double DQN mažina pervertinimo riziką.
- Dueling DQN padeda geriau įvertinti būsenos ir veiksmo svarbą.

## DQN panaudojimo atvejai

1. **Žaidimai (Atari, Pong, Breakout):**
2. **Autonominės transporto priemonės:**
3. **Robotų valdymas:**
4. **Finansų sprendimai:**
5. **Sistemų ir tinklų optimizavimas:**

## Išvada

Q-mokymasis agresyviai ieško optimalios politikos, bet gali pervertinti Q reikšmes. SARSA laikosi dabartinės politikos, todėl yra stabilesnis ir saugesnis. DQN ir jo variantai – Double DQN, Dueling DQN – leidžia spręsti sudėtingas užduotis didelėse erdvėse. Pasirinkimas priklauso nuo tikslų – ar norima optimalaus elgesio bet kokia kaina, ar svarbiau stabilumas ir saugumas.

Pavyzdžiai ir straipsniai:

- [Kaggle – Solving MDP using TD Learning](https://www.kaggle.com/code/editama/solving-mdp-using-td-learning)
- [Kaggle – Dueling Double DQN](https://www.kaggle.com/code/masurte/dueling-double-dqn)
- [IEEE – Deep Reinforcement Learning Paper](https://ieeexplore.ieee.org/abstract/document/10854435)
