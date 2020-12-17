<template>
    <div id="User">
        <br />
        <h2 >Bienvenido</h2>
        <br />
        <center>
            <form>
                <div class = "formulario" >
                    <div class="form-row" >
                        <div class="form-group col-md-5">
                            <label for="usuario">Usuario:</label>
                            <input type="text" class="form-control" id="usuario" name="usuario" value=""  placeholder="Ingrese su usuario"/>
                        </div>
                    </div>
                    <div class="form-row" >
                        <div class="form-group col-md-5">
                            <label for="password">Contraseña:</label>
                            <input type="text" class="form-control" id="password" name="password" value=""  placeholder="Ingrese su contraseña"/>
                        </div>
                        <div>
                            <br>
                            <button type="button" class="btn btn-warning" v-on:click="mostrarContrasena">Mostrar contraseña</button>
                        </div>
                    </div>
                </div>
                <button type="submit" class="btn btn-warning">Ingresar</button><br><br>
                <button type="button" class="btn btn-warning">Olvidó su contraseña</button>
            </form>
        </center>
    </div>
</template>

<script>
    import axios from "axios";
export default {
    name: "User",

    data: function () {
        return {
            user_name: "",
            user_pass: "",
        };
    },

    methods: {
        init: function () {
        if (this.$route.name != "user") {
            let username = input.usuario.getItem("current_username");
            this.$router.push({name: "user", params: { username: 'username' }});
        }
        },

        mostrarContrasena: function (){
        var tipo = document.getElementById("password");
        if(tipo.type == "password"){
            tipo.type = "text";
        }else{
            tipo.type = "password";
        }
        }
    },
}
</script>

<style>
#User span{
    color: #f5a018;
    font-weight: bold;
}

#User {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-items: center; 
    margin-bottom: 0%;
}
#User h2{
    width: 100%;
    text-align: center;
    margin-top: 1%;
    color:  #fffdfd;
}
#User .formulario {
    color:  #fffdfd;
    align-content: center;
    display: block;
    margin-left: 37%;
    font-weight: bold;
    margin-bottom: 1%;
    place-content: center;
}

#User button {
    color:  #181818;
}

</style>
