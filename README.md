# Angular FilePond

Angular FilePond is a handy adapter component for [FilePond](https://github.com/pqina/filepond), a JavaScript library that can upload anything you throw at it, optimizes images for faster uploads, and offers a great, accessible, silky smooth user experience.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/pqina/ngx-filepond/blob/master/LICENSE)
[![npm version](https://badge.fury.io/js/ngx-filepond.svg)](https://www.npmjs.com/package/ngx-filepond)
![npm](https://img.shields.io/npm/dt/ngx-filepond)
![npm peer dependency version](https://img.shields.io/npm/dependency-version/ngx-filepond/peer/@angular/core)

<img src="https://github.com/pqina/filepond-github-assets/blob/master/filepond-animation-01.gif?raw=true" width="370" alt=""/>

## Installation

Install FilePond component from npm.

```bash
npm install ngx-filepond filepond --save
```

Import `FilePondModule` and if needed register any plugins. Please note that plugins need to be [installed from npm](https://pqina.nl/filepond/docs/patterns/plugins/introduction/#installing-plugins) separately.

Add FilePond styles path `./node_modules/filepond/dist/filepond.min.css` to the `build.options.styles` property in `angular.json`

```ts
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

// import filepond module
import { FilePondModule, registerPlugin } from 'ngx-filepond';

// import and register filepond file type validation plugin
import FilePondPluginFileValidateType from 'filepond-plugin-file-validate-type';
registerPlugin(FilePondPluginFileValidateType);

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FilePondModule // add filepond module here
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

```html
<!-- app.component.html -->
<file-pond #myPond 
    [options]="pondOptions" 
    [files]="pondFiles"
    (oninit)="pondHandleInit()"
    (onaddfile)="pondHandleAddFile($event)">
</file-pond>
```

```ts
// app.component.ts
import { Component, ViewChild } from '@angular/core';
import { FilePondComponent } from './modules/filepond/filepond.component';
import { FilePondOptionProps } from 'filepond';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})

export class AppComponent {

  @ViewChild('myPond') myPond: FilePondComponent;

  pondOptions: FilePondOptionProps = {
    class: 'my-filepond',
    allowMultiple: true,
    labelIdle: 'Drop files here',
    acceptedFileTypes: 'image/jpeg, image/png'
  }

  pondFiles: FilePondOptionProps["files"] = [
    'index.html'
  ]

  pondHandleInit() {
    console.log('FilePond has initialised', this.myPond);
  }

  pondHandleAddFile(event: any) {
    console.log('A file was added', event);
  }
}
```

[Read the docs for more information](https://pqina.nl/filepond/docs/patterns/frameworks/angular/)
