<template>
    <transition :enter-active-class="enterActiveClass" :leave-active-class="leaveActiveClass" @before-enter="beforeEnter" @after-enter="afterEnter" @before-leave="beforeLeave">
        <div class="toast" :class="['toast-'+type]" :style="{backgroundColor:toastBackgroundColor}" v-if="show">
            <button class="toast-close-button" role="button" @click="hideToastr" v-if="closeButton">×</button>
            <div class="toast-progress" v-if="progressBar" :style="'width: ' + progress.percent + '%'"></div>
            <div class="toast-icon">
            <img :src="iconSrc"/>
            </div>
            <div class="toast-message">{{message}}</div>
        </div>
    </transition>
</template>

<script>

export default {
    name: 'Toastr',
    data: () => {
        return {
            show: false
        }
    },
    props: {
        type: {
            type: String,
            default: 'success'
        },
        position: {
            type: String,
            default: 'bottom right'
        },
        message: {
            type: String
        },
        closeButton: {
            type: Boolean,
            default: true
        },
        icon: {
            type: String
        },
        timeOut: {
            default: '1500'
        },
        showMethod: {
            type: String,
            default: 'fadeIn'
        },
        hideMethod: {
            type: String,
            default: 'fadeOut'
        },
        showDuration: {
            default: '2000'
        },
        hideDuration: {
            default: '1000'
        },
        delay: {
            default: '0'
        }
    },
    beforeMount() {
        let toastContainer = document.querySelector(`.bulma-toastr-container.toast-${this.positionClass}`)
        if (!toastContainer) {
            toastContainer = document.createElement('div')

            toastContainer.classList.add('bulma-toastr-container')
            toastContainer.classList.add(`toast-${this.positionClass}`)
            document.body.appendChild(toastContainer)
        }
        toastContainer.appendChild(this.$el)
    },
    mounted() {
        setTimeout(() => this.showToastr(), this.delay)
    },
    computed: {
        positionClass() {
            return this.position.split(' ').join('-')
        },
        enterActiveClass() {
            return 'animated ' + this.showMethod
        },
        leaveActiveClass() {
            return 'animated ' + this.hideMethod
        },
        
    },
    methods: {
        showToastr() {
            this.show = true
            this.sto = setTimeout(() => this.hideToastr(), this.timeOut)
        },
        hideToastr() {
            clearTimeout(this.sto)
            clearTimeout(this.progress.intervalId)
            this.show = false
        },
        beforeEnter(el) {
            el.style.animationDuration = this.showDuration + 'ms'
        },
        afterEnter(el) {
            this.$el.classList.add('animated')
            this.$el.classList.add(this.showMethod)
        },
        beforeLeave(el) {
            el.style.animationDuration = this.hideDuration + 'ms'
        }
    }
}

</script>

