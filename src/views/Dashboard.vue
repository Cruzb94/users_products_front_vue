<template>
    <div>
        <div class="container-fluid">
            
            <br><br>
            <h2>List of users</h2>
                
                <button style="margin-left: 85%;" type="button" class="btn btn-warning" v-on:click="openModalNuevoUsuario">New User</button> 
                    <table class="table" id="datatable">
                        <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Email</th>
                            <th>Password</th>
                            <th>Phone</th>
                            <th>Username</th>
                            <th>Date Birth</th>
                            <th>State</th>
                            <th>Options</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="item in users" :key="item.id">
                            <td>{{item.id}}</td>
                            <td>{{item.name}}</td>
                            <td>{{item.email}}</td>
                            <td>{{item.password}}</td>
                            <td>{{item.phone}}</td>
                            <td>{{item.username}}</td>
                            <td>{{item.date_birth}}</td>
                            <td>{{item.state}}</td>
                            <td>
                                <button type="button" v-on:click="openModalEditarUsuario(item.id)" class="btn btn-info">Editar</button>
                                <button type="button" v-on:click="deleteUser(item.id)" class="btn btn-danger">Eliminar</button>
                            </td>
                        </tr>
                        </tbody>
                    </table>
                 <!-- Modal nuevo usuario -->
                <b-modal id="nuevo_usuario" hide-footer>
                    <div class="container-fluid" >  
                        <br>
                        <form>
                            <div class="form-group">
                                <label for="name">Name:</label>
                                <input type="text" class="form-control" id="name" placeholder="Nombre" v-model="name" required>
                            </div>
                            <div class="form-group">
                                <label for="email">Email:</label>
                                <input type="text" class="form-control" id="email" placeholder="Email" v-model="email" required>
                            </div>
                            <div class="form-group">
                                <label for="password">Password:</label>
                                <input type="text" class="form-control" id="password" placeholder="Password" v-model="password" required>
                            </div>
                            <div class="form-group">
                                <label for="phone">Phone:</label>
                                <input type="text" class="form-control" id="phone" placeholder="Phone" v-model="phone">
                            </div>
                            <div class="form-group">
                                <label for="username">Username:</label>
                                <input type="text" class="form-control" id="username" placeholder="Username" v-model="username" required>
                            </div>
                            <div class="form-group">
                                <label for="username">State:</label>
                                <input type="text" class="form-control" id="state" placeholder="State" v-model="state">
                            </div>
                            <div class="form-group">
                                <label for="date_birth">Date Birth:</label>
                                <input type="date" class="form-control" id="date_birth" placeholder="Date Birth" v-model="date_birth">
                            </div>
                            <br>
                            <button type="button" class="btn btn-primary" style="margin-bottom: 60px;" v-on:click="nuevoUsuario">Guardar</button>
                        </form>
                    </div>    
                </b-modal>
                 <!-- Modal editar usuario -->
                <b-modal id="editar_usuario" hide-footer>
                    <div class="container-fluid">  
                        <br>
                        <form>
                            <div class="form-group">
                                <label for="name">Name:</label>
                                <input type="text" class="form-control" id="name" placeholder="Nombre" v-model="name" required>
                            </div>
                            <div class="form-group">
                                <label for="email">Email:</label>
                                <input type="text" class="form-control" id="email" placeholder="Email" v-model="email" required>
                            </div>
                            <div class="form-group">
                                <label for="password">Password:</label>
                                <input type="text" class="form-control" id="password" placeholder="Password" v-model="password" required>
                            </div>
                            <div class="form-group">
                                <label for="phone">Phone:</label>
                                <input type="text" class="form-control" id="phone" placeholder="Phone" v-model="phone">
                            </div>
                            <div class="form-group">
                                <label for="username">Username:</label>
                                <input type="text" class="form-control" id="username" placeholder="Username" v-model="username" required>
                            </div>
                            <div class="form-group">
                                <label for="date_birth">Date Birth:</label>
                                <input type="text" class="form-control" id="date_birth" placeholder="Date Birth" v-model="date_birth">
                            </div>
                            <div class="form-group">
                                <label for="date_birth">State:</label>
                                <input type="text" class="form-control" id="state" placeholder="State" v-model="state">
                            </div>
                            <br>
                            <button type="button" class="btn btn-primary" style="margin-bottom: 60px;" v-on:click="updateUsuario">Guardar</button>
                        </form>
                    </div>    
                </b-modal>
            </div>
        
            
            <br><br>
            <h2>List of Products</h2>
                
                <button style="margin-left: 85%;" type="button" class="btn btn-warning" v-on:click="openModalNuevoProducto">New Product</button> 
                    <table class="table" id="datatable_products">
                        <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                            <th>Description</th>
                            <th>Sku</th>
                            <th>Quantity</th>
                            <th>Amount</th>
                            <th>Options</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="item in products" :key="item.id">
                            <td>{{item.id}}</td>
                            <td>{{item.name}}</td>
                            <td>{{item.description}}</td>
                            <td>{{item.sku}}</td>
                            <td>{{item.quantity}}</td>
                            <td>{{item.amount}}</td>
                            <td>
                                <button type="button" v-on:click="openModalEditarProduct(item.id)" class="btn btn-info">Editar</button>
                                <button type="button" v-on:click="deleteProduct(item.id)" class="btn btn-danger">Eliminar</button>
                            </td>
                        </tr>
                        </tbody>
                    </table>
                   <!-- Modal nuevo producto -->
                <b-modal id="nuevo_producto" hide-footer>
                    <div class="container-fluid" >  
                        <br>
                        <form>
                            <div class="form-group">
                                <label for="name">Name:</label>
                                <input type="text" class="form-control" id="name" placeholder="Nombre" v-model="product_name">
                            </div>
                            <div class="form-group">
                                <label for="description">Description:</label>
                                <input type="text" class="form-control" id="description" placeholder="Description" v-model="product_description">
                            </div>
                            <div class="form-group">
                                <label for="sku">Sku:</label>
                                <input type="text" class="form-control" id="sku" placeholder="Sku" v-model="product_sku">
                            </div>
                            <div class="form-group">
                                <label for="Quantity">Quantity:</label>
                                <input type="text" class="form-control" id="quantity" placeholder="Quantity" v-model="product_quantity">
                            </div>
                            <div class="form-group">
                                <label for="amount">Amount:</label>
                                <input type="text" class="form-control" id="amount" placeholder="Amount" v-model="product_amount">
                            </div>
                            <br>
                            <button type="submit" class="btn btn-primary" style="margin-bottom: 60px;" v-on:click="nuevoProducto">Guardar</button>
                        </form>
                    </div>    
                </b-modal>
                <!-- Modal editar producto -->
                <b-modal id="editar_producto" hide-footer>
                    <div class="container-fluid" >  
                        <br>
                        <form>
                            <div class="form-group">
                                <label for="name">Name:</label>
                                <input type="text" class="form-control" id="name" placeholder="Nombre" v-model="product_name" required>
                            </div>
                            <div class="form-group">
                                <label for="description">Description:</label>
                                <input type="text" class="form-control" id="description" placeholder="Description" v-model="product_description">
                            </div>
                            <div class="form-group">
                                <label for="sku">Sku:</label>
                                <input type="text" class="form-control" id="sku" placeholder="Sku" v-model="product_sku">
                            </div>
                            <div class="form-group">
                                <label for="Quantity">Quantity:</label>
                                <input type="text" class="form-control" id="quantity" placeholder="Quantity" v-model="product_quantity" required>
                            </div>
                            <div class="form-group">
                                <label for="amount">Amount:</label>
                                <input type="text" class="form-control" id="amount" placeholder="Amount" v-model="product_amount" required>
                            </div>
                            <br>
                            <button type="button" class="btn btn-primary" style="margin-bottom: 60px;" v-on:click="updateProduct">Guardar</button>
                        </form>
                    </div>    
                </b-modal>
    </div>
