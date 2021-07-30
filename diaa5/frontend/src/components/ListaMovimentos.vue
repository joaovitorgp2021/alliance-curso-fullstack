<template>
    <div>
        <b-navbar toggleable="lg" type="dark" variant="info">
            <b-navbar-brand>Movimentações</b-navbar-brand>
            <b-navbar-nav class="ml-auto">
                <b-button v-on:click="$bvModal.show('modal-insert')">
                    <b-icon-plus></b-icon-plus>
                </b-button>
            </b-navbar-nav>
        </b-navbar>
        <b-alert v-model="mostrarErro" variant="danger" dismissible>
            Falha ao {{errorMessage.action}} - {{errorMessage.message}}
        </b-alert>
        <