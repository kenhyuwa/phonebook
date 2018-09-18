<template>
    <div class="modal"
        :class="{ 'is-active' : isOpen }"
    >
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
                <p class="modal-card-title">New friend</p>
                <button class="delete" aria-label="close"
                    @click="$nuxt.$emit('closeModal', false)"
                ></button>
            </header>
            <form @submit="newFriend">
                <section class="modal-card-body">
                    <div class="field">
                        <label class="label">Name</label>
                        <div class="control has-icons-left has-icons-right">
                            <input class="input is-success" placeholder="Text input"
                                autofocus="true"
                                v-model="name"
                            >
                            <span class="icon is-small is-left">
                                <i class="fa fa-user"></i>
                            </span>
                            <span class="icon is-small is-right">
                                <i class="fa fa-check"></i>
                            </span>
                            <span class="icon is-small is-right">
                                <i class="fa fa-times"></i>
                            </span>
                        </div>
                        <p class="help is-success">This username is available</p>
                    </div>
                    <div class="field">
                        <label class="label">Phone number</label>
                        <div class="control has-icons-left has-icons-right">
                            <input class="input is-success" placeholder="Text input"
                                v-model="phone"
                            >
                            <span class="icon is-small is-left">
                                <i class="fa fa-user"></i>
                            </span>
                            <span class="icon is-small is-right">
                                <i class="fa fa-check"></i>
                            </span>
                            <span class="icon is-small is-right">
                                <i class="fa fa-times"></i>
                            </span>
                        </div>
                        <p class="help is-success">This username is available</p>
                    </div>
                </section>
                <footer class="modal-card-foot">
                    <button class="button"
                        @click="$nuxt.$emit('closeModal', false)"
                    >Cancel</button>
                    <button class="button is-success">Save</button>
                </footer>
            </form>
        </div>
    </div>
</template>

<script>
    export default{
        props:['isOpen', 'count', 'friend'],
        data(){
            return{
                name: this.friend.length > 0 ? this.friend.name : '',
                phone: this.friend.length > 0 ? this.friend.phone : ''
            }
        },
        methods:{
            newFriend(e){
                e.preventDefault()
                if(this.name != '' && this.phone != ''){
                    this.$nuxt.$emit('newFriend', {
                        id: ++this.count,
                        name: this.name,
                        phone: this.phone
                    })
                    this.$nuxt.$emit('closeModal', false)
                    this.formReset()
                }
            },
            formReset(){
                this.name = ''
                this.phone = ''
            }
        }
    }
</script>