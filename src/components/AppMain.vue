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
        <section class="container form-container">
            <input class="form-control form-control-lg" type="text" placeholder="Cosa devi fare?" aria-label=".form-control-lg example">
            <input class="form-control form-control-lg" type="date" placeholder="Entro che giorno?" aria-label=".form-control-lg example">
            <select class="form-select form-select-lg" aria-label="Large select example">
                <option selected>Livello di Priorità</option>
                <option value="0">Super Urgentissimissimo</option>
                <option value="1">Urgente</option>
                <option value="2">Meh, quasi urgente</option>
                <option value="3">Cos'era più?</option>
            </select>
            <div class="d-grid gap-2">
                <button type="button" class="btn btn-info btn-lg">
                    Invia
                </button>
            </div>
        </section>
    </main>
</template>

<style scoped lang="scss">

</style>