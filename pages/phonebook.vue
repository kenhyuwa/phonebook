<template>
    <div>
        <nav class="navbar is-transparent is-fixed-top">
            <div class="container is-fluid">
                <div class="navbar-brand">
                    <a class="navbar-item" :href="`/`">
                        <img src="https://bulma.io/images/bulma-logo.png" alt="Bulma: a modern CSS framework based on Flexbox" width="112" height="28">
                    </a>
                    <div class="navbar-burger burger" 
                        :class="{ 'is-active' : isActive }"
                        @click="isActive = !isActive"
                    >
                        <span></span>
                        <span></span>
                        <span></span>
                    </div>
                </div>
                <div class="navbar-menu"
                    :class="{ 'is-active' : isActive }"
                >
                    <div class="navbar-start">
                        <a class="navbar-item" :href="`/`">
                            Home
                        </a>
                        <div class="navbar-item has-dropdown is-hoverable">
                            <a class="navbar-link" href="/documentation/overview/start/">
                                Docs
                            </a>
                            <div class="navbar-dropdown is-boxed">
                                <a class="navbar-item" href="/documentation/overview/start/">
                                    Overview
                                </a>
                                <a class="navbar-item" href="https://bulma.io/documentation/modifiers/syntax/">
                                    Modifiers
                                </a>
                                <a class="navbar-item" href="https://bulma.io/documentation/columns/basics/">
                                    Columns
                                </a>
                                <a class="navbar-item" href="https://bulma.io/documentation/layout/container/">
                                    Layout
                                </a>
                                <a class="navbar-item" href="https://bulma.io/documentation/form/general/">
                                    Form
                                </a>
                                <hr class="navbar-divider">
                                <a class="navbar-item" href="https://bulma.io/documentation/elements/box/">
                                    Elements
                                </a>
                                <a class="navbar-item is-active" href="https://bulma.io/documentation/components/breadcrumb/">
                                    Components
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="navbar-end">
                        <div class="navbar-item">
                            <div class="field is-grouped"
                                :style="'justify-content: center;'"
                            >
                                <p class="control">
                                    <a class="bd-tw-button button is-danger" data-social-network="Twitter" data-social-action="tweet" data-social-target="http://localhost:4000" target="_blank" href="https://twitter.com/intent/tweet?text=Bulma: a modern CSS framework based on Flexbox&amp;hashtags=bulmaio&amp;url=http://localhost:4000&amp;via=jgthms">
                                        <span class="icon">
                                            <i class="fa fa-twitter"></i>
                                        </span>
                                        <span>
                                            Tweet
                                        </span>
                                    </a>
                                </p>
                                <p class="control">
                                    <a class="button is-primary" href="https://github.com/jgthms/bulma/releases/download/0.7.1/bulma-0.7.1.zip">
                                        <span class="icon">
                                            <i class="fa fa-download"></i>
                                        </span>
                                        <span>Download</span>
                                    </a>
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </nav>
        <section class="hero is-primary"
            :style="'margin-top: 50px;'"
        >
            <div class="hero-body">
                <div class="container">
                    <h1 class="title">
                    Phonebook App
                    </h1>
                    <h2 class="subtitle">
                    Learn nuxt-JS example
                    </h2>
                </div>
            </div>
        </section>
        <section class="section">
            <div class="container">
                <div class="columns">
                    <div class="column is-4">
                        <nav class="panel">
                            <p class="panel-heading">
                                My friends
                            </p>
                            <div class="panel-block">
                                <p class="control has-icons-left">
                                    <input class="input is-small" type="text" placeholder="search">
                                    <span class="icon is-small is-left">
                                        <i class="fa fa-search" aria-hidden="true"></i>
                                    </span>
                                </p>
                            </div>
                            <a class="panel-block" 
                                v-for="f in friends"
                                :key="f.id"
                                @click="showFriend(f)"
                            >
                                <span class="panel-icon">
                                    <i class="fa fa-book" aria-hidden="true"></i>
                                </span>
                                {{ f.name }}
                            </a>
                            <div class="panel-block">
                                <button class="button is-link is-outlined is-fullwidth"
                                    @click="isOpenModal = true"
                                >
                                New friend
                                </button>
                            </div>
                        </nav>
                    </div>
                    <div class="column is-8">
                        <nav class="panel">
                            <p class="panel-heading">
                                Detail friends
                                <button class="button is-small is-pulled-right is-danger"
                                    @click="destroyFriend(friend)"
                                >Delete
                                </button>
                            </p>
                            <div>
                                <div class="panel-block">
                                    Name : {{ friend.name }}
                                </div>
                                <div class="panel-block">
                                    Phone : {{ friend.phone }}
                                </div>
                            </div>
                        </nav>
                    </div>
                </div>
            </div>
        </section>
        <div class="modal"
            :class="{ 'is-active' : isOpenModal }"
        >
            <div class="modal-background"></div>
            <div class="modal-card">
                <header class="modal-card-head">
                    <p class="modal-card-title">New friend</p>
                    <button class="delete" aria-label="close"
                        @click="closeModal"
                    ></button>
                </header>
                <form @submit="newFriend">
                    <section class="modal-card-body">
                        <div class="field">
                            <label class="label">Name</label>
                            <div class="control has-icons-left has-icons-right">
                                <input class="input" placeholder="Text input"
                                    autofocus="true"
                                    v-model="name"
                                    :class="{ 'is-danger' : !validName, 'is-success' : validName }"
                                    @keyup="validationName"
                                >
                                <span class="icon is-small is-left">
                                    <i class="fa fa-user"></i>
                                </span>
                                <span class="icon is-small is-right" v-if="validName && name.length > 0">
                                    <i class="fa fa-check"></i>
                                </span>
                                <span class="icon is-small is-right" v-if="!validName">
                                    <i class="fa fa-times"></i>
                                </span>
                            </div>
                            <p class="help is-danger" v-if="!validName">This name is required</p>
                        </div>
                        <div class="field">
                            <label class="label">Phone number</label>
                            <div class="control has-icons-left has-icons-right">
                                <input class="input" placeholder="Text input"
                                    v-model="phone"
                                    :class="{ 'is-danger': !validPhone || !validPhoneNumber, 'is-success' : validPhone }"
                                    @keyup="validationPhone"
                                >
                                <span class="icon is-small is-left">
                                    <i class="fa fa-user"></i>
                                </span>
                                <span class="icon is-small is-right" v-if="validPhone && phone.length > 0">
                                    <i class="fa fa-check"></i>
                                </span>
                                <span class="icon is-small is-right" v-if="!validPhone">
                                    <i class="fa fa-times"></i>
                                </span>
                            </div>
                            <p class="help is-danger" v-if="!validPhone">This phone number is required</p>
                            <p class="help is-danger" v-if="!validPhoneNumber">This phone number is not valid</p>
                        </div>
                    </section>
                    <footer class="modal-card-foot">
                        <button class="button"
                            @click="closeModal"
                        >Cancel</button>
                        <button class="button is-success">Save</button>
                    </footer>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        data(){
            return{
                isActive: false,
                isOpenModal: false,
                friends: [],
                friend: {},
                name: '',
                phone: '',
                count: 0,
                validName: true,
                validPhone: true,
                validPhoneNumber: true,
            }
        },

        methods:{
            validationName(){
                if(this.name == ''){
                    this.validName = false
                }else{
                    this.validName = true
                }
            },
            validationPhone(){
                if(this.phone == ''){
                    this.validPhone = false
                }else{
                    this.validPhone = true
                }
                if(this.phone != '' && Number(this.phone) >= 0 == false){
                    this.validPhoneNumber = false
                }else{
                    this.validPhoneNumber = true
                }
            },
            newFriend(e){
                e.preventDefault()
                if(this.name != '' && this.phone != ''){
                    const data = {
                        id: ++this.count,
                        name: this.name,
                        phone: this.phone
                    }
                    this.friends.push(data)
                    this.formReset()
                }
            },
            formReset(){
                this.name = ''
                this.phone = ''
                this.isOpenModal = false
                validName: true
                validPhone: true
                validPhoneNumber: true
            },
            showFriend(friend){
                this.friend = friend
            },
            destroyFriend(friend){
                _.remove(this.friends, function(o){
                    return o.id == friend.id
                })
                this.friend = {}
            },
            closeModal(){
                this.formReset()
            }
        },
    }
</script>

<style lang="scss">
.wrapper{
    clear: both;
    box-sizing: border-box;
    .left{
        width: 30%;
        float: left;
    }
    .right{
        width: 70%;
    }
}
</style>