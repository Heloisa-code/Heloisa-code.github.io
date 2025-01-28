<script>
    import { jogos, gêneros } from '$lib/Jogos.js';
  
    let gênerosSelecionados = $state([]);
    let textoFiltro = $state('');
    let filtrados = $state(jogos.slice());
  
    function filtrar() {
      filtrados = jogos.filter((jogos) => {
        const correspondeTitulo = filme.título.toLowerCase().includes(textoFiltro.toLowerCase());
        const correspondeGenero =
          gênerosSelecionados.length === 0 ||
          gênerosSelecionados.some((gênero) => jogos.gêneros.includes(gênero));
        return correspondeTitulo && correspondeGenero;
      });
    }
  
    function filtrarGenero(event) {
      if (event.target.checked) {
        gênerosSelecionados.push(event.target.value);
      } else {
        gênerosSelecionados.splice(gênerosSelecionados.indexOf(event.target.value), 1);
      }
      filtrar();
    }
  
    function filtrarTexto(event) {
      textoFiltro = event.target.value;
      filtrar();
    }
  </script>
  
  <div class="row align-items-center mb-3">
    <div class="col-4">
      <input
        class="form-control"
        placeholder="Filtrar..."
        oninput={filtrarTexto}
      />
    </div>
    {#each gêneros as gênero}
      <div class="col">
        <div class="form-check form-check-inline">
          <input
            oninput={filtrarGenero}
            class="form-check-input"
            type="checkbox"
            id={gênero}
            value={gênero}
          />
          <label class="form-check-label" for={gênero}>{gênero}</label>
        </div>
      </div>
    {/each}
  </div>
  
  <div class="row g-4">
    {#each filtrados as jogos}
      <div class="col-md-6 col-xl-3">
        <div class="card h-100">
          <div class="row g-0">
            <div class="col-3 col-sm-4">
              <img src={jogos.imagem} class="img-fluid rounded-start" alt="capa do jogos" />
            </div>
            <div class="col-sm-8">
              <div class="card-body">
                <h5 class="card-title">{jogos.título}</h5>
                <h6 class="card-subtitle mb-2 text-body-secondary">{jogos.ano}</h6>
                <p class="card-text">{jogos.sinopse}</p>
                <p class="card-text">
                  {#each jogos.gêneros as gênero}
                    <span class="badge text-bg-secondary mx-1">{gênero}</span>
                  {/each}
                </p>
              
              </div>
            </div>
          </div>
        </div>
      </div>
    {/each}
  </div>