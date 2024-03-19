<template>
    <div class="homoglyph">
      <div class="white-box">
        <h2>Calculate Homoglyph TypoSquatting possibilities</h2>
        <div v-if="!isLoading">
          <form @submit.prevent="submitForm">
            <input type="text" v-model="formData.original" placeholder="DNS without TLS">
            <label>
              Enable Visual Similarity
              <input type="checkbox" v-model="isVisualSimilarityChecked">
            </label>
            <input type="number" v-if="showVisualSimilarityScore" v-model="formData.visual_similarity_score" placeholder="Visual Similarity Score">
            <button type="submit">Submit</button>
          </form>
          <div v-if="result">
            <p>Result: {{ result }}</p>
          </div>
        </div>
        <div v-else>
          Loading...
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'Homoglyph',
    data() {
      return {
        items: [],
        isLoading: false,
        isVisualSimilarityChecked: false,
        formData: {
          original: '',
          visual_similarity: false,
          visual_similarity_score: null
        },
        result: null
      }
    },
    computed: {
      showVisualSimilarityScore() {
        return this.isVisualSimilarityChecked;
      }
    },
    methods: {
      submitForm() {
        this.isLoading = true;
  
        // Set visual_similarity based on isVisualSimilarityChecked
        this.formData.visual_similarity = this.isVisualSimilarityChecked;
  
        // Serialize the formData object into URL-encoded string
        const formDataString = new URLSearchParams(this.formData).toString();
  
        // Append the serialized data to the URL
        const url = 'http://localhost:8080/dns/homoglyph?' + formDataString;
  
        axios.get(url)
          .then(response => {
            // Handle successful response
            console.log(response.data);
            this.items = response.data; // Assign the received data to the items property
            this.isLoading = false;
            // Optionally, do something with response.data if needed
            this.result = response.data.join(', '); // Displaying the result under the submit button
          })
          .catch(error => {
            // Handle error
            console.error('Error:', error);
            this.isLoading = false;
          });
      }
    }
  }
  </script>
  
  <style scoped>
  .homoglyph {
    display: flex;
    justify-content: center;
    
  }
  
  .white-box {
    background-color: white;
    border: 1px solid #ccc;
    padding: 20px;
    border-radius: 5px;
    max-width: 600px;
    margin: 0 50px;
    
  }
  
  form {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  input, button {
    margin-bottom: 10px;
  }
  </style>
  