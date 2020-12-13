<template>
    <div id="Cliente">
        <h2 style='text-align:center'>REGISTRO DE CLIENTES</h2>
        <h2 id="11" value=""></h2>
        <div style='text-align:left'>
            <right>
                <button  v-on:click="findCliente">Buscar</button>
                <button  v-on:click="makeCliente">Crear</button>
                <button>Actualizar</button>
                <button>Eliminar</button><br /><br />
                
            </right>
        </div>
        <center>
            <form>
                
                <label for="Phone1">Telefono:</label>
                <input type="text" id="Phone" name="Phone" value=""  />&nbsp;
                
                <label for="name">Nombre:</label>
                <input type="text" id="name" name="name" value="" /><br /><br />
                
                <label for="adress">Direccion:</label>
                <input type="text" id="adress" name="adress" value="" />&nbsp;
                
                <label for="zone">Barrio:</label>
                <input type="text" id="zone" name="zone" value="" /><br /><br />
                
                <label for="idCC">Cedula:</label>
                <input type="text" id="idCC" name="idCC" value="" />&nbsp;
                
                <label for="birth">Cumpleanos:</label>
                <input type="text" id="birth" name="birth" value="" /><br /><br />
            </form>
            
        </center>

        
    </div>
</template>

<script>

import axios from "axios";
export default {
    name: "Cliente",
    data: function () {
        return {
            telefono: 0,
            nombre: "",
            direccion: "",
            barrio: "",
            cedula: 0,
            cumpleanos: "",
            balance: 0,
        };
    },

    methods: {
        init: function () {
        if (this.$route.name != "user") {
            let username = input.Phone.getItem("current_username");
            this.$router.push({ name: "user", params: { username: username } });
        }
        },

        findCliente: function () {
            this.telefono = document.getElementById("Phone").value
            let self = this
            axios.get("https://restaurante-back-g1.herokuapp.com/cliente/consulta/" + this.telefono)
                .then((result) => {
                    self.telefono = result.data.telefono
                    self.nombre = result.data.nombre
                    self.direccion = result.data.direccion
                    self.barrio = result.data.barrio
                    self.cedula = result.data.cedula
                    self.cumpleanos = result.data.cumpleanos
                    document.getElementById("Phone").value = self.telefono;
                    document.getElementById("name").value = self.nombre;
                    document.getElementById("adress").value = self.direccion
                    document.getElementById("zone").value = self.barrio
                    document.getElementById("idCC").value = self.cedula
                    document.getElementById("birth").value = self.cumpleanos
                    document.getElementById("11").value = "Se encontro usuario" + self.nombre
                    
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });

        },
        makeCliente: function () {
            this.telefono = document.getElementById("Phone").value
            this.nombre = document.getElementById("name").value
            this.direccion = document.getElementById("adress").value
            this.barrio = document.getElementById("zone").value
            this.cedula = document.getElementById("idCC").value
            this.cumpleanos = document.getElementById("birth").value

            /*newCliente = {
                            "telefono": parseInt(this.telefono, 10),
                            "nombre": this.nombre,
                            "direccion": this.direccion,
                            "barrio": this.barrio,
                            "cedula": this.cedula,
                            "cumpleanos": this.cumpleanos
            };*/    

            let self = this
            //const res = await axios.post('https://httpbin.org/post', { answer: 42 });
            
            axios.post("https://restaurante-back-g1.herokuapp.com/cliente/crear/", {
                            "telefono": parseInt(this.telefono, 10),
                            "nombre": this.nombre,
                            "direccion": this.direccion,
                            "barrio": this.barrio,
                            "cedula": this.cedula,
                            "cumpleanos": this.cumpleanos
            })
                .then((result) => {
                    alert("Cliente Creado");
                    /*
                    self.telefono = result.data.telefono
                    self.nombre = result.data.nombre
                    self.direccion = result.data.direccion
                    self.barrio = result.data.barrio
                    self.cedula = result.data.cedula
                    self.cumpleanos = result.data.cumpleanos
                    document.getElementById("Phone").value = self.telefono;
                    document.getElementById("name").value = self.nombre;
                    document.getElementById("adress").value = self.direccion
                    document.getElementById("zone").value = self.barrio
                    document.getElementById("idCC").value = self.cedula
                    document.getElementById("birth").value = self.cumpleanos
                    document.getElementById("11").value = "Se encontro usuario" + self.nombre
                    */
                    
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });

        }
    },
    /*created: function() {

            this.username = this.$route.params.username

            let self = this
            axios.get("https://cajero-api2.herokuapp.com/user/balance/" + this.username)
                .then((result) => {
                    self.balance = result.data.balance
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });
        }*/

    

};

</script>

<style>
#UserBalance {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
#UserBalance h2 {
    font-size: 50px;
    color: #283747;
}
#UserBalance span {
    color: crimson;
    font-weight: bold;
}
button{
    color: #000000;
    background: #f5a018;
    border: 1px solid #007efc;
    border-radius: 5px;
    padding: 10px 20px;
}
button:hover{
    color: #000000;
    background: #7fbfff;
    border: 1px solid #358035;
}
</style>