# Load Guard & DevTools

A partir de la branche **step-6**, vous pouvez obtenir le style réalisé à la fin de celle-ci.

![styles](https://github.com/fausfore/ngrx-guide/blob/master/assets/images/styles.png)


### *[Début de la branche step-7]*

Actuellement, c'est **AllTodosComponent** qui déclenche le chargement des *todos*.
Avec un **Guard Angular**, le simple fait d'aller sur l'url */todo-list* nous permettra de vérifier si elle est chargée ( grâce à la propriété *loaded* ) et dans le cas contraire, il déclenchera l'action **LoadInitTodos**.

*Générer un Guard* :
```bash
ng g guard guards/is-todos-loaded/is-todos-loaded
```
Déclarer dans le **AppModule** :

```typescript
// [...]
import { IsTodosLoadedGuard } from './guards/is-todos-loaded/is-todos-loaded.guard';

@NgModule({
  declarations: [
    // [...]
  ],
  imports: [
    //[...]
  ],
  providers: [
    // [...]
    IsTodosLoadedGuard
  ],
  // [...]
```

*guards/is-todos-loaded/is-todos-loaded.guard*

```typescript
import { Observable } from 'rxjs/Observable';
import { Injectable } from '@angular/core';
import { ActivatedRouteSnapshot, CanActivate, RouterStateSnapshot, Router } from '@angular/router';
import { select, Store } from '@ngrx/store';
import { AppState } from '@StoreConfig';
import { map } from 'rxjs/operators';
import { selectTodosLoaded$ } from '@Selectors/todo-list.selector';
import { TodoListModule } from '@Actions/todo-list.action';

@Injectable()
export class IsTodosLoadedGuard implements CanActivate {
  constructor(
    private store: Store<AppState>,
    private router: Router
  ) {}
  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {

    return this.store
      .pipe(
        select(selectTodosLoaded$),
        map(isLoaded => {
          if (!isLoaded) {
            this.store.dispatch(new TodoListModule.LoadInitTodos());
          }
          return true;
        })
      );
  }
}
```
Ajouter le  *Guard* dans le fichier de *routing* :

 *app.routing.ts*  
```typescript
// [...]
import { IsTodosLoadedGuard } from './guards/is-todos-loaded/is-todos-loaded.guard';
// [...]
			{
		        path: 'todo-list',
		        loadChildren: './modules/todo-list/todo-list.module#TodoListModule',
		        canActivate: [IsTodosLoadedGuard]
		    },
// [...]
```
Supprimer le **LoadInitTodos** dans le *component* :

```typescript
[...]
	  /*
	  A supprimer
	  ngOnInit(){
		  this.store.dispatch(new TodoListModule.LoadInitTodos());
	  }
	  */
// [...]
```
De cette manière, la donnée sera chargée sans être dépendante du *component*.

## Redux Devtools

Il existe une extension de Chrome pour le développement avec Redux : [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=fr).
Pour l'installer sur le projet, il  faut le package [@ngrx/store-devtools](https://github.com/ngrx/platform/blob/master/docs/store-devtools/README.md).

Pour le définir dans le module principale : 
```typescript
// [...]
import { StoreDevtoolsModule } from '@ngrx/store-devtools';
import { environment } from 'environments/environment';


@NgModule({
  // [...]
  imports: [
	// [...]
    StoreDevtoolsModule.instrument({
      name: '[TODOLIST]',
      maxAge: 25, // Retains last 25 states
      logOnly: environment.production // Restrict extension to log-only mode
    })
  ],
  // [...]
})
export class AppModule { }
```
![redux devtools](https://d33wubrfki0l68.cloudfront.net/595e2922eee1bf85b801cdc86b8f7e135cc46ee0/0fd92/images/angular/store-devtools/store-devtools-screen.jpg)

**Redux DevTools** vous permettra de voir chaque changement de state, de conserver un historique et de faire un export de vos states (et inversement).

### [Suite >>](step-08.md)
