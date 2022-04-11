<template>
        <form id="uploadForm" @submit.prevent="uploadPhoto" class="d-flex flex-column justify-content-center">
              <div >
                <p>Description: 

                </p>
                 <textarea v-model="uploadPhoto" class="form-control mb-2 mr-sm-2" placeholder="Enter description and upload image" >
                </textarea>
                  
             </div>
             <div>
               <p>Photo Upload</p><input type="file" accept="image/*" @change="onChange" />
               <button class="btn btn-primary mb-2">Submit</button>
             </div>
            
                      
              </form>
          
</template>

<script>
export default {
        data() {
          return {
            csrf_token: ''
         }
},
	// data() {
	//   return {
	//       articles: [],
	//       searchTerm :''
	//   }
    //  },
     methods: {
 uploadPhoto(){
     	    let self= this;
          let uploadForm = document.getElementById('uploadForm');
          let form_data = new FormData(uploadForm);
           fetch("/api/upload", {
        method: 'POST',
        body: form_data,
        headers: {
          'X-CSRFToken': this.csrf_token
        }
              })
        .then(function (response) {
              return response.json();
              })
        .then(function (data) {
            // display a success message
            console.log(data);
        })
        .catch(function (error) {
            console.log(error);
          });
        },
        created() {
            this.getCsrfToken();
        },
        getCsrfToken() {
          let self = this;
          fetch('/api/csrf-token')
          .then((response) => response.json())
          .then((data) => {
          console.log(data);
          self.csrf_token = data.csrf_token;
 })
 }
     }   
           
     };
     
     
</script>