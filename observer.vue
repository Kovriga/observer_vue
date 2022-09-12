<template class="observer">

</template>

<script lang="ts">
   import Vue from 'vue';
   import Component from 'vue-class-component';

   import 'intersection-observer';

   @Component({
       props: {
           options: {
               required: false,
           },
       },
    })
   export default class Observer extends Vue {
       observer: any = null;
       options: any;

       mounted() {
           const options = this.options || {};
           this.observer = new IntersectionObserver(([entry]) => {
               if (entry && entry.isIntersecting) {
                   this.$emit('intersect');
               }
           }, options);

           this.observer.observe(this.$el);
       }

       destroyed() {
           this.observer.disconnect();
       }
    }
</script>
