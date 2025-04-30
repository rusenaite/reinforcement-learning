# Kas yra stiprinamasis mokymasis? (Reinforcement Learning, RL)

**Stiprinamasis mokymasis** (angl. *Reinforcement Learning*) yra mokymosi metodas, kuriame agentas mokosi geriausios elgsenos (veiksmų sekos), siekdamas maksimaliai padidinti ilgalaikį atlygį sąveikaudamas su aplinka.

Skirtingai nei priežiūrimas mokymas (*supervised learning*), čia nėra pateikiamas teisingas atsakymas. Agentas mokosi iš patirties: jis bando veiksmus, stebi pasekmes ir prisitaiko.

---

## Pagrindinės sąvokos

| Sąvoka           | Paaiškinimas |
|------------------|--------------|
| **Agentas**      | Sprendimus priimantis "veikėjas" |
| **Aplinka**      | Pasaulis, su kuriuo sąveikauja agentas |
| **Veiksmas (action)** | Agentas atlieka veiksmus (pvz., judėti, sukti) |
| **Būsena (state)**    | Aplinkos situacija tam tikru momentu |
| **Atlygis (reward)**  | Skaičius, kuris rodo, kaip gerai pasielgė agentas |
| **Strategija (policy)** | Taisyklė, kaip agentas pasirenka veiksmus |
| **Vertės funkcija (value function)** | Prognozuojamas būsimos naudos dydis iš būsimos būsenos |

---

## Stiprinamojo mokymosi ciklas

1. Agentas yra būsenoje \( s \)
2. Pasirenka veiksmą \( a \) pagal strategiją \( \pi \)
3. Aplinka pateikia naują būseną \( s' \) ir atlygį \( r \)
4. Agentas atnaujina savo žinias
5. Kartojama

---

## Q-learning – pagrindinis algoritmas

Q-learning yra vienas populiariausių RL algoritmų. Jis palaiko Q lentelę \( Q(s, a) \), kurioje saugoma, kaip geras yra tam tikras veiksmas konkrečioje būsenoje.

### Atnaujinimo formulė:

\[ Q(s,a) \leftarrow Q(s,a) + \alpha \left( r + \gamma \max_{a'} Q(s', a') - Q(s,a) \right) \]

Kur:
- \( \alpha \) – mokymosi greitis
- \( \gamma \) – nuolaidos koeficientas
- \( r \) – atlygis
- \( s' \) – nauja būsena
- \( a' \) – galimas veiksmas naujoje būsenoje

---

## Veikimo principas

- **Veiksmų pasirinkimas**: Agentas renkasi veiksmą pagal strategiją
- **Aplinkos reakcija**: Nauja būsena ir atlygis
- **Žinių atnaujinimas**: Remiantis gauta informacija, atnaujinama Q reikšmė

---

## Markovo sprendimų procesas (MDP)

MDP yra RL formali struktūra:

- \( S \): galimų būsenų aibė
- \( A \): galimų veiksmų aibė
- \( P(s'|s,a) \): perėjimo tikimybė
- \( R(s,a) \): atlygis
- \( \gamma \): nuolaidos koeficientas

### Markovo savybė
Ateitis priklauso tik nuo dabartinės būsenos – ne nuo praeities.

### Bellmano lygtis

\[ V^*(s) = \max_a \left[ R(s,a) + \gamma \sum_{s'} P(s'|s,a)V^*(s') \right] \]

---

## RL algoritmai

### 1. Q-learning
- Modelio nepriklausomas
- Veikia su Q(s, a) lentele

### 2. Deep Q-learning (DQN)
- Naudoja neuroninius tinklus Q(s, a) aproksimacijai
- Tinka sudėtingoms aplinkoms (vaizdai, žaidimai)

### 3. Policy Gradient metodai
- Tiesiogiai optimizuoja politiką \( \pi(a|s) \)
- Naudoja gradientų metodus

---

## Pavyzdžiai

- **FrozenLake** – RL klasika: ežero perėjimas neįkrentant į duobes
- **Atari žaidimai** – Mokymas žaisti žaidimus nuo nulio
- **Autonominis vairavimas** – RL naudojamas sprendimams kelyje priimti

---

## Naudojimo sritys

| Sritis           | Pritaikymas |
|------------------|-------------|
| **Robotika**     | Judėjimas, objektų surinkimas |
| **Finansai**     | Investavimo strategijos |
| **Sveikatos apsauga** | Gydymo plano optimizavimas |
| **Žaidimų kūrimas** | Žaidimų agentai mokosi ir tobulėja |

---

## Naudingos nuorodos
- [ACM Reinforcement Learning Overview](https://dl.acm.org/doi/full/10.1145/3616864)
- [Introduction to RL Course](https://towardsdatascience.com/reinforcement-learning-introduction-and-main-concepts-48ea997c850c/?source=post_page-----7ce2828a1fdb---------------------------------------)
