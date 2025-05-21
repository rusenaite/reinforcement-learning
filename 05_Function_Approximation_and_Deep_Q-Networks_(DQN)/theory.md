# Funkcijų aproksimacija ir gilieji Q tinklai (DQN)

## 💡 Teorinė dalis

### Funkcijų aproksimacija

Funkcijų aproksimacija yra technika, naudojama stiprinamojo mokymosi (Reinforcement Learning, RL) kontekste, kai būsenų erdvė yra labai didelė arba net begalinė. Vietoje to, kad būtų kaupiamos visos būsenų-veiksmų poros Q reikšmės, naudojamas modelis (pvz., neuroninis tinklas), kuris apytiksliai apskaičiuoja šias vertes.

---

## 🧠 Deep Q-Networks (DQN)

### Kas yra DQN?

DQN – tai gilusis Q-mokymosi metodas, kuris neuroniniu tinklu aproksimuojamos Q reikšmės, leidžiančios efektyviai veikti didelėse būsenų erdvėse. Šis metodas išpopuliarėjo po 2015 m. pasirodžiusio darbo, kuriame DQN pasiekė žmogaus lygio rezultatų žaidžiant Atari žaidimus.

### Pagrindiniai komponentai:

- **Q tinklas:** Naudoja neuroninį tinklą Q(s, a) prognozei.
- **Patirties atkartojimas (Experience Replay):** Agentas saugo ankstesnius patyrimus ir mokosi iš jų atsitiktine tvarka, kad sumažintų sekos koreliaciją.
- **Tikslinis tinklas (Target Network):** Atskiras tinklas, kuris atnaujinamas retai, kad užtikrintų stabilumą mokymo metu.

---

## 🔁 Double DQN

### Problema:
Klasikinis DQN pervertina Q reikšmes, nes tas pats tinklas naudojamas ir veiksmo parinkimui, ir įvertinimui.

### Sprendimas:
Double DQN naudoja du tinklus:
- Vienas parenka geriausią veiksmą (`argmax`),
- Kitas įvertina to veiksmo reikšmę naudodamas atskirus svorius (`θ⁻`).

### Formulė:
```
Q(s, a) = r + γ * Q_target(s', argmax_a' Q(s', a'; θ), θ⁻)
```

---

## 🧾 Dueling DQN

### Problema:
Kai kuriose būsenose veiksmo pasirinkimas neturi didelės reikšmės, bet klasikinis DQN vis tiek modeliuoja visas Q reikšmes vienodai.

### Sprendimas:
Dueling DQN tinklo architektūra atskiria:
- **V(s):** būsena vertė,
- **A(s, a):** veiksmo pranašumas.

### Formulė:
```
Q(s, a) = V(s) + A(s, a) - max_a' A(s, a')
```

---

## 📍 Apibendrinimas

- **DQN:** sprendžia didelių erdvių problemas naudodamas neuroninius tinklus.
- **Double DQN:** sumažina Q reikšmių pervertinimą.
- **Dueling DQN:** leidžia tinklui geriau įvertinti būsenas net kai veiksmo pasirinkimas nėra svarbus.

---

## 🧪 Praktiniai DQN panaudojimo atvejai

### 1. Žaidimai (pvz., Atari)
- **Breakout, Space Invaders, Pong, Ms. Pac-Man**
- Agentas mokosi žaisti siekdamas maksimizuoti rezultatą.

### 2. Autonominės transporto priemonės
- **Veiksmai:** vairavimas, stabdymas, sukimas
- **Atlygis:** pasiektas tikslas, išvengtos kliūtys

### 3. Robotų valdymas
- **Užduotys:** objektų paėmimas, judėjimas
- **Atlygis:** sėkmingas užduoties atlikimas

### 4. Finansai
- **Veiksmai:** pirkti, parduoti, laikyti
- **Atlygis:** pelnas ar nuostolis

### 5. Sistemų ir tinklų optimizavimas
- **Būsena:** tinklo srautas, serverio apkrova
- **Veiksmai:** resursų paskirstymas
- **Atlygis:** optimizuota veikla

---

## 📚 Naudingi šaltiniai

- [IEEE publikacija](https://ieeexplore.ieee.org/abstract/document/10854435)
- Mnih et al., 2015 – "Human-level control through deep reinforcement learning"
- Wang et al., 2016 – "Dueling Network Architectures for Deep Reinforcement Learning"
- [Kaggle notebook: Dueling Double DQN](https://www.kaggle.com/code/masurte/dueling-double-dqn)
