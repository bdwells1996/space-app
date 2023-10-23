

<script setup>
import feather from 'vue-icon'
</script>

<template>
    <div class="museum-highlight__inner" :class="partnerOrg">
        <!-- Display the available information for the highlight -->
        <div class="museum-highlight__inner__icon">
            <!-- Slot to add icon in dependant on page -->
            <slot name="icon" />
        </div>
        <img :src='newImage' alt="highlight-img" class="museum-highlight__inner__image" />
        <h2 class="museum-highlight__inner__title">{{ highlight.name }}</h2>
        <p class="museum-highlight__inner__text">{{ highlight.description }}</p>
        <p @click="toggleClass()" class="museum-highlight__inner__news-link" v-if="checkNews">See latest news <v-icon name="close"></v-icon></p>
        <p class="museum-highlight__inner__news-text" :style='{"display"  : (isOpen? "block" : "none")}' v-if="checkNews">{{ highlight.news.title }} {{ newsDate }}</p>
        <div class="museum-highlight__inner__actions">
            <button @click="getRandomPhoto()" class="museum-highlight__inner__refresh-img">Refresh image</button>
            <slot name="additional-actions" />
        </div>
    </div>
</template>

<script>

export default {
    name: 'MuseumHighlight',
    components: {

    },
    mixins: [
    ],
    props: ['highlight'],
    data() {
        return {
            // Data for unsplash api requests, normally in .env file but kept here for convenience
            accessKey: 'D0zcLo-_Wr_UnlPItu_MnS_Jbe8mdltBCjZdjcQlBuo',
            url: 'https://api.unsplash.com/photos/random',
            newImage: 'https://images.unsplash.com/photo-1505506874110-6a7a69069a08?auto=format&fit=crop&q=80&w=2893&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
            isOpen: false
        };
    },
    computed: {
        partnerOrg(){
            return this.highlight.isPartner ? 'museum-highlight__inner--partner' : '';
        },
        cardImage() {
            //checks if newimage has been set, were initially getting on from an api so in this case it will be true, faked with data
            return this.newImage ? this.newImage : this.highlight.image;
        },
        checkNews() {
            // returns a boolean value based on if a value is retrieved for news
            return !!this.highlight.news
        },
        checkNewsDate() {
            // returns a boolean value for if there's a date of the news only if an item has news
            return this.checkNews && !!this.highlight.news.date;
        },
        newsDate() {
            // Highlight's news item date, returns news date if there is one or an empty string
            return this.checkNews && this.checkNewsDate ? new Date(this.highlight.news.date).toLocaleDateString() : '';
        },
    },
    methods: {
        getRandomPhoto(){
            fetch(this.url + `?client_id=${this.accessKey}`).then((response) =>{
                return response.json()
            }).then((json)=> {
                this.newImage= json.urls.regular
            }).catch((err) => {
                console.log('error', err);
            })
        },
        toggleClass: function(){ 
         // Check value 
         if(this.isOpen){ 
            this.isOpen = false; 
         }else{ 
            this.isOpen = true; 
         } 
        }
    },
    created() {
    },
};
</script>

<style lang="scss" scoped>

.museum-highlight__inner {
    position: relative;
    box-shadow: 0px 3px 8px 0px rgba(0, 0, 0, 0.15);
    padding-bottom: 40px;
    border-radius: 6px;

    &--partner{
        background-color:   #e1e1ea;
    }

    &__icon{
        background-color: #fff;
        position: absolute;
        top: 9px;
        right: 9px;
        display: flex;
        align-items: center;
        border-radius: 4px;
        font-weight: bold;
        padding: 0 8px;

        &__image {
            width: 27px;
            height: auto;
        }

        &__text {
            font-size: 10px;
            font-weight: 800;
        }
    }

    &__title{
        font-weight: 600;
        margin-bottom: 12px;
        margin-left: 20px;
    }

    &__text{
        margin-left: 20px;
        margin-bottom: 20px;
    }

    &__image {
        height: 240px;
        width: 100%;
        object-fit: cover;
        border-radius: 6px 6px 0 0;
    }

    &__news-link{
        margin-left: 20px;
        margin-bottom: 20px;
        display: flex;
        text-decoration: none;
    }

    &__news-text{
        margin-left: 20px;
    }

    &__actions{
        display: flex;
    }

    &__refresh-img{
        background: #AAAACE;
        border: none;
        border-radius: 3px;
        font-size: 16px;
        font-family: 'Montserrat', sans-serif;
        appearance: none;
        margin-left: 20px;
        padding: 10px 26px;
        cursor: pointer;
        transition: background 200ms ease;

        &:hover{
            background: #8989b7;
        }
    }
}

</style>
