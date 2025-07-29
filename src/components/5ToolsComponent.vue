<script setup>
import html5 from '@/assets/images/html5.png';
import css from '@/assets/images/css.svg';
import bootstrap from '@/assets/images/bootstrap.png';
import js from '@/assets/images/javascript.svg';

import mongodb from '@/assets/images/mongodb.svg';
import express from '@/assets/images/expressjs.svg';
import react from '@/assets/images/react.svg';
import node from '@/assets/images/node.svg';

import heroku from '@/assets/images/heroku.svg';
import git from '@/assets/images/git.svg';
import postman from '@/assets/images/postman.svg';
import vscode from '@/assets/images/vscode.png';
</script>

<template>
  <section id="tools" class="py-5 bg-dark text-white text-center">
    <div class="container my-3">
      <h2 class="display-4 fw-bold mb-5">Tools</h2>
      <div class="row justify-content-center g-4">
        <div class="col-12 col-md-4">
          <h3 class="mb-4 text-primary">Front End</h3>
          <div class="tool-icons row justify-content-center align-items-center g-4">
            <div class="col-6"><img :src="html5" alt="HTML5" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="css" alt="CSS3" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="bootstrap" alt="Bootstrap" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="js" alt="JavaScript" class="tool-icon img-fluid"></div>
          </div>
        </div>

        <div class="col-12 col-md-4">
          <h3 class="mb-4 text-success">MERN</h3>
          <div class="tool-icons row justify-content-center align-items-center g-4">
            <div class="col-6"><img :src="mongodb" alt="MongoDB" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="express" alt="Express.js" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="react" alt="React" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="node" alt="Node.js" class="tool-icon img-fluid"></div>
          </div>
        </div>

        <div class="col-12 col-md-4">
          <h3 class="mb-4 text-info">Other Tools</h3>
          <div class="tool-icons row justify-content-center align-items-center g-4">
            <div class="col-6"><img :src="heroku" alt="Heroku" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="git" alt="Git" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="postman" alt="Postman" class="tool-icon img-fluid"></div>
            <div class="col-6"><img :src="vscode" alt="Visual Studio Code" class="tool-icon img-fluid"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>