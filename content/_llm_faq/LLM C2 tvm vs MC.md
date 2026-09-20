
# Teorema do Valor Médio para Integrais e Monte Carlo


Excelente pergunta! A ligação entre o **TVMI** e o **Método de Monte Carlo** é direta: **Monte Carlo é a versão estatística (e numérica) do TVMI**, usada quando a integral é muito complicada ou tem muitas dimensões.

Enquanto o TVMI é **determinístico** (garante a existência de um $c$ exato), o Monte Carlo é **probabilístico** (estima o valor médio usando amostras aleatórias).

---

## A Fórmula que os Une

Pelo TVMI, o valor médio de $f$,  $\langle f \rangle$, em $[a; b]$ é:

$$
\langle f \rangle = \frac{1}{b-a} \int_a^b f(x) dx
$$

No Monte Carlo, aproximamos essa média pela **média aritmética** de \(N\) pontos sorteados aleatoriamente no intervalo:

$$
\langle f \rangle \approx \frac{1}{N} \sum_{i=1}^{N} f(x_i), \quad x_i \sim \text{Uniforme}(a,b)
$$

Assim, a integral é estimada por:

$$
\int_a^b f(x) dx \approx \frac{b-a}{N} \sum_{i=1}^{N} f(x_i)
$$

---

## Exemplo: $\int_0^1 x^2 dx$

- **Valor exato**: $1/3 \approx 0{,}3333$
- **Monte Carlo com 5 pontos** ($x$ sorteados): 0,12; 0,67; 0,45; 0,89; 0,31
  - $f(x)$: 0,0144 + 0,4489 + 0,2025 + 0,7921 + 0,0961 = 1,554
  - **Estimativa** = $\frac{1}{5} \times 1{,}554 = 0{,}3108$ (erro ~6,7%)

Com mais pontos (ex: 10.000), a estimativa converge para $0,3333$ pela **Lei dos Grandes Números**.

---

## Comparação Rápida

| Característica | TVMI              | Monte Carlo                   |
| :------------- | :---------------- | :---------------------------- |
| **Natureza**   | Exato (teórico)   | Aproximado (numérico)         |
| **Dimensão**   | 1D (ou poucas)    | Altas dimensões (10D+, 100D+) |
| **Custo**      | Baixo (analítico) | Alto (muitas amostras)        |
| **Erro**       | Zero              | Diminui com $1/\sqrt{N}$      |

---

## Por que Monte Carlo é útil?
- **Integrais multidimensionais**: Regra do trapézio cresce como $N^d$, Monte Carlo escala com $\sqrt{N}$ **independente** da dimensão.
- **Funções complexas**: sem primitiva ou com domínio irregular.
- **Física/Finanças**: simulações de partículas, opções financeiras, etc.

---

Quer ver o código Python para esse exemplo ou explorar como **reduzir a variância** (amostragem estratificada, importance sampling)? É só pedir! 🎲


Ver também: 
* [[LLM C2 numeric methods vs Monte Carlo methods]] (comparison between numerical methods of integration and monte carlo methods of integration)
* [chat source](https://chat.deepseek.com/a/chat/s/b6d1e17c-e5d6-400d-8738-d9763aaa1048)
