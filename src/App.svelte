<script>
  import cero from "/images/cero_rueda.svg?raw";
  import una from "/images/una_rueda.svg?raw";
  import dos from "/images/dos_ruedas.svg?raw";
  import tres from "/images/tres_ruedas.svg?raw";
  import cuatro from "/images/cuatro_ruedas.svg?raw";
  import verano from "/images/sol2.svg"
  import invierno from "/images/nieve.svg"
  import otonio from "/images/hoja.svg"
  import primavera from "/images/flor.svg"

  import * as d3 from "d3";

  const viajes = [
    {"ID":1,"Monto":850,"Region":"Europa","Estacion":"Verano","Mes":7,"Satisfaccion":5,"Acompaniantes":2},
    {"ID":2,"Monto":430,"Region":"Asia","Estacion":"Invierno","Mes":1,"Satisfaccion":3,"Acompaniantes":0},
    {"ID":3,"Monto":600,"Region":"América","Estacion":"Primavera","Mes":11,"Satisfaccion":4,"Acompaniantes":1},
    {"ID":4,"Monto":1250,"Region":"Oceanía","Estacion":"Otoño","Mes":8,"Satisfaccion":5,"Acompaniantes":4},
    {"ID":5,"Monto":300,"Region":"África","Estacion":"Verano","Mes":4,"Satisfaccion":2,"Acompaniantes":0},
    {"ID":6,"Monto":980,"Region":"Europa","Estacion":"Primavera","Mes":1,"Satisfaccion":4,"Acompaniantes":1},
    {"ID":7,"Monto":560,"Region":"Asia","Estacion":"Otoño","Mes":12,"Satisfaccion":3,"Acompaniantes":1},
    {"ID":8,"Monto":750,"Region":"América","Estacion":"Invierno","Mes":9,"Satisfaccion":5,"Acompaniantes":2},
    {"ID":9,"Monto":640,"Region":"Oceanía","Estacion":"Verano","Mes":5,"Satisfaccion":4,"Acompaniantes":1},
    {"ID":10,"Monto":1050,"Region":"África","Estacion":"Primavera","Mes":2,"Satisfaccion":5,"Acompaniantes":4},
    {"ID":11,"Monto":200,"Region":"Europa","Estacion":"Otoño","Mes":6,"Satisfaccion":1,"Acompaniantes":0},
    {"ID":12,"Monto":370,"Region":"Asia","Estacion":"Verano","Mes":10,"Satisfaccion":2,"Acompaniantes":1},
    {"ID":13,"Monto":820,"Region":"América","Estacion":"Primavera","Mes":3,"Satisfaccion":5,"Acompaniantes":3},
    {"ID":14,"Monto":450,"Region":"Oceanía","Estacion":"Invierno","Mes":4,"Satisfaccion":3,"Acompaniantes":1},
    {"ID":15,"Monto":690,"Region":"África","Estacion":"Otoño","Mes":7,"Satisfaccion":4,"Acompaniantes":2},
    {"ID":16,"Monto":730,"Region":"Europa","Estacion":"Invierno","Mes":9,"Satisfaccion":2,"Acompaniantes":0},
    {"ID":17,"Monto":950,"Region":"Asia","Estacion":"Primavera","Mes":6,"Satisfaccion":5,"Acompaniantes":4},
    {"ID":18,"Monto":960,"Region":"América","Estacion":"Verano","Mes":8,"Satisfaccion":3,"Acompaniantes":1},
    {"ID":19,"Monto":1210,"Region":"Oceanía","Estacion":"Primavera","Mes":10,"Satisfaccion":4,"Acompaniantes":2},
    {"ID":20,"Monto":490,"Region":"África","Estacion":"Invierno","Mes":5,"Satisfaccion":3,"Acompaniantes":1}
  ];

  function colorContinente(region) {
    const colores = {
      Europa: "#852EFF",
      Asia: "#FFC71D",
      América: "#127E16",
      Oceanía: "#36BCFF",
      África: "#FF49D7"
    };
    return colores[region] || "#696A70";
  }

  function anchoValija(monto) {
    if (monto < 550) return 151.2;
    if (monto <= 900) return 170.1;
    return 189;
  }

  function altoValija(monto) {
    if (monto < 550) return 235.2;
    if (monto <= 900) return 264.6;
    return 294;
  }

  function calcularLineaSatisfaccion(nivel, monto) {
  let total;
  if (monto < 550) {
    total = 110.488;
  } else if (monto <= 900) {
    total = 124.299;
  } else {
    total = 138.11;
  }
  const visible = (nivel / 5) * total;
  return { visible, total };
}

  // Coordenadas Y de las líneas, de abajo (nivel 1) a arriba (nivel 5)
  const nivelesY = [204, 180, 155, 132, 111];

  const iconosEstacion = {
  Verano: verano,
  Invierno: invierno,
  Otoño: otonio,
  Primavera:primavera
};
  
