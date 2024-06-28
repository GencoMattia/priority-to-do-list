<script>
export default {
    data() {
        return {
            coseDaFare: [
                { 
                    nome: "Lavare i piatti", 
                    priorità: 3,
                    scadenza: "",
                },
                { 
                    nome: "Sistemare camera", 
                    priorità: 0,
                    scadenza: "",
                },
                { 
                    nome: "Ordinare i cassetti", 
                    priorità: 1,
                    scadenza: "", 
                },
                { 
                    nome: "Ordinare l'armadio", 
                    priorità: 1,
                    scadenza: "", 
                },
                { 
                    nome: "Svuotare le ultime scatole e sistemare la scrivania", 
                    priorità: 0,
                    scadenza: "", 
                },
                { 
                    nome: "Sistemare gli scaffali", 
                    priorità: 1,
                    scadenza: "",
                },
                { 
                    nome: "Buttare la spazzatura", 
                    priorità: 3,
                    scadenza: "", 
                },
                { 
                    nome: "Pulire la cucina", 
                    priorità: 2,
                    scadenza: "", 
                },
                { 
                    nome: "Pulire e sistemare il bagno", 
                    priorità: 1,
                    scadenza: "", 
                },
                { 
                    nome: "Passare l'antiscarafaggi", 
                    priorità: 0,
                    scadenza: "", 
                },
                { 
                    nome: "Pulire i davanzali delle finestre/i bordi della portafinestra da ragnatele e schifo", 
                    priorità: 0,
                    scadenza: "", 
                },
                { 
                    nome: "Mettere le trappole per scarafaggi sotto la cucina", 
                    priorità: 0,
                    scadenza: "", 
                },
                { 
                    nome: "Passare l'aspirapolvere sotto la cucina e buttare via le trappole vecchie", 
                    priorità: 0,
                    scadenza: "", 
                },
                { 
                    nome: "Fare la spesa", 
                    priorità: 2,
                    scadenza: "", 
                },
                { 
                    nome: "Pulire i mobili della cucina e mettere in ordine le cose della casa (utensili che erano già qui)", 
                    priorità: 3,
                    scadenza: "", 
                },
                { 
                    nome: "Togliere i vestiti dallo stendino e metterli a posto", 
                    priorità: 2,
                    scadenza: "", 
                },
            ]
        };
    },

    computed: {
        coseDaFareOrdinate() {
            return this.coseDaFare.slice().sort((a, b) => {
            if (a.scadenza && b.scadenza) {
                return new Date(a.scadenza) - new Date(b.scadenza);
            } else if (a.scadenza) {
                return -1;
            } else if (b.scadenza) {
                return 1;
            } else {
                return a.nome.localeCompare(b.nome);
            }

            return a.priorità - b.priorità;
            });
        },
    },
};
</script>

<template>
    <main>
        <section class="container">
            <div class="alert alert-danger" role="alert" v-if="coseDaFareOrdinate.length > 0">
                <p class="m-0">
                    {{ coseDaFareOrdinate[0].nome }}
                </p>
            </div>
        </section>
    </main>
</template>

<style scoped lang="scss">

</style>