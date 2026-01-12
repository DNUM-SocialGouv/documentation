# 📊 Matomo – Documentation de tracking & plan de marquage

---

## Objectifs principaux du tracking
Ce document a pour objectif de fournir les connaissances de base pour la mise en place du tracking avec Matomo
 
- Comprendre le comportement des utilisateurs
- Mesurer la performance du site
- Aider à la prise de décision
- Améliorer l’expérience utilisateur
- Respecter les obligations légales (RGPD)
- _Optimiser les conversions_

---

## Architecture du tracking

### Outils
- Matomo Analytics
- JavaScript Tracker
- (Optionnel) Matomo Tag Manager

### Types de données collectées
- Données d'audience
- Données de navigation
- Données d'interaction
- Données de performance
- _Données de conversions (Goals)_

---

## Mise en place du tracking Matomo
Demander à l'administrateur la création d'un compte Matomo pour le produit. Il fournira : 
- Le tracking code
- l'URL du serveur Matomo (MATOMO_URL)
- l'identifiant du site de suivi dans Matomo (IDSITE)

### Ajout du tracking code 

À intégrer sur toutes les pages du site, juste après la balise `<body>` (ou dans la balise `<head>`)

```html
<!-- Matomo -->
<script type="text/javascript">
  var _paq = window._paq = window._paq || [];
  _paq.push(['trackPageView']);
  _paq.push(['enableLinkTracking']);
  (function() {
    var u="//{$MATOMO_URL}/";
    _paq.push(['setTrackerUrl', u+'matomo.php']);
    _paq.push(['setSiteId', {$IDSITE}]);
    var d=document, g=d.createElement('script'), s=d.getElementsByTagName('script')[0];
    g.type='text/javascript'; g.async=true; g.src=u+'matomo.js'; s.parentNode.insertBefore(g,s);
  })();
</script>
<!-- End Matomo Code -->
```

### Éléments trackés par défaut avec le code tracking Matomo 

| Catégorie                        | Tracké par défaut |
| -------------------------------- | ----------------- |
| Pages vues                       | ✅                 |
| Sessions                         | ✅                 |
| Sources de trafic                | ✅                 |
| Données techniques               | ✅                 |
| Localisation                     | ✅                 |
| Temps passé                      | ✅                 |
| Liens sortants / téléchargements | ✅*                |
| Événements personnalisés         | ❌                 |
| Conversions / objectifs          | ❌                 |
| Données personnelles             | ❌                 |
* si enableLinkTracking() est présent.

### Éléments NON trackés par défaut
Sans configuration spécifique, Matomo ne collecte pas :
- Événements personnalisés (clics sur boutons)
- Soumissions de formulaires
- Objectifs (conversions)
- E-commerce
- User ID
- Données personnelles nominatives (nom, email, etc.)
- Contenu des formulaires

## Plan de marquage (Measurement Plan)

### Conventions de nommage

| Élément | Règle |
|-------|------|
| Catégorie | Fonctionnelle (`cta`, `form`, `navigation`) |
| Action | Verbe (`click`, `submit`, `scroll`) |
| Label | Élément précis (`contact_form`) |
| Valeur | Numérique (optionnelle) |

---

### Exemple de plan de marquage global

| Page | Interaction | Catégorie | Action | Label |
|----|------------|----------|--------|-------|
| Accueil | Clic CTA | cta | click | hero_button |
| Contact | Submit formulaire | form | submit | contact_form |
| Blog | Scroll 75% | engagement | scroll | article |
| Global | Lien sortant | outbound | click | domain |
| Global | Téléchargement | download | click | file_name |
| Produit | Add to cart | ecommerce | add_to_cart | product_name |
| Checkout | Achat | ecommerce | purchase | order_id |

---

## Implémentation techniques

Cette section décrit les événements personnalisés suivis avec Matomo afin de mesurer les interactions clés des utilisateurs.

### Clic sur un bouton (CTA)

**Objectif**  
Mesurer les clics sur les boutons d’appel à l’action.

**Catégorie** : `cta`  
**Action** : `click`  
**Label** : `signup_button`

```html
<button id="signup-btn">S’inscrire</button>

<script>
document.getElementById('signup-btn').addEventListener('click', function () {
  _paq.push(['trackEvent', 'cta', 'click', 'signup_button']);
});
</script>
```
### Soumission de formulaire

**Objectif**  
Mesurer les soumissions de formulaire

```html
<form id="contact-form"></form>

<script>
document.getElementById('contact-form').addEventListener('submit', function () {
  _paq.push(['trackEvent', 'form', 'submit', 'contact_form']);
});
</script>
```