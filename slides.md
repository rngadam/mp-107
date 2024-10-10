---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://photos.fife.usercontent.google.com/pw/AP1GczOMK8tph5hFbSTOi14XOA6VIoueXuCD6OKqXNu4QWNxLs_rtec02qA94g=w1771-h1328-s-no-gm?authuser=0
# some information about your slides (markdown enabled)
title: Introduction à l'identité numérique décentralisée
info: |
## Presentation
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# take snapshot for each slide in the overview
overviewSnapshots: true
---
# Introduction à l'identité numérique décentralisée
---

# Agenda

<Toc v-click minDepth="1" maxDepth="2"></Toc>

---

# Introduction à l'identité numérique décentralisée

L’identité numérique décentralisée (DID; Decentralized Identifiers) est une approche innovante qui permet aux individus de contrôler directement leur propre identité numérique. Contrairement aux systèmes centralisés traditionnels, où les informations d’identité sont gérées par des entités tierces, l’identité décentralisée repose sur des technologies comme la blockchain pour offrir une gestion plus sécurisée et privée des données personnelles.

Dans cette présentation de 20 minutes, les concepts de base de l'identité décentralisée seront introduits ainsi que leurs applications autour de l'agent Python Aries de Hyperledger (transféré à l'OpenWallet Foundation)

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# Qu'est-ce que l'identité numérique décentralisée?

Les caractéristiques de l'identité numérique décentralisée:

- 🛡️**Contrôle utilisateur** - Les utilisateurs gèrent eux-mêmes leurs identifiants et informations personnelles, stockées dans un portefeuille numérique sécurisé
- 🔒 **Confidentialité et Sécurité** -  Les données ne sont pas stockées sur un serveur centralisé mais sur un portefeuille numérique local
- 🔄 **Interopérabilité** - Utilisation de normes ouvertes pour assurer que les identifiants peuvent être vérifiés et utilisés à travers différentes plateformes et services
- ✅ **Émission et Vérification** - Les identifiants sont émis par des entités de confiance (comme des gouvernements ou des institutions éducatives) et peuvent être vérifiés par n’importe quel service nécessitant une authentification
- 🌐 **Portabilité** - Les utilisateurs peuvent transporter et utiliser leurs identifiants numériques partout où ils en ont besoin, sans dépendre d’une seule entité
<br>
<br>

Lire plus [Decentralized Identity Foundation](https://identity.foundation/)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->
---
---
# Preuve à divulgation nulle de connaissance

> Une preuve à divulgation nulle de connaissance (Zero Knowledge Interactive proof ou ZKIP en anglais) est un protocole cryptographique permettant l'authentification sécurisée d'informations. Dans le cadre de ce protocole, une entité, nommée « fournisseur de preuve », prouve mathématiquement à une autre entité, le « vérificateur », qu'une proposition est vraie sans révéler d'autres informations que la véracité de la proposition.
---
---

# Lois des exposants

​​Produit de puissances de même base: $x^{a}*x^{b}=x^{a+b}$

​Puissance d'une puissance: $(x^a)^b = x^{a*b}$

```python
>>> (x, a, b) = (10, 2, 3)
>>> x**a * x**b == x**(a+b)
True
>>> (x**a)**b == x**(a*b)
True
```

---

# Modulo (opération)

En informatique, l'opération modulo est une opération binaire qui associe, à deux entiers naturels, le reste de la division euclidienne du premier par le second.

```python
>>> 9 % 3
0
>>> 9 % 4
1
```
---

# Fonction non-réversible

cette fonction est non-réversible:

$f(x) = g^{x} \mod p$

ce qui signifie que même si on connait g et p et f(x), il est difficile de retrouver x

en Python:

```python
>>> (g, p) = (101, 11)
>>> f = lambda x: g ** x % p
>>> [f(x) for x in range(0,100)]
[1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6, 1, 2, 4, 8, 5, 10, 9, 7, 3, 6]
>>> (x, r) = (13, 42)
>>> e = 42
>>> fx = f(x)
>>> fr = f(r)
>>> fv = f(r+(x*e))
>>> fv == fx*fr**e%p
True
```

---
dragPos:
  square: 641,6,167,_,-16
---

# Diagramme de séquence

```mermaid {scale: 0.9, alt: 'A simple sequence diagram'}
sequenceDiagram
  VDR->Alice: (g,p)
  VDR->John: (g,p)
  Alice->John: fx, fr
  John->Alice: e
  Alice->John: fv = f(r+(x*e))
  John->John: is fv == fx*fr**e%p?
```

---
---
# acapy (aka hyperledger/aries-cloudagent-python)

migré de hyperledger/aries-cloudagent-python à openwallet-foundation/acapy

<img src="https://openwallet.foundation/wp-content/uploads/sites/11/2023/10/OpenWallet_Foundation_Logo_White.svg">

---
---
# déploiement

<Transform :scale="0.8">
<img src="https://github.com/openwallet-foundation/acapy/blob/main/docs/assets/deploymentModel-full.png?raw=true" height="100%">
</Transform>
---
---
# Pour en apprendre plus

* https://www.quebec.ca/gouvernement/identite-numerique/programme-service-quebecois-identite-numerique
* https://github.com/rngadam/zkp-exemple
* https://github.com/hyperledger/indy-node
* https://github.com/bcgov/von-network
* https://github.com/hyperledger/anoncreds-rs
* https://aca-py.org/latest/
* https://github.com/openwallet-foundation/acapy
* https://github.com/openwallet-foundation/credo-ts
* https://github.com/openwallet-foundation/bifold-wallet/

<PoweredBySlidev mt-10 />
