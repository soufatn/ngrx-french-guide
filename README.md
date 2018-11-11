# Sommaire
*10/03/2018*

Ceci est un tutoriel pour débuter sur **NGRX**.
Vous verrez les différents concepts de cette librairie par le biais d'un exercice de création d'une **todo-list**, ainsi que l'optimisation de notre application par l'utilisation du pattern **Redux**.

>Actuellement **Ngrx** est en *version 5* ainsi que **Angular**.

### [0 - Introduction](step-00.md)
1.  #### Redux, kesako ?
2.  #### Pourquoi Redux alors ?
3.  #### Flux vs Redux
4.  #### Le Store, la base de tout
5.  ####  Le root reducer
6.  #### Le schéma
7.  #### Les actions
8.  ####  Action creator

### [1 - De Redux à NGRX](step-01.md)
1.  #### Installation
2.  #### Architecture Folder
3.  #### Commençons ! [ début du tutoriel ]

### [2 - Getters & create todo](step-02.md)
1.  #### Le Pipe et les opérateurs RXJS
2.  #### Les States Selectors
3.  #### Créer une todo

### [3 - Delete todo](step-03.md)
1.  #### Gérer les ids

### [4 - Un peu de refacto !](step-04.md)
1.  #### @Alias

### [5 - Select & Update Todo](step-05.md)

### [6 - Créer une API](step-06.md)
1.  #### Service Angular Get Todo
2.  #### Introduction de Effects

### [7 - Load Guard & DevTools](step-07.md)
1.  #### Redux Devtools

### [8 - Create Todo v2](step-08.md)

### [9 - Delete Todo v2](step-09.md)

### [10 - Update Todo v2](step-10.md)

### [11 - Les actions de type ERROR](step-11.md)
1.  #### Système de logs

### [12 - @Ngrx/Entity](step-12.md)

### [13 - Bonus Stage](step-13.md)
1.  #### Schematics
2.  #### Basics testing 
3.  #### Change Detection OnPush

### [14 - Advanced testing ](step-14.md)
1.  #### Mocks
2.  #### Actions
3.  #### Reducers
4.  #### Selectors
5.  #### Effects

## Conclusion 

J’espère que ce tutoriel vous aura permis de comprendre NGRX et son implémentation.
Il reste des points comme les **Meta-reducers** ou le **router-store** que vous pouvez retrouver sur le [gitHub officelle de NGRX](https://github.com/ngrx/platform).

Un autre utilitaire intéressant, le module [ngrx-actions](https://github.com/amcdnl/ngrx-actions).
Il vous permettra de réduire votre code *reduxien* avec des décorateurs.


*Auteur : **@Fausfore / Matias Ljubica***