</script>

<main>
  <div class="headline">
    <h2>Visualización de Valijas</h2>
  </div>
  <div class= "header">
  <img src="/images/Referencias.svg" width="850" justify-content= "center" align-items= "center"
  alt="explicacion"/>
  </div>
  <div class="container" style="display: flex; flex-wrap: wrap; max-width: 900px; gap: 20px;">
    {#each viajes as viaje}
    <div class="valija">
      {#if viaje.Acompaniantes === 0}
          <svg width="{anchoValija(viaje.Monto)}" height="{altoValija(viaje.Monto)}" viewBox="0 0 189 286" fill="none" xmlns="http://www.w3.org/2000/svg">
            <image
              href="{iconosEstacion[viaje.Estacion]}"
              x="120"
              y="210"
              width="40"
              height="40"
            />
            <g filter="url(#filter0_d_13_88)">
            <rect x="73.5" y="2.5" width="46" height="39" rx="7.5" stroke="black" stroke-width="5" shape-rendering="crispEdges"/>
            </g>
            <g filter="url(#filter1_d_13_88)">
            <rect id= "relleno" x="4" y="35" width="181" height="243" rx="25" fill="{colorContinente(viaje.Region)}" fill-opacity="0.30" shape-rendering="crispEdges"/>
            <rect id="borde" x="9" y="40" width="171" height="233" rx="20" stroke="{colorContinente(viaje.Region)}" stroke-width="10" shape-rendering="crispEdges"/>
            </g>
            <path id= "cierre" d="M35.0871 88.8847L34.4472 226.993" stroke="#B7A6A6" stroke-width="2"/>
            {#each nivelesY as y, i}
              <line
                x1="30" y1={y}
                x2="40" y2={y}
                stroke={i < viaje.Satisfaccion ? "#000000" : "#B7A6A6"}
                stroke-width="2"
              />
            {/each}
            <!-- <path d="M34.4472 226.993 L35.0871 88.8847" stroke="black" stroke-width="2" stroke-dasharray="{dashLength}, {totalLength - dashLength}" stroke-dashoffset="0"/> -->
            <g filter="url(#filter2_d_13_88)">
            <rect width="48.3648" height="62.1777" rx="3" transform="matrix(0.974669 -0.223652 0.231685 0.972791 98.2067 47.0853)" fill="#404040"/>
            </g>
            <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 129 48)" fill="white"/>
            <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 134 67.1497)" fill="white"/>

            <g filter="url(#filter3_d_13_88)">
            <path d="M138 37.5C138 37.5 132.019 22.3911 126.5 19.5C121.527 16.895 118.486 16.7363 113 18.5C107.486 20.2728 106 22 104 27C101.047 34.383 105.5 45.5 105.5 45.5" stroke="black" stroke-width="2"/>
            </g>
            <ellipse cx="106.08" cy="45.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 106.08 45.2264)" fill="black"/>
            <ellipse cx="138.08" cy="38.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 138.08 38.2264)" fill="black"/>
            <defs>
            <filter id="filter0_d_13_88" x="67" y="0" width="59" height="52" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
            <feFlood flood-opacity="0" result="BackgroundImageFix"/>
            <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
            <feOffset dy="4"/>
            <feGaussianBlur stdDeviation="2"/>
            <feComposite in2="hardAlpha" operator="out"/>
            <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
            <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_88"/>
            <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_88" result="shape"/>
            </filter>
            <filter id="filter1_d_13_88" x="0" y="35" width="189" height="251" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
            <feFlood flood-opacity="0" result="BackgroundImageFix"/>
            <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
            <feOffset dy="4"/>
            <feGaussianBlur stdDeviation="2"/>
            <feComposite in2="hardAlpha" operator="out"/>
            <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
            <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_88"/>
            <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_88" result="shape"/>
            </filter>
            <filter id="filter2_d_13_88" x="94.8196" y="36.8626" width="68.3195" height="78.1145" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
            <feFlood flood-opacity="0" result="BackgroundImageFix"/>
            <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
            <feOffset dy="4"/>
            <feGaussianBlur stdDeviation="2"/>
            <feComposite in2="hardAlpha" operator="out"/>
            <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
            <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_88"/>
            <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_88" result="shape"/>
            </filter>
            <filter id="filter3_d_13_88" x="97.9885" y="16.3328" width="44.9411" height="37.5385" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
            <feFlood flood-opacity="0" result="BackgroundImageFix"/>
            <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
            <feOffset dy="4"/>
            <feGaussianBlur stdDeviation="2"/>
            <feComposite in2="hardAlpha" operator="out"/>
            <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
            <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_88"/>
            <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_88" result="shape"/>
            </filter>
            </defs>
            <text
              x="142"
              y="74"
              text-anchor="middle"
              font-size="20"
              fill="black"
              font-family="sans-serif"
              transform="rotate(-15 90 75)"
            >
              {viaje.Mes.toString().padStart(2, '0')[0]}
            </text>

            <text
              x="142"
              y="94.5"
              text-anchor="middle"
              font-size="20"
              fill="black"
              font-family="sans-serif"
              transform="rotate(-15 90 75)"
            >
              {viaje.Mes.toString().padStart(2, '0')[1]}
            </text>

            </svg>
            {:else if viaje.Acompaniantes === 1}
            <svg width="{anchoValija(viaje.Monto)}" height="{altoValija(viaje.Monto)}" viewBox="0 0 189 294" fill="none" xmlns="http://www.w3.org/2000/svg">
              <image
              href="{iconosEstacion[viaje.Estacion]}"
              x="120"
              y="210"
              width="40"
              height="40"
              />
              <circle cx="94" cy="285" r="9" fill="#404040"/>
              <circle cx="94" cy="285" r="5" fill="white"/>
              <g filter="url(#filter0_d_13_89)">
              <rect x="73.5" y="2.5" width="46" height="39" rx="7.5" stroke="black" stroke-width="5" shape-rendering="crispEdges"/>
              </g>
              <g filter="url(#filter1_d_13_89)">
              <rect x="4" y="35" width="181" height="243" rx="25" fill="{colorContinente(viaje.Region)}" fill-opacity="0.30" shape-rendering="crispEdges"/>
              <rect x="9" y="40" width="171" height="233" rx="20" stroke="{colorContinente(viaje.Region)}" stroke-width="10" shape-rendering="crispEdges"/>
              </g>
              <path id= "cierre" d="M35.0871 88.8847L34.4472 226.993" stroke="#B7A6A6" stroke-width="2"/>
              {#each nivelesY as y, i}
                <line
                  x1="30" y1={y}
                  x2="40" y2={y}
                  stroke={i < viaje.Satisfaccion ? "#000000" : "#B7A6A6"}
                  stroke-width="2"
                />
              {/each}
              <g filter="url(#filter2_d_13_89)">
              <rect width="48.3648" height="62.1777" rx="3" transform="matrix(0.974669 -0.223652 0.231685 0.972791 98.2067 47.0853)" fill="#404040"/>
              </g>
              <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 129 48)" fill="white"/>
              <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 134 67.1497)" fill="white"/>
              
              <g filter="url(#filter3_d_13_89)">
              <path d="M138 37.5C138 37.5 132.019 22.3911 126.5 19.5C121.527 16.895 118.486 16.7363 113 18.5C107.486 20.2728 106 22 104 27C101.047 34.383 105.5 45.5 105.5 45.5" stroke="black" stroke-width="2"/>
              </g>
              <ellipse cx="106.08" cy="45.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 106.08 45.2264)" fill="black"/>
              <ellipse cx="138.08" cy="38.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 138.08 38.2264)" fill="black"/>
              <defs>
              <filter id="filter0_d_13_89" x="67" y="0" width="59" height="52" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_89"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_89" result="shape"/>
              </filter>
              <filter id="filter1_d_13_89" x="0" y="35" width="189" height="251" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_89"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_89" result="shape"/>
              </filter>
              <filter id="filter2_d_13_89" x="94.8196" y="36.8626" width="68.3195" height="78.1145" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_89"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_89" result="shape"/>
              </filter>
              <filter id="filter3_d_13_89" x="97.9885" y="16.3328" width="44.9411" height="37.5385" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_89"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_89" result="shape"/>
              </filter>
              </defs>
              <text
              x="142"
              y="74"
              text-anchor="middle"
              font-size="20"
              fill="black"
              font-family="sans-serif"
              transform="rotate(-15 90 75)"
            >
              {viaje.Mes.toString().padStart(2, '0')[0]}
            </text>

            <text
              x="142"
              y="94.5"
              text-anchor="middle"
              font-size="20"
              fill="black"
              font-family="sans-serif"
              transform="rotate(-15 90 75)"
            >
              {viaje.Mes.toString().padStart(2, '0')[1]}
            </text>

              </svg>
            {:else if  viaje.Acompaniantes === 2}
            <svg width="{anchoValija(viaje.Monto)}" height="{altoValija(viaje.Monto)}" viewBox="0 0 189 294" fill="none" xmlns="http://www.w3.org/2000/svg">
              <image
              href="{iconosEstacion[viaje.Estacion]}"
              x="120"
              y="210"
              width="40"
              height="40"
              />
              <circle cx="154" cy="285" r="9" fill="#404040"/>
              <circle cx="154" cy="285" r="5" fill="white"/>
              <circle cx="41" cy="285" r="9" fill="#404040"/>
              <circle cx="41" cy="285" r="5" fill="white"/>
              <g filter="url(#filter0_d_25_2)">
              <rect x="73.5" y="2.5" width="46" height="39" rx="7.5" stroke="black" stroke-width="5" shape-rendering="crispEdges"/>
              </g>
              <g filter="url(#filter1_d_25_2)">
              <rect x="4" y="35" width="181" height="243" rx="25" fill="{colorContinente(viaje.Region)}" fill-opacity="0.30" shape-rendering="crispEdges"/>
              <rect x="9" y="40" width="171" height="233" rx="20" stroke="{colorContinente(viaje.Region)}" stroke-width="10" shape-rendering="crispEdges"/>
              </g>
              <path id = "cierre" d="M35.0871 88.8847L34.4472 226.993" stroke="#B7A6A6" stroke-width="2"/>
              {#each nivelesY as y, i}
                <line
                  x1="30" y1={y}
                  x2="40" y2={y}
                  stroke={i < viaje.Satisfaccion ? "#000000" : "#B7A6A6"}
                  stroke-width="2"
                />
              {/each}
              <g filter="url(#filter2_d_25_2)">
              <rect width="48.3648" height="62.1777" rx="3" transform="matrix(0.974669 -0.223652 0.231685 0.972791 98.2067 47.0853)" fill="#404040"/>
              </g>
              <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 129 48)" fill="white"/>
              <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 134 67.1497)" fill="white"/>
              
              <g filter="url(#filter3_d_25_2)">
              <path d="M138 37.5C138 37.5 132.019 22.3911 126.5 19.5C121.527 16.895 118.486 16.7363 113 18.5C107.486 20.2728 106 22 104 27C101.047 34.383 105.5 45.5 105.5 45.5" stroke="black" stroke-width="2"/>
              </g>
              <ellipse cx="106.08" cy="45.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 106.08 45.2264)" fill="black"/>
              <ellipse cx="138.08" cy="38.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 138.08 38.2264)" fill="black"/>
              <defs>
              <filter id="filter0_d_25_2" x="67" y="0" width="59" height="52" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_25_2"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_25_2" result="shape"/>
              </filter>
              <filter id="filter1_d_25_2" x="0" y="35" width="189" height="251" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_25_2"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_25_2" result="shape"/>
              </filter>
              <filter id="filter2_d_25_2" x="94.8196" y="36.8626" width="68.3195" height="78.1145" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_25_2"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_25_2" result="shape"/>
              </filter>
              <filter id="filter3_d_25_2" x="97.9884" y="16.3328" width="44.9411" height="37.5385" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
              <feFlood flood-opacity="0" result="BackgroundImageFix"/>
              <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
              <feOffset dy="4"/>
              <feGaussianBlur stdDeviation="2"/>
              <feComposite in2="hardAlpha" operator="out"/>
              <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
              <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_25_2"/>
              <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_25_2" result="shape"/>
              </filter>
              </defs>
              <text
                x="142"
                y="75"
                text-anchor="middle"
                font-size="21"
                fill="black"
                font-family="sans-serif"
                transform="rotate(-15 90 75)"
              >
                {viaje.Mes.toString().padStart(2, '0')[0]}
            </text>

            <text
              x="142"
              y="95"
              text-anchor="middle"
              font-size="21"
              fill="black"
              font-family="sans-serif"
              transform="rotate(-15 90 75)"
            >
              {viaje.Mes.toString().padStart(2, '0')[1]}
            </text>

              </svg>
              {:else if  viaje.Acompaniantes === 3}
              <svg width="{anchoValija(viaje.Monto)}" height="{altoValija(viaje.Monto)}" viewBox="0 0 189 294" fill="none" xmlns="http://www.w3.org/2000/svg">
                <image
                href="{iconosEstacion[viaje.Estacion]}"
                x="120"
                y="210"
                width="40"
                height="40"
                />
                <circle cx="153" cy="285" r="9" fill="#404040"/>
                <circle cx="153" cy="285" r="5" fill="white"/>
                <circle cx="95" cy="285" r="9" fill="#404040"/>
                <circle cx="95" cy="285" r="5" fill="white"/>
                <circle cx="37" cy="285" r="9" fill="#404040"/>
                <circle cx="37" cy="285" r="5" fill="white"/>
                <circle cx="95" cy="285" r="5" fill="white"/>
                <g filter="url(#filter0_d_13_91)">
                <rect x="73.5" y="2.5" width="46" height="39" rx="7.5" stroke="black" stroke-width="5" shape-rendering="crispEdges"/>
                </g>
                <g filter="url(#filter1_d_13_91)">
                <rect x="4" y="35" width="181" height="243" rx="25" fill="{colorContinente(viaje.Region)}" fill-opacity="0.30" shape-rendering="crispEdges"/>
                <rect x="9" y="40" width="171" height="233" rx="20" stroke="{colorContinente(viaje.Region)}" stroke-width="10" shape-rendering="crispEdges"/>
                </g>
                <path id= "cierre" d="M35.0871 88.8847L34.4472 226.993" stroke="#B7A6A6" stroke-width="2"/>
                {#each nivelesY as y, i}
                <line
                  x1="30" y1={y}
                  x2="40" y2={y}
                  stroke={i < viaje.Satisfaccion ? "#000000" : "#B7A6A6"}
                  stroke-width="2"
                />
                {/each}
                <g filter="url(#filter2_d_13_91)">
                <rect width="48.3648" height="62.1777" rx="3" transform="matrix(0.974669 -0.223652 0.231685 0.972791 98.2067 47.0853)" fill="#404040"/>
                </g>
                <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 129 48)" fill="white"/>
                <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 134 67.1497)" fill="white"/>
                
                <g filter="url(#filter3_d_13_91)">
                <path d="M138 37.5C138 37.5 132.019 22.3911 126.5 19.5C121.527 16.895 118.486 16.7363 113 18.5C107.486 20.2728 106 22 104 27C101.047 34.383 105.5 45.5 105.5 45.5" stroke="black" stroke-width="2"/>
                </g>
                <ellipse cx="106.08" cy="45.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 106.08 45.2264)" fill="black"/>
                <ellipse cx="138.08" cy="38.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 138.08 38.2264)" fill="black"/>
                <defs>
                <filter id="filter0_d_13_91" x="67" y="0" width="59" height="52" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_91"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_91" result="shape"/>
                </filter>
                <filter id="filter1_d_13_91" x="0" y="35" width="189" height="251" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_91"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_91" result="shape"/>
                </filter>
                <filter id="filter2_d_13_91" x="94.8196" y="36.8626" width="68.3195" height="78.1145" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_91"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_91" result="shape"/>
                </filter>
                <filter id="filter3_d_13_91" x="97.9884" y="16.3328" width="44.9411" height="37.5385" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_91"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_91" result="shape"/>
                </filter>
                </defs>
                <text
                  x="142"
                  y="74"
                  text-anchor="middle"
                  font-size="20"
                  fill="black"
                  font-family="sans-serif"
                  transform="rotate(-15 90 75)"
                >
                  {viaje.Mes.toString().padStart(2, '0')[0]}
                </text>

                <text
                  x="142"
                  y="94.5"
                  text-anchor="middle"
                  font-size="20"
                  fill="black"
                  font-family="sans-serif"
                  transform="rotate(-15 90 75)"
                >
                  {viaje.Mes.toString().padStart(2, '0')[1]}
                </text>

                </svg>
              {:else if  viaje.Acompaniantes === 4} 
              <svg width="{anchoValija(viaje.Monto)}" height="{altoValija(viaje.Monto)}" viewBox="0 0 189 294" fill="none" xmlns="http://www.w3.org/2000/svg">
                <image
                href="{iconosEstacion[viaje.Estacion]}"
                x="120"
                y="210"
                width="40"
                height="40"
                />
                <circle cx="34" cy="285" r="9" fill="#404040"/>
                <circle cx="155" cy="285" r="9" fill="#404040"/>
                <circle cx="132" cy="285" r="9" fill="#404040"/>
                <circle cx="57" cy="285" r="9" fill="#404040"/>
                <circle cx="34" cy="285" r="5" fill="white"/>
                <circle cx="57" cy="285" r="5" fill="white"/>
                <circle cx="132" cy="285" r="5" fill="white"/>
                <circle cx="155" cy="285" r="5" fill="white"/>
                <g filter="url(#filter0_d_13_92)">
                <rect x="73.5" y="2.5" width="46" height="39" rx="7.5" stroke="black" stroke-width="5" shape-rendering="crispEdges"/>
                </g>
                <g filter="url(#filter1_d_13_92)">
                <rect x="4" y="35" width="181" height="243" rx="25" fill="{colorContinente(viaje.Region)}" fill-opacity="0.30" shape-rendering="crispEdges"/>
                <rect x="9" y="40" width="171" height="233" rx="20" stroke="{colorContinente(viaje.Region)}" stroke-width="10" shape-rendering="crispEdges"/>
                </g>
                <path  id= "cierre" d="M35.0871 88.8847L34.4472 226.993" stroke="#B7A6A6" stroke-width="2"/>
                {#each nivelesY as y, i}
                  <line
                    x1="30" y1={y}
                    x2="40" y2={y}
                    stroke={i < viaje.Satisfaccion ? "#000000" : "#B7A6A6"}
                    stroke-width="2"
                  />
                {/each}
                <g filter="url(#filter2_d_13_92)">
                <rect width="48.3648" height="62.1777" rx="3" transform="matrix(0.974669 -0.223652 0.231685 0.972791 98.2067 47.0853)" fill="#404040"/>
                </g>
                <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 129 48)" fill="white"/>
                <rect width="14.202" height="16.0479" rx="1" transform="matrix(0.975098 -0.221775 0.229748 0.97325 134 67.1497)" fill="white"/>
          
                <g filter="url(#filter3_d_13_92)">
                <path d="M138 37.5C138 37.5 132.019 22.3911 126.5 19.5C121.527 16.895 118.486 16.7363 113 18.5C107.486 20.2728 106 22 104 27C101.047 34.383 105.5 45.5 105.5 45.5" stroke="black" stroke-width="2"/>
                </g>
                <ellipse cx="106.08" cy="45.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 106.08 45.2264)" fill="black"/>
                <ellipse cx="138.08" cy="38.2264" rx="5.00106" ry="0.964926" transform="rotate(-15 138.08 38.2264)" fill="black"/>
                <defs>
                <filter id="filter0_d_13_92" x="67" y="0" width="59" height="52" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_92"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_92" result="shape"/>
                </filter>
                <filter id="filter1_d_13_92" x="0" y="35" width="189" height="251" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_92"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_92" result="shape"/>
                </filter>
                <filter id="filter2_d_13_92" x="94.8196" y="36.8626" width="68.3195" height="78.1145" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_92"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_92" result="shape"/>
                </filter>
                <filter id="filter3_d_13_92" x="97.9884" y="16.3328" width="44.9411" height="37.5385" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
                <feFlood flood-opacity="0" result="BackgroundImageFix"/>
                <feColorMatrix in="SourceAlpha" type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0" result="hardAlpha"/>
                <feOffset dy="4"/>
                <feGaussianBlur stdDeviation="2"/>
                <feComposite in2="hardAlpha" operator="out"/>
                <feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.25 0"/>
                <feBlend mode="normal" in2="BackgroundImageFix" result="effect1_dropShadow_13_92"/>
                <feBlend mode="normal" in="SourceGraphic" in2="effect1_dropShadow_13_92" result="shape"/>
                </filter>
                </defs>
                <text
                  x="142"
                  y="74"
                  text-anchor="middle"
                  font-size="20"
                  fill="black"
                  font-family="sans-serif"
                  transform="rotate(-15 90 75)"
                >
                  {viaje.Mes.toString().padStart(2, '0')[0]}
                </text>

                <text
                  x="142"
                  y="94.5"
                  text-anchor="middle"
                  font-size="20"
                  fill="black"
                  font-family="sans-serif"
                  transform="rotate(-15 90 75)"
                >
                  {viaje.Mes.toString().padStart(2, '0')[1]}
                </text>


                </svg> 
          {/if}
      </div>
    {/each}
  </div>
</main>

<style>

  h2{
    font-size: 50px;

  }
  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 80px;
    margin-bottom: 80px;
  }
  .headline {
      font-size: 40px;
      font-weight: 300;
      line-height: 1.2;
      text-align: center;
      margin: 20px;
      margin-top: 50px;
    }
  
  .valija {
    flex: 1 1 200px;    /* Ocupar al menos 200px, expandirse si hay lugar */
    max-width: 220px;   /* Para que no crezcan demasiado */
  }

  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 40px;         /* Espacio horizontal y vertical entre valijas */
    max-width: 1200px; /* Ancho máximo de la grilla */
    margin: 0 auto;    /* Centra el contenedor dentro de la página */
    padding: 40px 20px;
  }

</style>