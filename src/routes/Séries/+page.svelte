<script>
    import { séries } from '$lib/Séries.js';
  
    
    let textoFiltro = $state('');
    let filtrados = $state(séries.slice());
  
    function filtrar() {
      filtrados = séries.filter((séries) => {
        const correspondeTitulo = séries.título.toLowerCase().includes(textoFiltro.toLowerCase());
       
        return correspondeTitulo;
      });
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
  
  </div>
  
  <div class="row g-4">
    {#each filtrados as séries}
      <div class="col-md-6 col-xl-3">
        <div class="card h-100">
          <div class="row g-0">
            <div class="col-3 col-sm-4">
              <img src={séries.imagem} class="img-fluid rounded-start" alt="capa do séries" />
            </div>
            <div class="col-sm-8">
              <div class="card-body">
                <h5 class="card-title">{séries.título}</h5>
                <h6 class="card-subtitle mb-2 text-body-secondary">{séries.ano}</h6>
              
                <p class="card-text">
                  {#each séries.gêneros as gênero}
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