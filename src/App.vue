<script setup>
import { computed, reactive, ref } from 'vue';

/***** 1.1  *****/
const count = ref(5);
const decrease = () => {
    count.value--;
}
const increase= () => {
    count.value++;
}
/***** 1.1  *****/

/***** 1.2  *****/
const articles = reactive([
    { nom: "Écouteurs sans fil", description: "Écouteurs bluetooth avec réduction de bruit", prix: 129.99, quantite: 0 },
    { nom: "Tasse à café", description: "Tasse en céramique 350ml", prix: 12.50, quantite: 0 },
    { nom: "Clavier mécanique", description: "Clavier gaming rétroéclairé", prix: 89.99, quantite: 0 },
    { nom: "Cahier premium", description: "Cahier A4 avec couverture rigide", prix: 15.99, quantite: 0 },
    { nom: "Sac à dos", description: "Sac à dos imperméable pour ordinateur", prix: 45.00, quantite: 0 },
    { nom: "Lampe de bureau", description: "Lampe LED ajustable", prix: 34.99, quantite: 0 },
    { nom: "Souris ergonomique", description: "Souris sans fil ergonomique", prix: 59.99, quantite: 0 },
    { nom: "Plante artificielle", description: "Plante décorative en pot", prix: 24.50, quantite: 0 },
    { nom: "Chargeur portable", description: "Batterie externe 10000mAh", prix: 29.99, quantite: 0 },
    { nom: "Support téléphone", description: "Support de bureau ajustable", prix: 19.99, quantite: 0 },
    { nom: "Enceinte portable", description: "Mini enceinte bluetooth étanche", prix: 49.99, quantite: 0 },
    { nom: "Agenda 2025", description: "Agenda journalier format A5", prix: 22.50, quantite: 0 },
    { nom: "Tapis de souris", description: "Tapis de souris XXL avec repose-poignet", prix: 27.99, quantite: 0 },
    { nom: "Câble USB", description: "Câble de charge tressé 2m", prix: 9.99, quantite: 0 },
    { nom: "Bloc-notes adhésif", description: "Pack de notes repositionnables", prix: 5.99, quantite: 0 },
    { nom: "Webcam HD", description: "Webcam 1080p avec micro intégré", prix: 79.99, quantite: 0 },
    { nom: "Pochette ordinateur", description: "Housse de protection 15 pouces", prix: 32.50, quantite: 0 },
    { nom: "Hub USB", description: "Hub 4 ports USB 3.0", prix: 25.99, quantite: 0 },
    { nom: "Ventilateur USB", description: "Mini ventilateur de bureau silencieux", prix: 18.50, quantite: 0 },
    { nom: "Support tablette", description: "Support ajustable pour tablette", prix: 28.99, quantite: 0 }
]);

const removeArticle = (article) => {
    if(article.quantite <= 0) {
        return;
    }
    article.quantite--;
} 
const addArticle = (article) => {
    article.quantite++;
}

const countArticles = computed(() => articles.reduce((p,c) => p + c.quantite,0))
const totalPrice = computed(() => { 
    let total = articles.reduce((p,c) => p + c.quantite * c.prix, 0);
    if(countArticles.value > 0) {
        total *= 0.95;
    }
    return total;
})
/***** 1.2  *****/



</script>

<template>
    <div id="root">
        <div class="panel">
            <h1>Ex 1.1</h1>
            <hr>
            <div>
                <p :class="['compteur', {
                    red: count < 3,
                    orange: count >=3 && count < 5,
                    blue: count >= 5&& count < 8,
                    green: count >= 8
                }]">{{ count }}</p>
                <div>
                    <button :disabled="count <= 0" @click="decrease">-</button>
                    <button :disabled="count >= 10" @click="increase">+</button>
                </div>
            </div>
        </div>
        <div class="panel">
            <h1>Exercice 1.2</h1>
            <hr>
            <table>
                <thead>
                    <tr>
                        <th>Nom</th>
                        <th>Description</th>
                        <th>Prix</th>
                        <th>Quantité</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in articles">
                        <td>{{ item.nom }}</td>
                        <td>{{ item.description }}</td>
                        <td>{{ item.prix }} €</td>
                        <td><button :disabled="item.quantite <= 0" @click="removeArticle(item)">-</button>{{ item.quantite  }}<button @click="addArticle(item)">+</button></td>
                    </tr>
                </tbody>
                <tfoot v-if="countArticles > 0">
                    <tr>
                        <td>Total</td>
                        <td></td>
                        <td>{{ totalPrice.toFixed(2) }}€</td>
                        <td>{{ countArticles }}</td>
                    </tr>
                </tfoot>
            </table>
        </div>
        <div class="panel"></div>
    </div>
</template>

<style scoped>
    #root {
        display: flex;
        flex-direction: column;
        gap: 10px;
        .compteur {
            font-size: 40px;
            font-weight: bold;
            &.red {color: red;}
            &.orange { color: orange;}
            &.blue { color: blue;}
            &.green { color: green;}
        }
    }
</style>