<script>
    import { text } from "svelte/internal";

    async function getCards() {
        const response = await fetch(
            "https://db.ygoprodeck.com/api/v7/cardinfo.php?staple=yes"
        );
        const data = await response.json();
        if (response.ok) return data;
    }
</script>

{#await getCards()}
    <div
        style="height: 100vh; display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: colunm;
        flex-direction: column;"
    >
        <h1>Universidad Tecnológica Metropolitana</h1>
        <h2>
            <strong>Asignatura: </strong>Aplicaciones Web para Industria 4.0
        </h2>
        <h3><strong>Maestra: </strong> Ruth Bedsaida Martinez Dominguez</h3>
        <h3><strong>Alumno: </strong> Adrian Alejandro Mis Jimenez</h3>
        <h4><strong>Grado: </strong>5 <strong>Grupo: </strong>A</h4>
        <div class="spinner-border" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>
{:then cards}
    {#each cards.data as card}
        <div class="card mb-3 p-4" style="max-width: 100%; min-width: 460px;">
            <div class="row no-gutters">
                <div class="col-md-2">
                    <img
                        src={card.card_images[0].image_url}
                        class="card-img"
                        alt="..."
                    />
                    <div class="text-center m-2">
                        <button class="btn btn-success">
                            {card.card_prices[0].cardmarket_price} $
                        </button>
                    </div>
                </div>
                <div class="col-md-10">
                    <div class="card-body">
                        <h5 class="card-title">{card.name}</h5>
                        <p class="card-text">
                            {card.desc.length > 124
                                ? card.desc
                                      .split("")
                                      .splice(0, 124)
                                      .join("")
                                      .concat(" ...")
                                : card.desc}
                        </p>
                    </div>
                    <div class="card-footer">
                        <p class="card-text">
                            <small class="text-muted"
                                ><strong> type: </strong> {card.type}</small
                            >
                        </p>
                    </div>
                    <div class="card-footer">
                        <p class="card-text">
                            <small class="text-muted"
                                ><strong> franetype: </strong>
                                {card.frameType}</small
                            >
                        </p>
                    </div>
                    <div class="card-footer">
                        <p class="card-text">
                            <small class="text-muted"
                                ><strong> atk: </strong>
                                {card.atk || "none"} <strong> def: </strong>
                                {card.def || "none"}</small
                            >
                        </p>
                    </div>
                    <div class="card-footer">
                        <p class="card-text">
                            <small class="text-muted"
                                ><strong> level: </strong>
                                {card.level || "none"}</small
                            >
                        </p>
                    </div>
                    <div class="card-footer">
                        <p class="card-text">
                            <small class="text-muted"
                                ><strong> attribute: </strong>
                                {card.attribute || "none"}</small
                            >
                        </p>
                    </div>
                    <div class="card-footer">
                        <p class="card-text">
                            <small class="text-muted"
                                ><strong> race: </strong>
                                {card.race || "none"}</small
                            >
                        </p>
                    </div>
                    <div class="card-footer">
                        <p class="card-text">
                            <small class="text-muted"
                                ><strong> card sets: </strong>
                                {card.card_sets[0].set_name},  <br>
                                {card.card_sets[0].set_code} 
                                {card.card_sets[0].set_rarity} 
                                {card.card_sets[0].set_rarity_code}
                            </small>
                        </p>
                    </div>
                </div>
            </div>
        </div>
    {/each}
{/await}
