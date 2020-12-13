<template>
    <div id="Inventario">
        <h2 style='text-align:center'>MÓDULO DE INVENTARIOS</h2>
        <div style='text-align:left'>
            <left>
                <button v-on:click="init"> Crear </button>
                <button v-on:click="getBalance"> Buscar </button>
                <button> Actualizar </button>
                <button>Eliminar</button>
            </left>
        </div>
        <center>
            <form>
                <label for="idprod">Id producto:</label>
                <input type="text" id="idprod" name="idprod" value="">

                <label for="nomprod">Nombre:</label>
                <input type="text" id="nomprod" name="nomprod" value=""><br><br>

                <label for="precprod">Precio:</label>
                <input type="text" id="precprod" name="precprod" value="">

                <label for="cantprod">Cantidad:</label>
                <input type="text" id="cantprod" name="cantprod" value="">

                <label for="catprod">Categoría:</label>
                <input type="text" id="catprod" name="catprod" value=""><br><br>
            
                <button>Mostrar lista de productos</button><br>
            </form>

        </center>
            <table style="width:100%">
                <tr>
                    <th>Id</th>
                    <th>Nombre</th>
                    <th>Precio</th>
                    <th>Cantidad</th>
                    <th>Categoría</th>
                </tr>
                <tr>
                    <td>CA01</td>
                    <td>Carne asada</td>
                    <td>17000</td>
                    <td>15</td>
                    <td>Carnes</td>
                </tr>
                <tr>
                    <td></td>
                    <td></td>
                    <td></td>
                </tr>
            </table>
        </center>
    </div>
</template>

<script>

import axios from "axios";
export default {
    name: "Inventario",
    data: function () {
        return {
            id: "",
            nombre: "",
            precio: 0,
            cantidad: 0,
            categoria: "",
        };
    },


    methods: {
        init: function () {
        if (this.$route.name != "user") {
            let username = input.idprod.getItem("current_username");
            this.$router.push({ name: "user", params: { username: username }});
        }
        },

        findProducto: function () {
            this.idprod = document.getElementById("idprod").value
            let self = this
            axios.get("https://restaurante-back-g1.herokuapp.com/producto/consulta/" + this.idprod)
                .then((result) => {
                    self.idprod = result.data.idprod
                    self.nomprod = result.data.nomprod
                    self.precprod = result.data.precprod
                    self.cantprod = result.data.cantprod
                    self.catprod = result.data.catprod
                    
                    document.getElementById("idprod").value = self.idprod;
                    document.getElementById("nomprod").value = self.nomprod;
                    document.getElementById("precprod").value = self.precprod
                    document.getElementById("cantprod").value = self.cantprod
                    document.getElementById("catprod").value = self.catprod
                    document.getElementById("11").value = "Se encontro el producto" + self.nomprod                  
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });
        },
        makeProducto: function () {
            this.idprod = document.getElementById("idprod").value
            this.nomprod = document.getElementById("nomprod").value
            this.precprod = document.getElementById("precprod").value
            this.cantprod = document.getElementById("cantprod").value
            this.catprod = document.getElementById("catprod").value
    
            let self = this
            
            axios.post("https://restaurante-back-g1.herokuapp.com/producto/crear/", {
                            "id": parseInt(this.idprod, 10),
                            "nombre": this.nomprod,
                            "precio": this.precprod,
                            "cantidad": this.cantprod,
                            "categoria": this.catprod,
            })
                .then((result) => {
                    alert("Producto Creado");
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });

        }
    },
}
</script>

<style>
#Inventario body {
    margin: 0 0 0 0;
    background-color: #19191a;
    /*background-image: url("./assets/carnep.jpg");*/
    background-size: 100%;
    overflow: hidden;
  }

  #Inventario table, th, td {
    border: 1px solid black;
  }

  #Inventario .main-component{
    height: 75vh;
    margin: 0%;
    padding: 0%;
    background: #fcfafa ;
  } 
</style>