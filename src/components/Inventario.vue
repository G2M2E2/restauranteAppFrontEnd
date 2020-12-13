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
            let username = input.id.getItem("current_username");
            this.$router.push({ name: "user", params: { username: username }});
        }
        },

        findProducto: function () {
            this.id = document.getElementById("id").value
            let self = this
            axios.get("https://restaurantemintic.herokuapp.com/producto/consulta/" + this.id)
                .then((result) => {
                    self.id = result.data.id
                    self.nombre = result.data.nombre
                    self.precio = result.data.precio
                    self.cantidad = result.data.cantidad
                    self.categoria = result.data.categoria
                    
                    document.getElementById("id").value = self.id;
                    document.getElementById("name").value = self.nombre;
                    document.getElementById("price").value = self.precio
                    document.getElementById("quantity").value = self.cantidad
                    document.getElementById("category").value = self.categoria
                    document.getElementById("11").value = "Se encontro el producto" + self.nombre                   
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });
        },
        makeProducto: function () {
            this.id = document.getElementById("id").value
            this.nombre = document.getElementById("name").value
            this.precio = document.getElementById("price").value
            this.cantidad = document.getElementById("quantity").value
            this.categoria = document.getElementById("category").value
    
            let self = this
            
            axios.post("https://restaurante-back-g1.herokuapp.com/producto/crear/", {
                            "id": parseInt(this.telefono, 10),
                            "nombre": this.nombre,
                            "precio": this.precio,
                            "cantidad": this.cantidad,
                            "categoria": this.categoria,
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