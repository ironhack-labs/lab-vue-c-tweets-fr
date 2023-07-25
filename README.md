![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | Tweets de Vue.js (Composition API)

## Introduction

La transmission de données via les *props* est un concept important de Vue.js qui est mieux compris grâce à la pratique. Nous allons utiliser cet exercice pour vous aider à consolider votre compréhension des props.

Nous allons cloner une interface utilisateur existante d'une application populaire, Twitter. Commençons !

<p align="center">
  <img src="https://education-team-2020.s3.eu-west-1.amazonaws.com/web-frontend-vue/lab-vue-tweets-4.png" width="500">
</p>

## Configuration

- Fork ce repo
- Clonez ce repo
- Ouvrez le LAB et commencez :

  ```bash
  $ cd lab-vue-c-tweets
  $ npm install
  $ npm run dev
  ```

## Remise

- Une fois terminé, exécutez les commandes suivantes :abc: 

  ```bash
  git add .
  git commit -m "done"
  git push origin main
  ```

- Créez une pull request (demande d'extraction) afin que vos TAs puissent vérifier votre travail.

## Pour commencer
   

1. Nous allons utiliser [Font Awesome](https://fontawesome.com/v5.15/icons?d=gallery&p=1) pour les icônes de notre application. Ajoutez la feuille de style suivante dans la balise `head` de la page `index.html` :
  
   ```html
       <link
         rel="stylesheet"
         href="https://pro.fontawesome.com/releases/v5.10.0/css/all.css"
         integrity="sha384-AYmEC3Yw5cVb3ZcuHtOA93w35dYTsvhLPVnYs9eStHfGJvOvKxVfELGroGkvsg+p"
         crossorigin="anonymous"
       />
   ```

## Instructions

### Itération 1 | Contenu initial

Pour vous permettre de vous concentrer sur Vue.js sans vous soucier de la mise en forme, nous vous avons fourni les styles CSS. Tout le CSS est inclus dans le code de départ dans le fichier `src/App.vue`, à l'intérieur de la balise `<style>`. 

Nous vous avons également fourni le contenu initial du fichier `App.vue` et nous avons inclus la structure HTML pour le composant `Tweet.vue`. Avant de commencer à travailler, prenez un moment pour examiner ces deux fichiers.

Une fois que vous exécutez initialement l'application, vous devriez voir ce qui suit :

![Tweet component after the initial setup](https://education-team-2020.s3.eu-west-1.amazonaws.com/web-frontend-vue/lab-vue-tweets-1.png)

Le composant `Tweet` affiche actuellement du contenu statique. Nous allons changer cela dans la prochaine itération. Nous allons mettre à jour le composant `Tweet` pour afficher le contenu provenant des `props`.


### Itération 2 | Passer le tweet en tant que prop

Dans `App.vue`, nous avons un tableau nommé `tweets` qui contient des objets représentant des tweets. Nous utiliserons le composant `Tweet` pour afficher ces objets tweet. Dans le composant `Tweet`, nous afficherons le `nom` de l'utilisateur, son `image`, son `handle`, la `timestamp` du tweet et le `message`. 

**Passez le tweet en tant que prop**

Passez le premier objet de données du tableau `tweets`  en tant que prop dans le composant `Tweet` :

```vue
<!-- src/App.vue -->
<!-- ... -->

<Tweet :tweet="tweets[0]" />
```

**Affichez le contenu du tweet dans le composant `Tweet`**

Mettez à jour le composant `Tweet` pour afficher les valeurs provenant de la prop `tweet`. N'oubliez pas que la valeur que nous avons passée est un objet !

**Résultat attendu**

Une fois terminé, votre composant `Tweet` devrait afficher le contenu suivant :

![Tweet component after passing the "tweets" prop](https://education-team-2020.s3.eu-west-1.amazonaws.com/web-frontend-vue/lab-vue-tweets-2.png)


### Itération 3 | Créer les composants

Nous allons maintenant créer de nouveaux fichiers pour les composants que nous allons créer lors des itérations suivantes. À l'intérieur du dossier  `src/components/`, créez les nouveaux fichiers suivants :

- `src/components/ProfileImage.vue` ,
- `src/components/User.vue` ,
- `src/components/Timestamp.vue` ,
- `src/components/Message.vue`  et
- `src/components/Actions.vue`.


Lors des prochaines itérations, vous devrez refactoriser le composant `Tweet`. Vous devrez extraire des parties de la structure HTML existante vers de nouveaux composants :

![Example - Refactoring the "Tweet" component](https://education-team-2020.s3.eu-west-1.amazonaws.com/web-frontend-vue/lab-vue-tweets-3.png)
<br>

**Une fois que vous avez terminé toutes les itérations**, la version finale de votre composant `Tweet` ressemblera à ceci :

<details>
<summary>Cliquez pour voir le code</summary>

```vue
<!-- FINAL VERSION -->

<template>
  <div class="tweet">
    <ProfileImage image="user.image" />

    <div class="body">
      <div class="top">
        <User userData="user" />
        <Timestamp time="timestamp" />
      </div>

      <Message message="message" />
      <Actions />
    </div>

    <i class="fas fa-ellipsis-h"></i>
  </div>
</template>

<script>
  const props = defineProps({
    user: Object,
    timestamp: String,
    message: String
  });
</script>
```

:heavy_exclamation_mark: Ne copiez pas directement le code ci-dessus dans le composant `Tweet`!

Vous le ferez dans les prochaines itérations, étape par étape. Vous remplacerez les parties du HTML à mesure que vous créerez chaque nouveau composant.

<hr>
<br>
</details>

### Itération 4 | Composant ProfileImage

**Extraction du HTML**

Extrayez la balise `img` txistante et affichez-la à l'aide du composant `ProfileImage` :

```jsx
<img src="IMAGE_URL" class="profile" alt="profile"/>
```

**Rendu du composant**

Une fois terminé, importez le composant `ProfileImage` dans `Tweet.js`.  Après l'avoir importé, affichez le composant à l'intérieur de `Tweet` de la manière suivante :

```vue
<!-- ... -->
<template>
  <div class="tweet">
    <ProfileImage image="user.image" />
<!-- ... -->
```

**Accéder aux props**

`ProfileImage` reçoit une prop `image`. Définissez cette valeur en tant que `src` de la balise `<img />`.


### Itération 5 | Composant User

**Extraction du HTML**

Extrayez les balises `span` existantes affichant les informations de l'utilisateur et affichez-les à l'aide du composant `User` :

```vue
<span class="user">
  <span class="name"> USER_NAME </span>
  <span class="handle">@ USER_HANDLE</span>
</span>
```

**Rendu du composant**

Importez le composant `User` dans `Tweet.js`.  Après l'avoir importé, affichez le composant à l'intérieur de `Tweet` de la manière suivante :

```vue
<!-- ... -->

<template>
  <div class="tweet">
    <ProfileImage image="user.image" />

    <div class="body">
      <div class="top">
        <User userData="user" />

<!-- ... -->
```

**Accéder aux props**

WNous avons passé l'objet avec les informations de l'utilisateur via la prop `userData`. Accédez et affichez le nom de l'utilisateur et le handle Twitter.



### Itération 6 | Composant Timestamp

**Extraction du HTML**

Extrayez la balise `span` existante affichant les informations de l'horodatage et affichez-la à l'aide du composant `Timestamp` :

```jsx
<span class="timestamp"> TWEET_TIMESTAMP </span>
```

**Rendu du composant**

Importez le composant `Timestamp` dans `Tweet.js`.  Après l'avoir importé, affichez le composant à l'intérieur de `Tweet` de la manière suivante :

```vue
<!-- ... -->

<template>
  <div class="tweet">
    <ProfileImage image="user.image" />

    <div class="body">
      <div class="top">
        <User userData="user" />
        <Timestamp time="timestamp" />

<!-- ... -->
```


**Accéder aux props**

`Timestamp` reçoit une prop `time`. Affichez cette valeur en tant que contenu de la balise `span`.


### Itération 7 | Composant Message

**Extraction du HTML**

Extrayez la balise `p` existante et affichez-la à l'aide du composant `Message` :

```jsx
<p class="message"> TWEET_MESSAGE </p>
```

**Rendu du composant**

Une fois terminé, importez le composant `Message` et affichez-le dans `Tweet.js` de la manière suivante :

```vue
<!-- ... -->

<template>
  <div class="tweet">
    <ProfileImage image="user.image" />

    <div class="body">
      <div class="top">
        <User userData="user" />
        <Timestamp time="timestamp" />
      </div>

      <Message message="message" />
<!-- ... -->
```

**Accéder aux props**

`Message` reçoit une prop `message`. Affichez cette valeur dans la balise `p`.


### Itération 8 | Composant Actions

**Extraction du HTML**

Extrayez la balise `div.actions` existante et affichez-la à l'aide du composant `Actions` :

```jsx
    <div class="actions">
      <i class="far fa-comment"></i>
      <i class="fas fa-retweet"></i>
      <i class="far fa-heart"></i>
      <i class="fas fa-share"></i>
    </div>
```

**Rendu du composant**

Une fois terminé, importez le composant `Actions` et affichez-le dans `Tweet.js` de la manière suivante :

```vue
<!-- ... -->

<template>
  <div class="tweet">
    <ProfileImage image="user.image" />

    <div class="body">
      <div class="top">
        <User userData="user" />
        <Timestamp time="timestamp" />
      </div>

      <Message message="message" />
      <Actions />

<!-- ... -->
```
Félicitations, vous avez maintenant créé tous les composants nécessaires pour le composant `Tweet` !

`Actions` ne nécessite aucune prop.


### Itération 9 | Afficher plusieurs Tweets

Une fois que vous avez terminé de refactoriser le composant `Tweet`, mettez à jour `App.vue` pour afficher trois composants `<Tweet />`. Chaque `<Tweet />` devrait recevoir un objet tweet distinct à partir du tableau `tweetsArray`. 

Une fois terminé, votre application devrait afficher le contenu suivant :

<details>

<summary>Cliquez pour voir l'image</summary>

![Example - Final Result](https://education-team-2020.s3.eu-west-1.amazonaws.com/web-frontend-vue/lab-vue-tweets-4.png)


</details>

<hr>

Bon codage ! :blue_heart: