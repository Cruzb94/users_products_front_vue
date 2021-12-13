<template>
    <div>
        <div class="container">
            
            <br><br>
            <h2>Lista de usuarios</h2>
                
                <div class="container">
                <button style="margin-left: 85%;" type="button" class="btn btn-warning" v-on:click="openModalNuevoUsuario">Nuevo Contacto</button> 
                    <div class="row card_user" v-for="user in users" :key="user.id">
                        <div class="col-2">
                        <img :src="getUserImagen(user.id)" class="rounded" alt="Cinque Terre" style="width: 72px;
height: 72px;">
                        
                        </div>
                        <div class="col-2">
                        {{ user.name}}
                        </div>
                        <div class="col-6">
                         {{ user.description}}
                        </div>
                        <div class="col">
                        <svg style="cursor:pointer;" v-on:click="openModalEditarUsuario(user.id)" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil" viewBox="0 0 16 16">
  <path d="M12.146.146a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1 0 .708l-10 10a.5.5 0 0 1-.168.11l-5 2a.5.5 0 0 1-.65-.65l2-5a.5.5 0 0 1 .11-.168l10-10zM11.207 2.5 13.5 4.793 14.793 3.5 12.5 1.207 11.207 2.5zm1.586 3L10.5 3.207 4 9.707V10h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.293l6.5-6.5zm-9.761 5.175-.106.106-1.528 3.821 3.821-1.528.106-.106A.5.5 0 0 1 5 12.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.468-.325z"/>
</svg>
                        </div>
                    </div>
                </div>
                 <!-- Modal nuevo usuario -->
                <modal name="nuevo_usuario" >
                    <div class="container-fluid" style="height: 200px;">  
                        <br>
                        <form>
                            <div class="form-group">
                                <label for="name">Nombre:</label>
                                <input type="text" class="form-control" id="name" placeholder="Nombre" v-model="name">
                            </div>
                            <div class="form-group">
                                <label for="email">email:</label>
                                <input type="text" class="form-control" id="email" placeholder="Email" v-model="email">
                            </div>
                            <div class="form-group">
                                <label for="description">Descripción:</label>
                                <input type="text" class="form-control" id="description" placeholder="Descripción" v-model="description">
                            </div>
                            <div class="form-group">
                                <label for="exampleFormControlFile1">Foto</label>
                                <input type="file" v-on:change="obtenerImagen" class="form-control-file" id="exampleFormControlFile1">
                            </div>
                            <br>
                            <button type="button" class="btn btn-primary" style="margin-bottom: 60px;" v-on:click="nuevoUsuario">Guardar</button>
                        </form>
                    </div>    
                </modal>
                 <!-- Modal editar usuario -->
                <modal name="editar_usuario" >
                    <div class="container-fluid" style="height: 200px;">  
                        <br>
                        <form>
                            <div class="form-group">
                                <label for="name">Nombre:</label>
                                <input type="text" class="form-control" id="name" placeholder="Nombre" v-model="name">
                            </div>
                            <div class="form-group">
                                <label for="email">email:</label>
                                <input type="text" class="form-control" id="email" placeholder="Email" v-model="email">
                            </div>
                            <div class="form-group">
                                <label for="description">Descripción:</label>
                                <input type="text" class="form-control" id="description" placeholder="Descripción" v-model="description">
                            </div>
                            <div class="form-group">
                                <label for="exampleFormControlFile1">Foto</label>
                                <input type="file" v-on:change="obtenerImagen" class="form-control-file" id="exampleFormControlFile1">
                            </div>
                            <br>
                            <button type="button" class="btn btn-primary" style="margin-bottom: 60px;" v-on:click="updateUsuario">Actualizar</button>
                        </form>
                    </div>    
                </modal>
            </div>
    </div>
</template>
<script>

