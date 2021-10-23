<script>
  import viewmodel from './components/ViewModal.vue';
  import addElements from './components/AddElements.vue'
  export default {
    components: {
      viewmodel,
      addElements,
    },
    data() {
      return {
        snippetItems: [],
        isHidden: true,
        selectedItem: null,

      }
    },
    methods: {
      ItemView(id) {
        console.log(id)
      },
      snippetFetch() {
        fetch('http://0.0.0.0:5000/snippets').then(response => response.json()).then(data => {
          this.snippetItems = data;
          var len = this.snippetItems.length;
          console.log("my array", len)
        });
        this.isHidden = true;
      }
    },
    created() {
      this.snippetFetch();
      
    }
  }
</script>

<template>
  <div>
    <header>
      <div class="collapse bg-dark" id="navbarHeader">
        <div class="container">
          <div class="row">
            <div class="col-sm-8 col-md-7 py-4">
              <h4 class="text-white">About</h4>
              <p class="text-muted">Add some information about the album below, the author, or any other background
                context. Make it a few sentences long so folks can pick up some informative tidbits. Then, link them off
                to some social networking sites or contact information.</p>
            </div>
            <div class="col-sm-4 offset-md-1 py-4">
              <h4 class="text-white">Contact</h4>
              <ul class="list-unstyled">
                <li>
                  <a href="#" class="text-white">Email me</a>
                </li>
              </ul>
            </div>
          </div>


        </div>
      </div>
      <div class="navbar navbar-dark bg-dark shadow-sm">
        <div class="container">
          <a href="#" class="navbar-brand d-flex align-items-center">
            <ion-icon name="code-slash-outline"></ion-icon>
            <strong>Codes</strong>
          </a>
          <button class="btn" @click="isHidden = false"><i class="fa fa-plus-circle"></i>Add Code</button>
          <!-- <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarHeader" aria-controls="navbarHeader" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button> -->
        </div>
      </div>
    </header>
    <section class="code-list code-demo pt-5 pb-5">
      <add-elements @created="snippetFetch" v-if="!isHidden"></add-elements>
      <div class="container" v-if="!selectedItem">
        <h3 class="text-center">Source Codes</h3>
        <div class="row">
          <div class="col-md-6" v-for="item in snippetItems">
            <div class="list-snippet">
              <div class="source-desc">
                <h5>{{ item.codename }}</h5>
                <p>{{ item.codelanguage }}</p>
              </div>

              <div class="source-code">
                <!-- <div class="source-top"></div> -->
                <button class="btn btn-primary" @click="selectedItem = item">View Code</button>
                <!--                                 <a href="#" class="btn btn-primary" @click="Itemview(item.id)" id="item.codename">View Code</a> -->
                <!-- <span class="copy-item">View Code</span> -->
              </div>

            </div>
          </div>
        </div>
      </div>
      <div class="container" v-if="selectedItem">
        <viewmodel :compitem="selectedItem"></viewmodel>
      </div>
    </section>
  </div>

</template>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    /* text-align: center; */
    color: #2c3e50;
    /* margin-top: 60px; */
  }

  .list-snippet {
    display: flex;
    align-items: center;
    justify-content: space-around;
    background: #f8f9fa;
    border-radius: 10px;
    padding: 10px 20px;
    box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
    margin-top: 50px;
  }

  .list-snippet p {
    margin: 0;
  }

  /* code editor */
  input[type="text"] {
    margin-bottom: 1rem;
  }

  .text-area {
    padding: 10px;
    background-color: #f8f9fa;
    border-radius: 5px;
    margin-top: 1rem;
  }

  .navbar .btn {
    color: white;
    display: flex;
    align-items: center;
  }

  .navbar .btn i {
    font-size: 25px;
    margin-right: 5px;
  }
  .footer-main{
    background-color: #212529;
    position: fixed;
    bottom: 0;
    width: 100%;
    z-index: 999;
}

</style>