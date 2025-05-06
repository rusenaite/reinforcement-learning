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

* **α** – mokymosi greitis
* **γ** – nuolaidos veiksnys
* **R(s,a)** – atlygis
* **s'** – būsena po veiksmo

### Tyrinėjimas ir išnaudojimas

* **Tyrinėjimas** – naujų veiksmų išbandymas, kaip mokslininko eksperimentas.
* **Išnaudojimas** – turimų žinių panaudojimas geriausiam sprendimui priimti.

### Parametrai:

* **Mokymosi greitis (α):** Kaip greitai agentas atnaujina Q reikšmes. Didelis α – greitesnis mokymasis, mažas – atsargesnis.
* **Nuolaidų faktorius (γ):** Kaip svarbūs būsimi atlygiai. Didelis γ – ilgalaikė strategija, mažas – trumpalaikis pelnas.

Atlygio sistema veikia kaip elgesio psichologijoje – apdovanojimai ir bausmės formuoja elgesį.

## Q-learning vs SARSA

### Q-learning

Q-learning yra off-policy algoritmas, kuris mokosi pagal vertinimą, nepriklausomai nuo agento faktiškai atliktų veiksmų.

#### Formulė:

```
Q(s,a) ← Q(s,a) + α [R(s,a) + γ max_a Q(s',a) − Q(s,a)]
```

#### Ypatybės:

* **Off-policy:** Mokosi pagal vertinimą, nepriklausomai nuo politikos.
* **Naudoja maksimalų Q vertinimą:** Atnaujina pagal optimalią strategiją.
* **Gali pervertinti Q vertes.**

### SARSA

SARSA yra on-policy algoritmas, kuris mokosi pagal dabartinę politiką, naudodamas faktiškai atliktus veiksmus.

#### Formulė:

```
Q(s,a) ← Q(s,a) + α [R(s,a) + γ Q(s',a') − Q(s,a)]
```

#### Ypatybės:

* **On-policy:** Mokosi pagal realią strategiją.
* **Naudoja veiksmą a', kurį agentas tikrai atliko.**
* **Mažesnė rizika pervertinti Q reikšmes.**

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

## Naudojimo atvejai

### Q-learning:

* **Robotika:** Robotas mokosi naršyti labirinte.
* **Žaidimų AI:** Mokomas žaisti šachmatais, Go.
* **Autonominės transporto priemonės:** Sprendimų priėmimas eisme, pvz., stabdymas, kliūčių vengimas.
* **Rekomendacijų sistemos:** Rekomenduoja filmus, naudodamas tyrimą ir optimizavimą.

### SARSA:

* **Robotika:** Robotas paima daiktus nuo stalo, vengdamas rizikos (numesti objektą).
* **Žaidimai:** Kryžiukai-nuliukai, paprasti arkadiniai žaidimai.
* **Navigacija su apribojimais:** Robotas sandėlyje su kliūtimis – laikosi saugumo politikos.
* **Sveikatos priežiūra:** Individualizuotas gydymas, reaguojant į paciento rezultatus realiu laiku.

## Išvada

Q-mokymasis agresyviai ieško optimalios politikos, bet gali pervertinti Q reikšmes. SARSA laikosi dabartinės politikos, todėl yra stabilesnis ir saugesnis. Pasirinkimas priklauso nuo tikslų – ar norima optimalaus elgesio bet kokia kaina, ar svarbiau stabilumas ir saugumas.

Pavyzdys: [Kaggle pavyzdys – Solving MDP using TD Learning](https://www.kaggle.com/code/editama/solving-mdp-using-td-learning)
