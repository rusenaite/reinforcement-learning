# Politikos gradiento metodai (Policy Gradient Methods)

Politikos gradiento metodai yra viena iš giliųjų stiprinamojo mokymosi (Reinforcement Learning) šakų, kurioje tiesiogiai optimizuojama politika — sprendimų priėmimo strategija, pagal kurią agentas mokosi priimti veiksmus.

---

## 🎯 Politikos parametrizavimas

### 🔹 Diskretūs veiksmai

Kai veiksmai yra baigtiniai (pvz., judėjimas į kairę, dešinę), politika gali būti apibrėžta kaip tikimybės funkcija:

```
πθ(a|s) = softmax(ws)
```
Kur `ws` – būsenos priklausomi svoriai.

### 🔹 Nuolatiniai veiksmai

Jeigu veiksmai yra nepertraukiami, politika gali būti apibrėžta kaip pasiskirstymo funkcija, pavyzdžiui:

```
πθ(a|s) = N(a; μs, σs)
```
Kur `μs` ir `σs` – priklauso nuo būsenos `s`.

---

## 📐 Politikos gradiento teorema

Teorema leidžia apskaičiuoti, kaip keisti politikos parametrus θ, kad maksimalizuotume atlygį:

```
∇θ J(θ) = Eπθ [∇θ log πθ(a|s) Qπθ(s,a)]
```

Kur:

- `J(θ)` – tikslinė funkcija (tikėtinas bendras atlygis).
- `πθ(a|s)` – tikimybė pasirinkti veiksmą `a` būsenoje `s`.
- `Qπθ(s, a)` – Q reikšmė, įvertinanti veiksmų naudą.
- `∇θ log πθ(a|s)` – politikos logaritminis gradientas.

---

## 🧮 Politikos gradiento algoritmas

1. **Inicializacija:** pasirenkama pradine parametrizuota politika `πθ`.
2. **Duomenų surinkimas:** agentas atlieka veiksmus pagal `πθ` ir kaupia epizodus su atlygio reikšmėmis.
3. **Gradiento apskaičiavimas:** naudojant politikos gradiento formulę.
4. **Parametrų atnaujinimas:** atliekamas naudojant SGD arba Adam optimizatorių.

---

## ✅ Privalumai

- **Tiesioginis politikos optimizavimas** – nereikia modeliuoti Q funkcijos.
- **Palaiko nuolatinės veiksmo erdves** – tinkamas kontroliuojamiems veiksmams.
- **Stabilus veikimas** – naudojant patobulinimus, pvz., PPO.

---

## ❌ Trūkumai

- **Didelis variabilumas** – gradientai triukšmingi, reikalinga daug epizodų.
- **Didelis duomenų poreikis** – reikia daug patirties efektyviam mokymuisi.

---

## 🧾 Santrauka

Politikos gradiento metodai leidžia tiesiogiai mokytis optimalios politikos, naudojant atlygio signalus ir gradientų skaičiavimus. Šie metodai ypač naudingi sudėtingose, nuolatinėse veiksmų erdvėse.

---

📚 Daugiau informacijos:  
[Policy Gradient Methods – Arxiv](https://arxiv.org/pdf/2401.13662)
