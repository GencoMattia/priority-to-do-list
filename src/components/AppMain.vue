<script>
export default {
    data() {
        return {
            coseDaFare: JSON.parse(localStorage.getItem('coseDaFare')) || [],
            nuovaAttivita: {
                nome: "",
                priorità: "",
                scadenza: "",
            },
            coseSvolte: JSON.parse(localStorage.getItem('coseSvolte')) || [],
        };
    },

    methods: {
        aggiungiAttivita() {
            if (this.nuovaAttivita.nome && this.nuovaAttivita.priorità && this.nuovaAttivita.scadenza) {
                this.coseDaFare.push({ ...this.nuovaAttivita }); 

                this.nuovaAttivita.nome = "";
                this.nuovaAttivita.priorità = "";
                this.nuovaAttivita.scadenza = "";
            } else {
                alert("Per favore, compila tutti i campi.");
            }
            this.salvaDatiInLocalStorage();
        },
        rimuoviAttivita() {
            if (this.coseDaFareOrdinate.length > 0) {
                this.coseSvolte.push(this.coseDaFareOrdinate[0]);

                this.coseDaFare.splice(this.coseDaFare.indexOf(this.coseDaFareOrdinate[0]), 1);
            }
            this.salvaDatiInLocalStorage();
        },
        salvaDatiInLocalStorage() {
            localStorage.setItem('coseDaFare', JSON.stringify(this.coseDaFare));
            localStorage.setItem('coseSvolte', JSON.stringify(this.coseSvolte));
        },
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

    mounted() {
        this.salvaDatiInLocalStorage();
    },
};
</script>

<template>
    <main>
        <section class="container">
            <div class="row">
                <div class="alert alert-danger m-0 d-flex justify-content-between" role="alert" v-if="coseDaFareOrdinate.length > 0">
                    <p class="m-0" v-if="coseDaFareOrdinate.length > 0">
                        {{ coseDaFareOrdinate[0].nome }}
                    </p>
                    <p class="m-0" v-else>
                        Bravissima, hai fatto tutto!
                    </p>
                    <button type="button" class="btn-close" aria-label="Close" @click="rimuoviAttivita" v-if="coseDaFareOrdinate.length > 0"></button>
                </div>
            </div>
        </section>
        <section class="container form-container">
            <input class="form-control form-control-lg" type="text" placeholder="Cosa devi fare?" aria-label=".form-control-lg example" v-model="nuovaAttivita.nome">
            <input class="form-control form-control-lg" type="date" placeholder="Entro che giorno?" aria-label=".form-control-lg example" v-model="nuovaAttivita.scadenza">
            <select class="form-select form-select-lg" aria-label="Large select example" v-model="nuovaAttivita.priorità">
                <option selected>Livello di Priorità</option>
                <option value="0">Super Urgentissimissimo</option>
                <option value="1">Urgente</option>
                <option value="2">Meh, quasi urgente</option>
                <option value="3">Cos'era più?</option>
            </select>
            <div class="d-grid gap-2">
                <button type="button" class="btn btn-info btn-lg" @click="aggiungiAttivita">
                    Invia
                </button>
            </div>
        </section>
    </main>
</template>

<style scoped lang="scss">

</style>