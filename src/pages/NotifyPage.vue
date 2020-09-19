<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <!-- wrapper -->
        <div class="notify notify--wrapper">

          <!-- title -->
          <div class="notify__title">
            <p>Notify app</p>
            <!-- svg -->
          </div>

          <div class="notify__content">
            <Preloader v-if="loading" :width="90" :height="90"/>
            <Notify
              v-if="!loading"
              :messages="messages"/>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import Notify from '@/components/Notify.vue';


//UI
import Preloader from '@/components/UI/Preloader.vue';

export default {
  components: {
    Preloader,
    Notify,
  },
  data() {
    return {
      loading: false,
      messages: []
    }
  },
  mounted() {
    this.getNotify()
  },
  methods: {
    getNotify () {
      this.loading = true
      axios
        .get('http://localhost/notify/notifyApi.php')
          .then(response => {
            let res = response.data.notify
            this.messages = res
          })
          .catch(error => {
            console.log(error)
          })
          .finally(() => (this.loading = false))
    }
  },
}
</script>

<style lang="scss" scoped>
  .container {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 90vh;

  }

  .notify {

    &--wrapper {
      width: 400px;
      background-color: #fff;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0 12px 22px 0 rgba(0,0,0,.1);
    }

    &__title {
      p {
        font-size: 24px;
      }
    }

    &__content {
      display: flex;
      align-items: center;
      flex-direction: column;
      min-height: 300px;

    }
  }

</style>