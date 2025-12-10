# Clean Code (TypeScript)

## 🏗️ Règles de design

### Garder les constantes configurables accessibles

Les constantes doivent être faciles à modifier et centralisées.

```python
# ❌ Mauvais
if age > 18: ...

# ✅ Bon
AGE_MINIMUM = 18
if age > AGE_MINIMUM: ...
```

### Préférer la composition aux if/else interminables

Utiliser des objets de configuration et des fonctions spécialisées pour éviter les chaînes de conditions.

```typescript
// ❌ Mauvais
function calculateAllocationAmount(recipient: Recipient): number {
  if (recipient.category === "handicap") {
    return recipient.baseAmount * 1.5;
  } else if (recipient.category === "senior") {
    return recipient.baseAmount * 1.3;
  } else if (recipient.category === "unemployed") {
    return recipient.baseAmount * 1.0;
  }
  return 0;
}

// ✅ Bon - Approche fonctionnelle
const ALLOCATION_MULTIPLIERS: Record<RecipientCategory, number> = {
  handicap: 1.5,
  senior: 1.3,
  unemployed: 1.0,
};

function calculateAllocationAmount(recipient: Recipient): number {
  const multiplier = ALLOCATION_MULTIPLIERS[recipient.category];
  return recipient.baseAmount * multiplier;
}
```

### Éviter la sur-configuration

