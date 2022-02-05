<template>
    <div id="myModal" class="modal">

    <!-- Modal content -->
    <div class="modal-content">
        <span @click="closeModal" class="close">&times;</span>
        <p>{{ text }}</p>
    </div>

</div>
</template>

<script>
export default {
    name: 'Message',
    props: {
        text: String
    },
    data(){
        return {

        }
    },
    computed: {

    },
    methods:{
        closeModal(){
            let modal = document.getElementById("myModal");
            modal.style.display = "none";
        }

    }
}
</script>

<style scoped>

p{
    font-size: 1.3rem;
}

.modal {
   /* Hidden by default */
    display: hidden;
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 4rem; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}
.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 60%;
  border-radius: 10px;
}


/* The Close Button */
.close {
  color: #aaaaaa;
  float: right;
  font-size: 2rem;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
</style>