</template>
<script>

import 'jquery/dist/jquery.min.js';
import 'bootstrap/dist/css/bootstrap.min.css';
import "datatables.net-dt/js/dataTables.dataTables"
import "datatables.net-dt/css/jquery.dataTables.min.css"
import axios from 'axios';
import $ from 'jquery'; 

    export default {
        name: "Dashboard",
        data(){
            return {
                //user
                users: '',
                user_id: '',
                name: '',
                email: '',
                password: '',
                phone: '',
                username: '',
                date_birth: '',
                state: '',
                //products
                products: '',
                product_id: '',
                product_name: '',
                product_description: '',
                product_sku: '',
                product_quantity: '',
                product_amount: ''
            }
        },
        components: {
        },
        mounted: function() {
            
            this.getUsuarios();
            this.getProducts();
        },
        methods: {
            getUsuarios() {

                 const config = {
                headers: { Authorization: `Bearer ${localStorage.token}` }
            };

                let url = process.env.VUE_APP_URL+'/api/v1/users';

                axios.get(url, config).then(data => {
                    this.users = data.data;
                     
                }).finally(() => {
                    $('#datatable').DataTable(); 
                });
            },
            nuevoUsuario: function() {
                const config = {
                    headers: { Authorization: `Bearer ${localStorage.token}` }
                };

                const url = process.env.VUE_APP_URL+'/api/v1/users';

                let formData = new FormData();
                formData.append('name', this.name);
                formData.append('email', this.email);
                formData.append('password', this.password);
                formData.append('phone', this.phone);
                formData.append('username', this.username);
                formData.append('date_birth', this.date_birth);
                formData.append('state', this.state);


                axios.post(url, formData, config)
                    .then(data => {
                        
                    this.getUsuarios();
                     alert(data.data.message);
                     

                    this.user_id = '';
                    this.name = '';
                    this.email = '';
                    this.password = '';
                    this.phone = '';
                    this.username = '';
                    this.date_birth = '';
                    this.state = '';

                    this.$bvModal.hide('nuevo_usuario');
                }).catch(error => {
                    console.log(error);
                    alert('You must fill in all fields');

                });
            },
            updateUsuario: function() {
                const config = {
                    headers: { Authorization: `Bearer ${localStorage.token}` }
                };

                const url = process.env.VUE_APP_URL+'/api/v1/users/'+this.user_id;

                let formData = new FormData();
                formData.append('_method', 'PUT');
                formData.append('id', this.user_id);
                formData.append('name', this.name);
                formData.append('email', this.email);
                formData.append('password', this.password);
                formData.append('phone', this.phone);
                formData.append('username', this.username);
                formData.append('date_birth', this.date_birth);
                formData.append('state', this.state);

                axios.post(url, formData, config)
                    .then(data => {
                    this.getUsuarios();
                     alert(data.data.message);
                    console.log(data);
                     
                    this.user_id = '';
                    this.name = '';
                    this.email = '';
                    this.password = '';
                    this.phone = '';
                    this.username = '';
                    this.date_birth = '';
                    this.state = '';

                    this.$bvModal.hide('editar_usuario');
                }).catch(error => {
                    console.log(error);
                    alert('You must fill in all fields');

                });
            },
            openModalEditarUsuario: function(id) {
                
                for (let i = 0; i < this.users.length; i++) {
                    if(this.users[i].id == id) {
                        this.user_id = this.users[i].id;
                        this.name = this.users[i].name;
                        this.email = this.users[i].email;
                        this.password = this.users[i].password;
                        this.phone = this.users[i].phone;
                        this.username = this.users[i].username;
                        this.date_birth = this.users[i].date_birth;
                        this.state = this.users[i].state;
                    }
                }

                this.$bvModal.show('editar_usuario');
            },
            openModalNuevoUsuario: function() {
                this.$bvModal.show('nuevo_usuario');
            },
            deleteUser: function(user_id) {

                if (window.confirm("Want to delete this user?")) {
                    const config = {
                        headers: { Authorization: `Bearer ${localStorage.token}` }
                    };

                    let formData = new FormData();
                    formData.append('_method', 'DELETE');

                    axios.post(process.env.VUE_APP_URL+"/api/v1/users/"+user_id, formData, config)
                        .then(data => {
                            this.getUsuarios();
                            alert('User Deleted');
                            console.log(data);
                            
                    });  
                    
                }
            }, 
            openModalNuevoProducto: function() {
                this.$bvModal.show('nuevo_producto');
            },
            getProducts() {

                const config = {
                    headers: { Authorization: `Bearer ${localStorage.token}` }
                };

                let url = process.env.VUE_APP_URL+'/api/v1/products';

                axios.get(url, config).then(data => {
                    this.products = data.data;
                     
                }).finally(() => {
                    $('#datatable_products').DataTable(); 
                });
            },
            nuevoProducto: function() {
                const config = {
                    headers: { Authorization: `Bearer ${localStorage.token}` }
                };

                const url = process.env.VUE_APP_URL+'/api/v1/products';

                let formData = new FormData();
                formData.append('name', this.product_name);
                formData.append('description', this.product_description);
                formData.append('sku', this.product_sku);
                formData.append('quantity', this.product_quantity);
                formData.append('amount', this.product_amount);

                axios.post(url, formData, config)
                    .then(data => {
                    this.getProducts();
                    alert(data.data.message);
                    this.product_id = '';
                    this.product_name = '';
                    this.product_description = '';
                    this.product_sku = '';
                    this.product_quantity = '';
                    this.product_amount = '';

                     this.$bvModal.hide('nuevo_producto');
                }).catch(error => {
                    console.log(error);
                    alert('You must fill in all fields');

                })
            },
            openModalEditarProduct: function(id) {
                
                for (let i = 0; i < this.products.length; i++) {
                    if(this.products[i].id == id) {
                        this.product_id = this.products[i].id;
                        this.product_name = this.products[i].name;
                        this.product_description = this.products[i].description;
                        this.product_sku = this.products[i].sku;
                        this.product_quantity = this.products[i].quantity;
                        this.product_amount = this.products[i].amount;
                    }
                }

                this.$bvModal.show('editar_producto');
            },
            updateProduct: function() {
                
                const config = {
                    headers: { Authorization: `Bearer ${localStorage.token}` }
                };

                const url = process.env.VUE_APP_URL+'/api/v1/products/'+this.product_id;

                let formData = new FormData();
                formData.append('_method', 'PUT');
                formData.append('name', this.product_name);
                formData.append('description', this.product_description);
                formData.append('sku', this.product_sku);
                formData.append('quantity', this.product_quantity);
                formData.append('amount', this.product_amount);

                axios.post(url, formData, config)
                    .then(data => {
                     alert(data.data.message);
                     console.log(data);
                     this.getProducts();

                    this.product_id = '';
                    this.product_name = '';
                    this.product_description = '';
                    this.product_sku = '';
                    this.product_quantity = '';
                    this.product_amount = '';

                    this.$bvModal.hide('editar_producto');
                }).catch(error => {
                    console.log(error);
                    alert('You must fill in all fields');

                });
            },
            deleteProduct: function(product_id) {

                if (window.confirm("Want to delete this product?")) {
                    const config = {
                        headers: { Authorization: `Bearer ${localStorage.token}` }
                    };

                    let formData = new FormData();
                    formData.append('_method', 'DELETE');

                    axios.post(process.env.VUE_APP_URL+"/api/v1/products/"+product_id, formData, config)
                        .then(data => {
                            this.getProducts();
                            console.log(data);
                            alert('Product Deleted');
                    });  
                    
                }
            }, 
        }   
    }

</script>
<style scoped>
button {
    margin: 5px;
}

.vm--modal {
    top: 0 !important;
    left: 401px;
    width: 600px;
    height: 600px !important;
}

</style>