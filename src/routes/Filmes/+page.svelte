<script>
    import { filmes, idade } from '$lib/Filmes.js';
  
    let idadeSelecionadas = $state([]);
    let textoFiltro = $state('');
    let filtrados = $state(filmes.slice());
  
    function filtrar() {
      filtrados = filmes.filter((filme) => {
        const correspondeTitulo = filme.título.toLowerCase().includes(textoFiltro.toLowerCase());
        const correspondeGenero =
          gênerosSelecionados.length === 0 ||
          gênerosSelecionados.some((idade) => filme.gêneros.includes(idade));
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
    {#each idade as idade}
      <div class="col">
        <div class="form-check form-check-inline">
          <input
            oninput={filtrarGenero}
            class="form-check-input"
            type="checkbox"
            id={idade}
            value={idade}
          />
          <label class="form-check-label" for={idade}>{idade}</label>
        </div>
      </div>
    {/each}
  </div>
  
  <div class="row g-4">
    {#each filtrados as filme}
      <div class="col-md-6 col-xl-3">
        <div class="card h-100">
          <div class="row g-0">
            <div class="col-3 col-sm-4">
              <img src={filme.imagem} class="img-fluid rounded-start" alt="capa do filme" />
            </div>
            <div class="col-sm-8">
              <div class="card-body">
                <h5 class="card-title">{filme.título}</h5>
                <h6 class="card-subtitle mb-2 text-body-secondary">{filme.ano}</h6>
                <p class="card-text">{filme.sinopse}</p>
                <p class="card-text">
                  {#each filme.idade as idade}
                    <span class="badge text-bg-secondary mx-1">{idade}</span>
                  {/each}
                </p>
                <a 
                  href={filme.referência} 
                  class="btn btn-primary" 
                  target="_blank" 
                  rel="noopener noreferrer">
                  Assistir IMDB
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    {/each}
  </div>