Ne pas préparer des options qui ne servent pas encore. Appliquer le principe YAGNI (You Aren't Gonna Need It).

### Séparation des responsabilités

En Node.js, utiliser le système de modules pour séparer les responsabilités plutôt que l'injection de dépendances complexe.

```typescript
// ❌ Mauvais - Tout dans un seul fichier
app.post("/users", async (req, res) => {
  // Logique métier mélangée avec la route
  if (!req.body.email?.includes("@")) {
    return res.status(400).json({ error: "Email invalide" });
  }
  await database.users.insert(req.body);
  await emailService.send(req.body.email, "Bienvenue");
  res.json({ success: true });
});

// ✅ Bon - Séparation claire des responsabilités
// routes/users.ts
router.post("/users", userController.createUser);

// controllers/userController.ts
export const userController = {
  createUser: async (req, res) => {
    try {
      const userData = validateUser(req.body); // validation des inputs du controller
      const user = await userService.createUser(userData);
      res.json(user);
    } catch (error) {
      res.status(400).json({ error: error.message });
    }
  },
};

// services/userService.ts
export const userService = {
  createUser: async (userData) => {
    // regles métier
    const user = await userRepository.save(userData); // ou ORM
    await emailService.sendWelcome(user.email);
    return user;
  },
};
```

### Loi de Déméter

Une fonction ne devrait connaître que ses dépendances directes, pas les dépendances de ses dépendances.

```typescript
// ❌ Mauvais - Chaîne d'appels profonde
const countryCode = user.getAddress().getCountry().getCode();

// ✅ Bon - Fonction dédiée
const countryCode = user.getCountryCode();

// Alternative fonctionnelle
const getUserCountryCode = (user: User): string => {
  return user.address.country.code;
};
```

## 👓 Astuces pour la compréhensibilité

### Etre cohérent

Un style unique pour tout le projet. Utiliser des outils de formatage automatique.

### Noms explicites

Les noms doivent révéler l'intention.

```javascript
// ❌ Mauvais
let d = 5;

// ✅ Bon
let joursAvantExpiration = 5;
```

### Encapsuler les conditions limites

Mieux vaut un endroit centralisé pour gérer les cas particuliers.

```typescript
// ❌ Mauvais - Conditions éparpillées
function validateApplication(application: Application): boolean {
  if (application.birthDate) {
    const age = calculateAge(application.birthDate);
    if (age < 18 || age > 65) {
      return false;
    }
  }
  if (application.income && application.income > 2000) {
    return false;
  }
  if (application.address && !application.address.includes("@")) {
    return false;
  }
  return true;
}

// ✅ Bon - Conditions centralisées
function validateApplication(application: Application): boolean {
  return (
    isEligibleAge(application) &&
    isEligibleIncome(application) &&
    hasValidEmail(application)
  );
}

function isEligibleAge(application: Application): boolean {
  if (!application.birthDate) return true;
  const age = calculateAge(application.birthDate);
  return age >= 18 && age <= 65;
}

function isEligibleIncome(application: Application): boolean {
  return !application.income || application.income <= 2000;
}

function hasValidEmail(application: Application): boolean {
  return !application.address || application.address.includes("@");
}
```

### Préférer des value objects

Plutôt que de manipuler des types primitifs partout.

```typescript
// ❌ Mauvais - Types primitifs
const amount = 500;
const period = "monthly";

// ✅ Bon - Value objects fonctionnels
type Period = "monthly" | "quarterly" | "yearly";

interface AllocationAmount {
  amount: number;
  period: Period;
}

const createAllocationAmount = (
  amount: number,
  period: Period
): AllocationAmount => ({
  amount,
  period,
});

const addAllocationAmounts = (
  amount1: AllocationAmount,
  amount2: AllocationAmount
): AllocationAmount => {
  if (amount1.period !== amount2.period) {
    throw new Error("Périodes différentes");
  }
  return createAllocationAmount(
    amount1.amount + amount2.amount,
    amount1.period
  );
};

const formatAllocationAmount = (allocation: AllocationAmount): string => {
  return `${allocation.amount}€/${allocation.period}`;
};

// Utilisation
const baseAmount = createAllocationAmount(500, "monthly");
const supplement = createAllocationAmount(100, "monthly");
const total = addAllocationAmounts(baseAmount, supplement);
```

### Éviter les dépendances logiques

Une méthode qui dépend trop d'une autre est un piège. Réduire le couplage.

### Éviter les conditions négatives

Préférer les conditions positives pour améliorer la lisibilité.

```typescript
// ❌ Mauvais
if (!isValid) {
  // ...
}

// ✅ Bon
if (isInvalid) {
  // ...
}
```

## 📝 Règles de nommage

### Noms descriptifs et sans ambiguïté

Le nom doit révéler l'intention sans nécessiter de commentaire.

```typescript
// ❌ Mauvais
let d: number, t: number, u: User;

// ✅ Bon
let daysSinceCreation: number, totalAmount: number, user: User;
```

### Prononçables et recherchables

Préférer `nombreUtilisateurs` à `nbUsr` pour faciliter la recherche et la communication.

### Pas de "magic numbers"

Les remplacer par des constantes avec des noms explicites.

```typescript
// ❌ Mauvais
if (user.age >= 18) { ... }

// ✅ Bon
const AGE_MAJORITE: number = 18;
if (user.age >= AGE_MAJORITE) { ... }
```

### Pas de préfixes inutiles

Éviter les préfixes comme `strName`, `intAge` qui n'apportent pas de valeur.

```typescript
// ❌ Mauvais
let strUserName: string, intUserAge: number;

// ✅ Bon
let userName: string, userAge: number;
```

## ⚙️ Règles relatives aux fonctions

### Courtes et concentrées

Une seule responsabilité par fonction.

```typescript
interface User {
  email: string;
  name: string;
}

// ❌ Mauvais
function processUser(user: User): void {
  // Validation
  if (!user.email || !user.email.includes("@")) {
    throw new Error("Email invalide");
  }

  // Sauvegarde
  database.save(user);

  // Envoi d'email
  emailService.send(user.email, "Bienvenue");

  // Log
  console.log("Utilisateur traité");
}

// ✅ Bon
function validateUser(user: User): void {
  if (!user.email || !user.email.includes("@")) {
    throw new Error("Email invalide");
  }
}

function saveUser(user: User): Promise<void> {
  return database.save(user);
}

function sendWelcomeEmail(user: User): Promise<void> {
  return emailService.send(user.email, "Bienvenue");
}
```

### Nom descriptif qui dit ce que ça fait

Le nom de la fonction doit être un verbe qui décrit l'action.

```typescript
// ❌ Mauvais
function data(): unknown { ... }
function process(): unknown { ... }

// ✅ Bon
function calculateTotalAllocations(recipients: Recipient[]): number { ... }
function validateEmail(email: string): boolean { ... }
```

### Peu d'arguments (idéalement ≤ 3)

Plus il y a d'arguments, plus la fonction est difficile à utiliser et tester.

```typescript
interface UserProfile {
  age: number;
  address: string;
  phone: string;
  role: string;
  department: string;
}

interface UserData {
  name: string;
  email: string;
  profile: UserProfile;
}

// ❌ Mauvais
function createUser(
  name: string,
  email: string,
  age: number,
  address: string,
  phone: string,
  role: string,
  department: string
): User { ... }

// ✅ Bon
function createUser(userData: UserData): User { ... }
// ou
function createUser(name: string, email: string, userProfile: UserProfile): User { ... }
```

### Pas d'effet de bord caché

La fonction ne doit pas modifier des variables globales ou des paramètres d'entrée.

### Pas de flags

Préférer deux fonctions claires plutôt qu'une fonction avec un booléen.

```typescript
// ❌ Mauvais
function process(user: User, isAdmin: boolean): void { ... }

// ✅ Bon
function processAsAdmin(user: User): void { ... }
function processAsUser(user: User): void { ... }
```

## 💬 Règles relatives aux commentaires

### Éviter le bruit

Ne pas commenter l'évidence.

```typescript
// ❌ Mauvais
i++; // incrémente i

// ✅ Bon
i++; // Préparer l'index pour la prochaine itération
```

### Expliquer l'intention, pas l'évidence

Les commentaires doivent expliquer le "pourquoi", pas le "quoi".

```typescript
// ❌ Mauvais
// Vérifier si l'utilisateur est connecté
if (user.isConnected) { ... }

// ✅ Bon
// Vérifier la connexion pour éviter les accès non autorisés
if (user.isConnected) { ... }
```

### Ne pas commenter du code mort

Le supprimer directement.

### Avertir des conséquences

Si une partie du code est délicate, expliquer pourquoi et quelles sont les implications.

```typescript
// ⚠️ ATTENTION: Cette fonction modifie l'état global
// Ne pas appeler dans un contexte multi-threadé
function updateGlobalState(): void { ... }
```

## 📐 Structure du code source

### Regrouper verticalement ce qui est lié

Les concepts liés doivent être proches dans le code.

### Déclarer les variables près de leur usage

Réduire la portée des variables au minimum nécessaire.

```typescript
// ❌ Mauvais
let user: User;
let email: string;
let isValid: boolean;

// ... 50 lignes plus tard ...
user = getUser();
email = user.email;
isValid = validateEmail(email);

// ✅ Bon
const user: User = getUser();
const email: string = user.email;
const isValid: boolean = validateEmail(email);
```

### Garder les lignes courtes

Maximum 120 caractères par ligne pour une meilleure lisibilité.

### Indentation propre

Pas d'alignement artificiel qui casse à la moindre modification.

## 🧩 Objets et structures de données

### Cacher les détails internes (encapsulation)

Exposer seulement ce qui est nécessaire pour l'utilisation du module.

```typescript
// ❌ Mauvais - Détails internes exposés
const hashPassword = (password) => bcrypt.hash(password, 10);
const generateToken = (user) => jwt.sign(...);

export const userService = {
  hashPassword, // Fonction interne exposée
  generateToken, // Fonction interne exposée
  createUser: async (userData) => {
    const hashedPassword = await hashPassword(userData.password);
    return database.users.create({ ...userData, password: hashedPassword });
  },
};

// ✅ Bon - Interface claire et encapsulée
export const userService = {
  createUser: async (userData) => {
    const hashedPassword = await hashPassword(userData.password);
    return database.users.create({ ...userData, password: hashedPassword });
  },
  authenticateUser: async (email, password) => {
    ...
  },
};
```

### Une fonction = une responsabilité

Chaque fonction doit avoir une seule raison de changer.

### Peu de paramètres

Si une fonction a trop de paramètres, elle fait probablement trop de choses.

### Pas de dépendances circulaires

Éviter les dépendances circulaires entre modules.

### Préférer plusieurs petites fonctions

Plutôt qu'une énorme fonction avec plein de paramètres.

## ✅ Tests

#### Un bon test est :

* **Simple** : un concept par test
* **Rapide** : s'exécute rapidement
* **Indépendant** : ne dépend pas d'autres tests
* **Lisible** : facile à comprendre
* **Répétable** : donne le même résultat à chaque exécution
* **Automatisé et auto-validant** : se valide lui-même

```typescript
// ❌ Mauvais
test("user test", (): void => {
  const user: User = createUser("John", "john@example.com");
  expect(user.name).toBe("John");
  expect(user.email).toBe("john@example.com");
  expect(user.isActive).toBe(true);
  expect(user.createdAt).toBeDefined();
  // ... trop de choses testées en même temps
});

// ✅ Bon
test("should create user with valid data", (): void => {
  const user: User = createUser("John", "john@example.com");
  expect(user.name).toBe("John");
});

test("should set user as active by default", (): void => {
  const user: User = createUser("John", "john@example.com");
  expect(user.isActive).toBe(true);
});
```

### Utiliser un outil de couverture

Vérifier ce qui est testé (et ce qui ne l'est pas) avec des outils comme Istanbul, Jest, ou SonarQube.

## 🚨 Indices d'un code "pas clean" (Code Smells)

### Rigidité

Difficile à faire évoluer. Chaque changement nécessite de modifier de nombreux endroits.

### Fragilité

Un petit changement casse autre chose. Le code est instable.

### Immobilité

Difficile à réutiliser ailleurs. Le code est trop couplé à son contexte.

### Complexité inutile

Code plus complexe que nécessaire pour résoudre le problème.

### Duplication

Même logique répétée à plusieurs endroits.

### Opacité

Difficile à comprendre. Le code ne révèle pas son intention.

## ⚠️ Gestion des erreurs

### Séparer logique métier et gestion des erreurs

Ne pas mélanger pas la logique principale avec la gestion des erreurs.

```typescript
interface Recipient {
  name: string;
  allocationAmount?: number;
}

// ❌ Mauvais
function calculateTotalAllocations(recipients: Recipient[]): number {
  if (!recipients || recipients.length === 0) {
    console.log("Erreur: pas de bénéficiaires");
    return 0;
  }

  let total: number = 0;
  for (let recipient of recipients) {
    if (!recipient.allocationAmount) {
      console.log("Erreur: montant manquant");
      continue;
    }
    total += recipient.allocationAmount;
  }
  return total;
}

// ✅ Bon
function calculateTotalAllocations(recipients: Recipient[]): number {
  if (!recipients || recipients.length === 0) {
    throw new Error("Aucun bénéficiaire fourni");
  }

  return recipients.reduce((total: number, recipient: Recipient): number => {
    if (!recipient.allocationAmount) {
      throw new Error(
        `Montant manquant pour le bénéficiaire: ${recipient.name}`
      );
    }
    return total + recipient.allocationAmount;
  }, 0);
}
```

### Utilisrz des exceptions, pas des codes d'erreurs

Les exceptions sont plus expressives et plus faciles à gérer.

### Éviter null pour les valeurs métier

Utiliser des valeurs explicites plutôt que `null` pour représenter des concepts métier.

```typescript
// ❌ Mauvais - null comme valeur métier
interface UserProfile {
  role: string | null; // null = pas de rôle
}

function buildACLValue(role: string): ACLValue {
  // 💥 Erreur si role est null
  return aclConfig[role];
}

// ✅ Bon - Valeur explicite pour l'absence
interface UserProfile {
  role: string; // Toujours une valeur valide
}

enum Role {
  ADMIN = "admin",
  READONLY = "readonly",
  NO_ROLE = "norole", // Valeur explicite
}

function buildACLValue(role: string): ACLValue {
  if (role === Role.NO_ROLE) {
    return getDefaultACL();
  }
  return aclConfig[role];
}
```

### Ajouter du contexte aux exceptions

Les messages d'erreur doivent être informatifs.

```javascript
// ❌ Mauvais
throw new Error("Erreur");

// ✅ Bon
throw new Error(
  `Impossible de sauvegarder l'utilisateur ${userId}: ${error.message}`
);
```

## 🌍 Règles générales

### KISS (Keep It Simple, Stupid)

Le plus simple est presque toujours le meilleur choix.

```typescript
// ❌ Trop complexe
if (isConnected === true && hasPermission === true) {
  start();
}

// ✅ Plus simple
if (isConnected && hasPermission) {
  start();
}
```

### Règle du boy-scout

Laisser le code un peu plus propre que nous l'avons trouvé. Chaque modification doit améliorer la qualité globale.

### Chercher la cause racine

Corriger le symptôme crée souvent de nouveaux bugs. Analyser le problème en profondeur.

### Principe de moindre surprise

Le code doit se comporter comme prévu, sans piège. Les noms de variables et fonctions doivent être explicites.

### DRY (Don't Repeat Yourself)

Éviter la duplication, mais attention à ne pas centraliser prématurément du code inutile. Trouver le bon équilibre entre réutilisabilité et simplicité.

## 🎯 Conclusion

Le clean code n'est pas une checklist à appliquer aveuglément. C'est une manière de coder en gardant en tête la **lisibilité**, la **simplicité** et la **maintenabilité**.

Un bon indicateur : si nous pouvons relire le code dans 6 mois et le comprendre immédiatement, nous somme sur la bonne voie.
