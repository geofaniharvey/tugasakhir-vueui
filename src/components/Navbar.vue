<template>

<div class="container-fluid">
    <div class="row row-cols-2">
        <div class="col col-auto">
            <nav id="navbar-example3" class="navbar navbar-light bg-light flex-column align-items-stretch p-3">
            <a class="navbar-brand" href="#">Piket</a>
            <nav class="nav nav-pills flex-column">
                <a class="nav-link" href="#namap">Nama Pegawai</a>
                    <router-link class="nav-link"  to="/">Home</router-link>
                <a class="nav-link" href="#shift">Shift</a>
                <nav class="nav nav-pills flex-column">
                  <router-link class="nav-link" to="/shifts">Shift</router-link>
                <a class="nav-link ms-3 my-1" href="#opening">Opening</a>
                <a class="nav-link ms-3 my-1" href="#closing">Closing</a>
                </nav>
            </nav>
            </nav>
    </div>
    </div>
    </div>
</template>

<script>
export default {};
</script>

<style>
</style>