
Great question! These two terms come from very creative visual and historical metaphors, and they’re among the most entertaining examples of statistical terminology.

Let’s get right to their origins:

## 1. Bootstrap (or “bootstrapping”)

The origin is the English expression **“to pull yourself up by your bootstraps”**—that is, *to pull yourself up by the straps of your own boots*.

- This was used as a metaphor for **accomplishing an impossible or circular task**, since no one can pull themselves up by their own boots.
- In statistics, the **bootstrap** (developed by **Bradley Efron** in 1979) does exactly what seems “impossible”: **estimating the variability of a statistic using only the data itself**, without any external assumptions about the population distribution.
- Since you *resample* the data you already have (with replacement) to simulate new samples, you are essentially “pulling” new information from the original sample itself—hence the name.
- Efron chose this name precisely because of its almost magical aspect

## 2. Jackknife

The origin here is more practical and comes from the **Swiss Army knife** or **pocket knife** (in English, *jackknife*).

- The metaphor comes from the idea that a pocket knife is a **simple, versatile, and useful tool for many everyday tasks**—you can use it to cut, open, scrape, etc.
- The **jackknife** method (proposed by **Maurice Quenouille** in 1949 and developed by **John Tukey** in the 1950s) is a resampling technique that involves **calculating the statistic of interest repeatedly, omitting one observation at a time**.
- It is a simpler and computationally lighter method than the bootstrap, but it also serves to reduce bias and estimate standard errors.
- Tukey liked to give suggestive and informal names, and chose *jackknife* to emphasize that it was a **practical, robust, and general-purpose tool**, like a pocket knife that every researcher should have on hand.
  

---

  

  

  

  

_Translated with [DeepL.com](https://www.deepl.com/?utm_campaign=product&utm_source=web_translator&utm_medium=web&utm_content=copy_free_translation) (free version)_