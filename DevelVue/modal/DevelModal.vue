<!-- <DevelModal modal="addOutpost">
    <div slot="header">
        <h2>Add Outpost</h2>
    </div>
    <div slot="bread">
        <form id="modal-form">
            <input type="text" v-model="outpost.name" placeholder="Outpost name">
            <select v-model="outpost.location_id">
                <option v-for='location in locations' :value="location._id" >{{ location.name }}</option>
            </select>
        </form>
    </div>
    <div slot="footer">
        <div class="form-control">
            <button type="button" @click="save()">save</button>
        </div>
    </div>
</DevelModal>
methods: {
    openModal() {
        this.mixinsToggleModal()
    },
    save () {
        const valid = this.mixinsToggleModal(this.meta_data.validation_rules.outpost, this.outpost)
        if (valid) {
            bus.$emit('save', 'outposts', this.outpost )
            this.outpost.name = ''
            this.outpost.location_id = ''
        }
    }
}, -->
<template lang="html">
    <div>
        <div :class="{ 'd-modal': true, 'd-modal-open': open}">
            <div class="d-modal-content">
                <header>
                    <span class="d-modal-close" @click="open = false">&times;</span>
                    <slot name="header"></slot>
                </header>
                <section class="d-modal-body">
                    <slot name="bread">

                    </slot>
                </section>
                <footer>
                    <slot name="footer"></slot>
                </footer>
            </div>
        </div>
    </div>
</template>

<script>
import { bus } from '../root'
export default {
    name: 'DevelModal',
    props: [ 'modal' ],
    data () {
        return {
            open: false
        }
    },
    created () {
        bus.$on('toggleModal', modal => {
            if ( this.modal !== undefined && modal === this.modal ) {
                this.open = !this.open
            }
        })
    }
}
</script>

<style lang="css">
    .d-modal {
        display: none;
        position: fixed; left: 0; top: 0; height: 100%; width: 100%; z-index: 1; overflow: auto;
        background: rgba(0,0,0,0.5);
    }
    .d-modal-open {
        display: block;
    }
    .d-modal-content {
        background: rgb(0, 119, 204);
        margin: 20% auto;
        width: 70%;
        box-shadow: 0 5px 8px 0 rgba(0,0,0,0.2), 0 7px 20px 0 rgba(0,0,0,0.2);
        animation-name: modal-open;
        animation-duration: .3s;
    }
    .d-modal-content header {
        padding: 15px;
    }
    .d-modal-body {
        padding: 10px 20px;
    }
    .d-modal-content footer {
        padding: 10px;
        text-align: center;
    }
    @keyframes modal-open {
        from { opacity: 0 }
        to { opacity: 1 }
    }
    .d-modal-close {
        color: #ccc;
        float: right;
        font-size: 30px;
    }
    .d-modal-close:hover, .d-modal-close:focus {
        cursor: pointer;
        color: rgb(0, 119, 204);
        text-decoration: none;
    }
</style>
