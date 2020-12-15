<template>
    <div id="Cliente">
        <br />
        <h2 style='text-align:center'>REGISTRO DE CLIENTES</h2>
        <br />
        
        <form>
            

            <div class="form-row">
                <div class="form-group col-md-6">
                    <label for="Phone1">Telefono:</label>
                    <input type="number" class="form-control" id="Phone" name="Phone" value=""  placeholder="Telefono"/>
                </div>
                <div class="form-group col-md-6">
                    <label for="name">Nombre:</label>
                    <input type="text" class="form-control" id="name" name="name" value="" placeholder="Nombre"/>
                </div>
            </div>
            <div class="form-group">
                <label for="adress">Direccion:</label>
                <input type="text" class="form-control" id="adress" name="adress" value="" placeholder="1234 Main St"/>
            </div>
            <div class="form-row">
                <div class="form-group col-md-6">
                    <label for="zone">Barrio:</label>
                    <input type="text" class="form-control" id="zone" name="zone" value="" placeholder="Barrio"/>

                </div>
                <div class="form-group col-md-4">
                    <label for="idCC">Cedula:</label>
                    <input type="text" class="form-control" id="idCC" name="idCC" value="" placeholder="Cedula"/>
                    
                </div>
                <div class="form-group col-md-2">
                    <label for="birth">Cumpleanos:</label>
                    <input type="text" class="form-control" id="birth" name="birth" value="" placeholder="yyyy-mm-dd"/>
                    
                </div>
            </div>
            <br />
            <div style='text-align:center'>
                <right>
                    <button type="button" class="btn btn-warning" v-on:click="myProvider">Lista</button>
                    <button type="button" class="btn btn-warning"  v-on:click="findCliente">Buscar</button>
                    <button type="button" class="btn btn-warning" v-on:click="makeCliente">Crear</button>
                    <button type="button" class="btn btn-warning" >Actualizar</button>
                    <button type="button" class="btn btn-warning" v-on:click="cleanCampos">Limpiar</button>
                    <button type="button" class="btn btn-warning" >Eliminar</button><br /><br />
                    
                    
                </right>
            </div>
        
        </form>
        <br />
        
        <b-table sticky-header ref="table" id="my-table" striped hover :items="items"></b-table>
        
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
            cedula: "",
            cumpleanos: "",
            balance: 0,
            newCliente: {},
            items: []
            
            
        };
    },

    methods: {
        init: function () {
        if (this.$route.name != "cliente") {
            let username = input.Phone.getItem("current_username");
            this.$router.push({name: "cliente", params:{ username: 'username' }});
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
                    confirm("Se encontro el cliente " + self.nombre);
                    document.getElementById("Phone").value = self.telefono;
                    document.getElementById("name").value = self.nombre;
                    document.getElementById("adress").value = self.direccion;
                    document.getElementById("zone").value = self.barrio;
                    document.getElementById("idCC").value = self.cedula;
                    document.getElementById("birth").value = self.cumpleanos;
                    
                })
                .catch((error) => {
                    alert("No se encontro el cliente");
                });

        },
        cleanCampos: function () {
            
            document.getElementById("Phone").value = ""
            document.getElementById("name").value = ""
            document.getElementById("adress").value = ""
            document.getElementById("zone").value = ""
            document.getElementById("idCC").value = ""
            document.getElementById("birth").value = ""
                                
        },
        makeCliente: function () {
            this.telefono = document.getElementById("Phone").value
            this.nombre = document.getElementById("name").value
            this.direccion = document.getElementById("adress").value
            this.barrio = document.getElementById("zone").value
            this.cedula = document.getElementById("idCC").value
            this.cumpleanos = document.getElementById("birth").value

            this.newCliente = {
                            "telefono": parseInt(this.telefono, 10),
                            "nombre": this.nombre,
                            "direccion": this.direccion,
                            "barrio": this.barrio,
                            "cedula": this.cedula,
                            "cumpleanos": this.cumpleanos
            }    
            let self = this            
            axios.post("https://restaurante-back-g1.herokuapp.com/cliente/crear/", this.newCliente)
                .then((result) => {
                    window.confirm("Cliente Creado");
                    
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });
            
            this.myProvider()
            this.$refs.table.refresh()

        },
        myProvider: function () {
            console.log("Entro");
            let self = this
            
            axios.get("https://restaurante-back-g1.herokuapp.com/cliente/lista/")
            .then((result) => {
                self.items = result.data
            }).catch(error => {
                
                alert("ERROR Servidor");
                return []
            })
        },
        

        
        
    },   

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

/*button{
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
}*/
b-table{
    overflow:scroll;
    height:10px;
    width:500px;
}
</style>