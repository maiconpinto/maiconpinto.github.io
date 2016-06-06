---
layout: page
title: Contato
permalink: /contato/
---

<div class="row">
    <form class="col s12" action="https://formspree.io/maiconsilva.pinto@gmail.com" method="POST">
        <input type="hidden" name="_subject" value="Mensagem de maiconpinto.github.io" />

        <div class="row">
            <div class="row">
                <div class="input-field col s6">
                    <input id="first_name" type="text" class="validate" name="nome">
                    <label for="first_name">Nome</label>
                </div>
                <div class="input-field col s6">
                    <input id="last_name" type="text" class="validate" name="sobrenome">
                    <label for="last_name">Sobrenome</label>
                </div>
            </div>
            <div class="row">
                <div class="input-field col s12">
                    <input id="email" type="email" class="validate" name="email">
                    <label for="email">Email</label>
                </div>
            </div>

            <div class="row">
                <div class="input-field col s12">
                    <textarea id="textarea1" class="materialize-textarea" name="mensagem"></textarea>
                    <label for="textarea1">Mensagem</label>
                </div>
            </div>

            <div class="row">
                <div class="input-field col s12">
                    <input id="submit" type="submit" class="waves-effect waves-light btn" value="Enviar">
                </div>
            </div>
        </div>
    </form>
</div>
