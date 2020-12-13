<template>
    <div id="Inventario">
        <h2 style='text-align:center'>MÓDULO DE INVENTARIOS</h2>
        <div style='text-align:left'>
            <left>
                <button  v-on:click="findProducto">Buscar</button>
                <button  v-on:click="createProducto">Crear</button>
                <button>Actualizar</button>
                <button>Eliminar</button><br><br>
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
            this.id = document.getElementById("idprod").value
            let self = this
            axios.get("https://restaurante-back-g1.herokuapp.com/producto/consulta/" + this.id)
                .then((result) => {
                    self.id = result.data.id
                    self.nombre = result.data.nombre
                    self.precio = result.data.precio
                    self.cantidad = result.data.cantidad
                    self.categoria = result.data.categoria
                    
                    document.getElementById("idprod").value = self.id;
                    document.getElementById("nomprod").value = self.nombre;
                    document.getElementById("precprod").value = self.precio;
                    document.getElementById("cantprod").value = self.cantidad;
                    document.getElementById("catprod").value = self.categoria;                 
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });
        },
        createProducto: function () {
            this.id = document.getElementById("idprod").value
            this.nombre = document.getElementById("nomprod").value
            this.precio = document.getElementById("precprod").value
            this.cantidad = document.getElementById("cantprod").value
            this.categoria = document.getElementById("catprod").value
    
            let self = this
            
            axios.post("https://restaurante-back-g1.herokuapp.com/producto/crear/", {
                            "id": this.id,
                            "nombre": this.nombre,
                            "precio": parseInt(this.precio),
                            "cantidad": parseInt(this.cantidad),
                            "categoria": this.categoria
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