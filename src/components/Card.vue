<template>
    <!-- il contenitore delle card richiama una funzione che, al mouseenter, effettua una chiamata axios per recuperare il cast -->
    <div class="card" @mouseenter="(data_object.title != undefined) ? getMovieCast(id) : getTvCast(id)">
        <div class="img_box">
            <!-- la locandina, se mancante, viene sosituita da un placeholder che contiene il titolo del film o il nome della serie -->
            <img class="cover" :src="(data_object.poster_path != null) ? `https://image.tmdb.org/t/p/w342${data_object.poster_path}` : `https://via.placeholder.com/185x278/CECECE/000000/?text=${data_object.title || data_object.name}`" :alt="data_object.title || data_object.name">

            <div class="info_box">
                
                <p><strong>Titolo:</strong> {{data_object.title || data_object.name}}</p>

                <p><strong>Titolo originale:</strong> {{data_object.original_title || data_object.original_name}}</p>

                <p v-if="data_object.overview != ''" class="overview"><strong>Panoramica:</strong> {{data_object.overview}}</p>

                <p><strong>Cast:</strong><span> {{castMembers}}</span></p>

                <div class="score">
                    <strong>Voto: </strong>
                    <!-- per stampare le stelle piene o vuote effettuo un ciclo cinque volte e, se l'indice se l'iterazione è minore o uguale al voto arrotondato, stampa una stella piena -->
                    <span class="stars" v-for="(score, index) in 5" :key="index">
                        <i v-if="score <= roundedScore(data_object.vote_average)" class="fas fa-star"></i>
                        <i v-else-if="score > roundedScore(data_object.vote_average)" class="far fa-star"></i>
                    </span>
                </div>
                <!-- l'icona della bandiera è inserita richiamandola da un pacchetto -->
                <lang-flag class="flag" :iso="data_object.original_language" :squared="false" />
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import LangFlag from 'vue-lang-code-flags';

export default {
    name: 'Card',

    components: {
        LangFlag
    },

    props: {
        data_object: Object,
        id: Number,
        genres: Array
    },

    data() {
        return {
            scoreStars: [],
            castMembers: String,
            combinedID: Number
        }
    },

    methods: {
        roundedScore: function(num) {
            let roundedNum = Math.ceil(num / 2);

            return roundedNum
        },

        // le funzioni che effettuano la chiamata per il cast accettano un argomento che corrisponderà all'ID del film o della serie 
        getMovieCast: function(num) {
            axios.get('https://api.themoviedb.org/3/movie/' + num + '/credits', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    language: 'it-IT'
                }
            })
            .then(
                (response) => {
                    // svuoto il data contenente i membri del cast 
                    this.castMembers = '';
                    // effettuo un controllo sulla lunghezza del risultato della chiamata
                    // se contiene meno di 5 elementi
                    if(response.data.cast.length < 5) {
                        // effettuo un ciclo per tutti gli elementi    
                        for(let i = 0; i < response.data.cast.length; i++) {
                            let actor = response.data.cast[i];
                            let actorName = actor.name;
                            if(i < response.data.cast.length - 1){
                                this.castMembers += `${actorName},  `;
                            } else {
                                this.castMembers += `${actorName}.`
                            }
                        }

                    } else {
                        // altrimenti ne prendo solo 5
                        for(let i = 0; i < 5; i++) {
                            let actor = response.data.cast[i];
                            let actorName = actor.name;
                            if(i < 4){
                                this.castMembers += `${actorName},  `;
                            } else {
                                this.castMembers += `${actorName}.`
                            }
                        }

                    }
                    
                    return this.castMembers;
                }
            );
        },

        getTvCast: function(num) {
            axios.get('https://api.themoviedb.org/3/tv/' + num + '/credits', {
                params: {
                    api_key: '1d2064f2ac36d63f2852970763f815fc',
                    language: 'it-IT'
                }
            })
            .then(
                (response) => {
                    this.castMembers = '';
                    if(response.data.cast.length < 5) {

                        for(let i = 0; i < response.data.cast.length; i++) {
                            let actor = response.data.cast[i];
                            let actorName = actor.name;
                            if(i < response.data.cast.length - 1){
                                this.castMembers += `${actorName},  `;
                            } else {
                                this.castMembers += `${actorName}.`
                            }
                        }

                    } else {

                        for(let i = 0; i < 5; i++) {
                            let actor = response.data.cast[i];
                            let actorName = actor.name;
                            if(i < 4){
                                this.castMembers += `${actorName},  `;
                            } else {
                                this.castMembers += `${actorName}.`
                            }
                        }
                        
                    }
                    
                    return this.castMembers;
                }
            );
        },

        // getGenre: function(num) {
        //     let genre = '';

        //     this.genres.filter(Element => {
        //         if (Element.id == num){
        //             this.genre = Element.name;
        //             console.log(this.genre)
        //             return genre;
        //         }
        //     })
        // }

    },

    // computed: {
    //     getCombinedID: function() {
    //         return this.combinedID = this.id;
    //     }
    // },

    // watch: {
    //     combinedID: function(val) {
    //         console.log(val);
    //     }
    // }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/common.scss';

    .card {
        position: relative;
        width: 100%;
        height: 400px;
        overflow: hidden;
        box-shadow: 0px 0px 12px rgb(240, 253, 255);
        border-radius: 10px;
        overflow: hidden;

        .img_box {
            height: 100%;
        }

        .cover {
            display: block;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .info_box {
            opacity: 0;
            transition: opacity 0.2s;
        }

        &:hover {

            .info_box {
                position: absolute;
                top: 0;
                right: 0;
                bottom: 0;
                left: 0;
                opacity: 1;
                background-color: rgba(0, 0, 0, 85%);
                color: #fff;
                padding: 1rem;

                .stars {
                    color: rgb(255, 217, 0);
                }

                .flag {
                    position: absolute;
                    bottom: 1rem;
                    right: 1rem;
                }
                
                p:not(:first-child) {
                    margin-block: 1rem;
                }

                .overview {
                    height: 6rem;
                    overflow-y: auto;
                    border: 1px solid rgba(255, 255, 255, 50%);
                    box-shadow: 0px 0px 8px rgba(255, 255, 255, 50%);

                    &::-webkit-scrollbar {
                        width: 0.5rem;
                    }
                }
            }
        }

    }

</style>