<script>
    import * as d3 from "d3"
  
    export let title = ""
    // export let numbers = ""
  
    let data = [{nivel: 1}, {nivel: 2}, {nivel: 3}, {nivel: 4}, {nivel: 5}]
  
    /* 
      d3.scaleLinear() retorna una función,
      la guardamos en alturaCierre
      para poder usarla en el template
    */
   let alturaCierre = d3.scaleLinear()
   .domain([0, d3.max(data, d => d.nivel)])
   .range([0, 82]) // ajuste para la tapa del vaso
   
   /* 
     d3.scaleLinear() puede ser usada para
     asignar colores a los elementos,
     la guardamos en color
     para poder usarla en el template
   */
    let color =  d3.scaleLinear()
        .domain(d3.extent(data, d => d.nivel)) // extent retorna [min, max] de nivel
        .range(["#EADBC8", "#543310"])
  
  </script>
  
  <h3 class="headline">{title}</h3>
  
  <div class="cierres-container">
    {#each data as d}
    <div>
      <p class="number" style="color: {color(d.nivel)}">{d.nivel}</p>
      <div class="column-wrapper">
        <div class="column-coffe" style="height: {alturaCierre(d.nivel)}%; background-color: {color(d.nivel)}"></div>
        <img class="coffe" src="./images/coffe-cup-mask.svg" alt="">
      </div>
    </div>
    {/each}
  </div>
  
  <style>
    .cierres-container {
      display: flex;
      gap: 15px;
    }
    .column-wrapper {
      position: relative;
      width: 100px;
      height: 125px;
      /* background-color: #ccc;
      border: black 1px solid; */
    }
    .column-coffe {
      position: absolute;
      height: 50%;
      left: 10%;
      right: 10%;
      bottom: 0;
      /* width: 100%; */
      background-color: red;
    }
    .coffe {
      position: absolute;
      bottom: -3px;
      width: 100%;
    }
    .number {
      text-align: center;
      font-size: 20px;
      font-weight: 900;
      margin-bottom: 15px;
    }
    .anio {
      text-align: center;
      font-size: 14px;
      margin-top: 15px;
    }
  </style>