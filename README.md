//To Do Component en Angular HTML

<p>todo works!</p>
<section class="container-fluid">
    <div class="container">
        <h1>Liste de choses à faire</h1>

        <div *ngFor="let tache of listeTache, index as i">

            <div class=" row {{tache.categorie}}" *ngIf="!tache.check">
                <img class="col-2" src="https://image.flaticon.com/icons/svg/1057/1057077.svg" width="20px" (click)="validTache(i)">
                <div class="col-4">{{tache.titre}}</div>
                <div class="col-3">{{tache.date | date:"MM/dd/yy" | uppercase }}</div>
                <div class="col-3">{{tache.categorie}}</div> 
             </div>
                </div>

        <h1>Liste de choses effectuées</h1>
        <div *ngFor="let tache of listeTache, index as i">

                <div class="row {{tache.categorie}}" *ngIf="tache.check">
                    <img class="col-2" src="https://image.flaticon.com/icons/svg/1057/1057048.svg" width="20px" (click)="supprimerTache(i)">
                    <div class="col-4">{{tache.titre}}</div>
                    <div class="col-3">{{tache.date | date:"MM/dd/yy" | uppercase }}</div>
                    <div class="col-3">{{tache.categorie}}</div> 
                 </div>
                    </div>

        <h2 class="col-12" id="tache">Créer un nouveau truc</h2>

        <form #tacheForm="ngForm" (ngSubmit)="ajouterTache(tacheForm)"class="col-12">
            <input ngModel name ="titre" id="titre" required type="text"><br>
            <select ngModel name="categorie" id="categorie">
                <option *ngFor="let categorie of listeCategorie" [value]="categorie">{{categorie}}</option>
            </select>
            <button type="submit" class="bg-dark"> Ajoute un texte</button>

        </form>

<div class="alert alert-primary" role="alert">
    A simple primary alert-check it out!
</div>
    </div>
</section>


// To Do Component TS, Angular

import { Component, OnInit } from '@angular/core';
import {NgForm} from '@angular/forms';

@Component({
  selector: 'app-todo',
  templateUrl: './todo.component.html',
  styleUrls: ['./todo.component.css']
})

export class TodoComponent implements OnInit {



  constructor() { }

  listeTache = [];
  listeCategorie = ['PHP', 'CSS', 'HTML', 'JS', 'Divers'];

  ngOnInit() {
  }

  ajouterTache(tacheForm: NgForm){
    console.log(tacheForm.form.value.titre);

    //Construction d'un objet temporaire
    const monObjTemp = { titre: '', date: null, check: false, categorie: null };

    //Remplissage de mon objet temporaire avec les valeurs du formulaire
    monObjTemp.titre = tacheForm.form.value.titre;
    monObjTemp.date = new Date();
    monObjTemp.categorie = tacheForm.form.value.categorie;

    //On Pousse la variable de type objet 'monObjTemp' dans le tableau d'objet listeTache
    this.listeTache.push(monObjTemp);

    //Intialisation du formualire
    tacheForm.resetForm();

  }
     supprimerTache(index){
     this.listeTache.splice(index, 1);

    }
    validTache(index){
      this.listeTache[index].check = true;
     }
}