import axios from 'axios';

    export default {
        name: "Dashboard",
        data(){
            return {
                users: '',
                user_id: '',
                name: '',
                email: '',
                description: '',
                image: '',
                url_image :process.env.VUE_APP_URL+"/storage/"
            }
        },
        components: {
        },
        mounted: function() {

            this.login();
            this.getUsuarios();
        },
        methods: {
            login() {

                axios.post(process.env.VUE_APP_URL+"/api/auth/login")
                    .then(data => {
                    if(data.statusText == 'OK') {
                        localStorage.token = data.data.access_token;
                    } else {
                        this.error = true;
                        this.error_msg = 'Datos incorrectos';
                    }
                    
                    })
            },
            getUsuarios() {
                 const config = {
                headers: { Authorization: `Bearer ${localStorage.token}` }
            };

                let url_groups = process.env.VUE_APP_URL+'/api/auth/users';

                axios.get(url_groups, config).then(data => {
                    this.users = data.data;

                    console.log(this.users);  
                })
            },
            getUserImagen(id) {
                
                for(let i = 0; i < this.users.length; i++) {
                    if(this.users[i].id == id) {
                        if(this.users[i].image.length > 0 && this.users[i].image !== "") {
                            console.log('this.users[i].image.length', this.users[i].image.length);
                            return this.url_image + this.users[i].image[0].Ima_profile;
                        } else {
                            return "/assets/user.jpg";
                        }
                    }
                }
            },
            nuevoUsuario: function() {
                const config = {
                    headers: { Authorization: `Bearer ${localStorage.token}` }
                };

                const url = process.env.VUE_APP_URL+'/api/auth/signup';

                let formData = new FormData();
                formData.append('name', this.name);
                formData.append('email', this.email);
                formData.append('description', this.description);
                formData.append('image', this.image);

                axios.post(url, formData, config)
                    .then(data => {
                     alert(data.data.message);
                     this.getUsuarios();

                    this.user_id = '';
                    this.name = '';
                    this.email = '';
                    this.description = '';
                    this.image = '';

                     this.$modal.hide('nuevo_usuario');
                });
            },
            updateUsuario: function() {
                const config = {
                    headers: { Authorization: `Bearer ${localStorage.token}` }
                };

                const url = process.env.VUE_APP_URL+'/api/auth/update';

                let formData = new FormData();
                formData.append('id', this.user_id);
                formData.append('name', this.name);
                formData.append('email', this.email);
                formData.append('description', this.description);
                formData.append('image', this.image);

                axios.post(url, formData, config)
                    .then(data => {
                     alert(data.data.message);
                     this.getUsuarios();

                    this.user_id = '';
                    this.name = '';
                    this.email = '';
                    this.description = '';
                    this.image = '';

                    this.$modal.hide('editar_usuario');
                });
            },
            openModalEditarUsuario: function(id) {
                for(let i = 0; i < this.users.length; i++) {
                    if(this.users[i].id == id) {
                       
                         this.user_id =  this.users[i].id;
                         this.name = this.users[i].name;
                         this.email = this.users[i].email;
                         this.description = this.users[i].description;
                        
                    }
                }
                this.$modal.show('editar_usuario');
            },
            openModalNuevoUsuario: function() {
                this.$modal.show('nuevo_usuario');
            },
            saveGroup: function() {
                const headers = { 
                    "Authorization": `Bearer ${localStorage.token}`,
                };

                const url_save = process.env.VUE_APP_URL+'/api/auth/save-group';

                const group = { name: this.new_group_name, description: this.new_group_description };
                axios.post(url_save, group, { headers })
                    .then(response => {
                        console.log(response);
                        this.getGroups();
                        alert('Grupo Creado!');
                    });

                    this.$modal.hide('nuevo_grupo');
            },
            obtenerImagen(e) {
                let file = e.target.files[0];
                this.image = file;
                // this.cargarImagen(file);
            }
        }   
    }

</script>
<style scoped>
button {
    margin: 5px;
}

.card_user {
    top: 199px;
    left: 49px;
    width: 100%;
    height: 114px;
    background: #FFFFFF ;
    box-shadow: 3px 3px 3px #A0A0A0BF;
    border-radius: 12px;
    opacity: 1;
    margin-top: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>