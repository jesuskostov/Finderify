<template>
  <div>
    <div class="city-name align-items-center" :class="{'d-none': show}">
      <h1 class="flex-grow-1">{{cityName}} - {{typeName}}</h1>
    </div>

    <div class="search-container" :class="{'show': show}">
      <div class="container py-4 d-flex flex-column justify-content-between align-items-center h-100">
        <div class="w-100">
          <h3 class="mb-4">Намери твоето място</h3>
          <select class="w-100" v-model="choosenCity" @change="locator">
            <option v-for="(city, i) in cities" :key="i" :value="`${city.lat},${city.lng},${city.city}`">{{city.city}}</option>
          </select>
          <div class="row">
            <div v-if="showBox" class="col-6 col-md-6">
              <!-- Transport -->
              <div @click='turnOn(transport)' class="category-box" :class="{'disable': disable}">
                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 612 612" style="enable-background:new 0 0 612 612;" xml:space="preserve">
                  <g>
                    <path d="M612,195.722c0,105.87-510.374,222.727-549.02,222.727c-21.667,0-46.25-4.994-46.25-24.969
                      c0-6.674,7.703-16.32,21.22-27.949l-0.015,0.008L2.109,301.883c-4.851-8.618-1.005-19.536,8.175-23.212l6.157-2.465
                      c11.159-4.468,23.718-3.802,34.341,1.821l65.039,34.432c25.323-15.02,54.049-30.746,84.326-46.229L73.402,184.001
                      c-10.027-6.506-9.92-21.22,0.201-27.578l10.368-6.514c17.256-10.841,38.234-14.043,57.938-8.846l210.85,55.616
                      c65.742-26.094,125.181-43.904,160.363-43.904c9.396,0,18.806,0.249,27.887,0.898l-63.675,28.745l-1.524,21.418l98.29-45.183
                      C597.661,164.272,612,174.759,612,195.722z M355.492,378.476l78.648,89.344c4.793,5.445,12.599,7.084,19.176,4.027l10.533-4.896
                      c19.208-8.928,30.521-29.172,28.061-50.209l-9.846-84.186c-0.61-5.209-5.896-8.506-10.843-6.764l-112.308,39.562
                      C353.447,367.281,351.661,374.125,355.492,378.476z"/>
                  </g>
                </svg>
                <h5>Транспорт</h5>
              </div>
            </div>
              <!-- Services -->
            <div v-if="showBox" class="col-6 col-md-6">
              <div @click="turnOn(service)" class="category-box" :class="{'disable': disable}">
                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512.014 512.014" style="enable-background:new 0 0 512.014 512.014;" xml:space="preserve">
                  <g>
                    <g>
                      <path d="M124.672,280.604c-18.283-17.323-91.392-22.933-113.365-24.235c-3.029-0.043-5.824,0.875-7.957,2.88
                        C1.216,261.255,0,264.071,0,267.015v192c0,5.888,4.779,10.667,10.667,10.667h64c4.608,0,8.704-2.987,10.133-7.36
                        c1.557-4.779,38.315-117.589,43.157-173.056C128.235,286.023,127.04,282.823,124.672,280.604z M66.88,448.348H21.333V278.45
                        c34.283,2.709,71.296,8.597,84.715,15.125C100.395,340.295,74.816,423.303,66.88,448.348z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M510.891,411.548c-14.827-29.632-47.637-44.715-79.744-36.672l-81.728,20.437c-5.717,1.429-9.195,7.211-7.765,12.928
                        c1.429,5.717,7.211,9.216,12.928,7.765l81.728-20.395c18.645-4.651,37.632,1.877,49.387,16.128l-105.749,48.085
                        c-89.685,36.757-92.779,35.584-131.243,21.077l-160-53.333c-5.632-1.856-11.627,1.152-13.483,6.741
                        c-1.856,5.589,1.152,11.627,6.741,13.483l159.595,53.184c17.941,6.763,30.315,10.688,44.224,10.688
                        c21.632,0,46.976-9.451,102.656-32.299l117.333-53.333c2.624-1.195,4.672-3.413,5.632-6.144
                        C512.363,417.138,512.192,414.151,510.891,411.548z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M311.637,341.938l-192-42.667c-5.675-1.173-11.456,2.368-12.736,8.107c-1.259,5.76,2.347,11.456,8.107,12.736
                        l191.723,42.603c23.637,5.909,33.131,15.211,34.432,34.688l-20.48,5.12c-7.573,1.899-15.659,2.112-23.381,0.555l-92.544-18.517
                        c-5.845-1.216-11.392,2.581-12.544,8.363c-1.152,5.781,2.581,11.392,8.363,12.544l92.565,18.517
                        c4.8,0.96,9.728,1.429,14.635,1.429c6.101,0,12.224-0.747,18.091-2.219l28.715-7.168c4.757-1.195,8.085-5.461,8.085-10.347v-3.371
                        C362.667,369.372,347.029,350.77,311.637,341.938z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M501.333,235.015H96c-5.888,0-10.667,4.779-10.667,10.667S90.112,256.348,96,256.348h405.333
                        c5.888,0,10.667-4.779,10.667-10.667S507.221,235.015,501.333,235.015z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M298.667,43.015c-105.856,0-192,86.144-192,192v10.667c0,5.888,4.779,10.667,10.667,10.667H480
                        c5.888,0,10.667-4.779,10.667-10.667v-10.667C490.667,129.159,404.523,43.015,298.667,43.015z M128,235.015
                        c0-94.123,76.565-170.667,170.667-170.667s170.667,76.565,170.667,170.667H128z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M298.667,85.682c-69.525,0-129.28,47.232-145.323,114.859c-1.344,5.739,2.197,11.477,7.915,12.843
                        c0.832,0.213,1.664,0.299,2.475,0.299c4.843,0,9.216-3.307,10.368-8.213c13.76-57.963,64.981-98.453,124.565-98.453
                        c5.888,0,10.667-4.779,10.667-10.667S304.555,85.682,298.667,85.682z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M298.667,0.348C275.136,0.348,256,19.484,256,43.015v10.667c0,5.888,4.779,10.667,10.667,10.667
                        s10.667-4.779,10.667-10.667V43.015c0-11.755,9.579-21.333,21.333-21.333c11.755,0,21.333,9.579,21.333,21.333v10.667
                        c0,5.888,4.779,10.667,10.667,10.667s10.667-4.779,10.667-10.667V43.015C341.333,19.484,322.197,0.348,298.667,0.348z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M487.552,238.151c-4.16-4.16-10.923-4.16-15.083,0l-39.552,39.552H164.416l-39.552-39.552
                        c-4.16-4.16-10.923-4.16-15.083,0c-4.16,4.16-4.16,10.923,0,15.083l42.667,42.667c2.005,1.984,4.715,3.115,7.552,3.115h277.333
                        c2.837,0,5.547-1.131,7.552-3.115l42.667-42.667C491.712,249.074,491.712,242.311,487.552,238.151z"/>
                    </g>
                  </g>
                </svg>
                <h5>Услуги</h5>
              </div>
            </div>
              <!-- Entertainment -->
            <div v-if="showBox" class="col-6 col-md-6">
              <div @click="turnOn(entertainment)" class="category-box" :class="{'disable': disable}">
                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve">
                  <g>
                    <g>
                      <path d="M384,310.857H18.286C8.187,310.857,0,319.044,0,329.143c0,10.099,8.187,18.286,18.286,18.286H384
                        c10.099,0,18.286-8.187,18.286-18.286C402.286,319.044,394.099,310.857,384,310.857z"/>
                      <path d="M237.714,246.857H76.16c-1.982,15.41-4.941,30.679-8.859,45.714h258.542c-3.918-15.035-6.877-30.304-8.859-45.714
                        h-42.697c-5.049,0-9.143-4.093-9.143-9.143s4.093-9.143,9.143-9.143h40.512c-1.143-10.907-2.103-23.077-2.798-36.571H164.571
                        c-5.049,0-9.143-4.093-9.143-9.143c0-5.049,4.093-9.143,9.143-9.143H311.25c-0.247-8.677-0.393-17.801-0.393-27.429
                        c-0.836-45.386,3.279-90.728,12.27-135.223c0.627-2.675-0.018-5.489-1.746-7.625c-1.742-2.182-4.385-3.448-7.177-3.438H78.939
                        c-2.792-0.01-5.435,1.256-7.177,3.438c-1.728,2.136-2.373,4.95-1.746,7.625c8.991,44.495,13.105,89.837,12.27,135.223
                        c0,9.627-0.146,18.752-0.393,27.429H128c5.049,0,9.143,4.093,9.143,9.143c0,5.049-4.093,9.143-9.143,9.143H81.143
                        c-0.695,13.495-1.655,25.664-2.798,36.571h159.369c5.049,0,9.143,4.093,9.143,9.143S242.764,246.857,237.714,246.857z"/>
                      <path d="M488.768,83.73c-14.765-13.927-34.694-21.025-54.939-19.566c-39.084,3.535-68.806,36.649-68.114,75.886v24.521
                        c-0.007,5.505,2.466,10.72,6.733,14.198c4.267,3.478,9.874,4.848,15.265,3.731c8.705-2.107,14.769-9.99,14.574-18.944v-26.414
                        c0-9.707,3.859-19.016,10.728-25.876c6.868-6.86,16.182-10.707,25.889-10.695c2.406,0.004,4.807,0.239,7.168,0.704
                        c17.35,3.729,29.645,19.202,29.358,36.946V384H512V137.143C511.954,116.897,503.547,97.568,488.768,83.73z"/>
                      <rect x="475.429" y="402.286" width="36.571" height="54.857"/>
                      <rect x="475.429" y="475.429" width="36.571" height="36.571"/>
                    </g>
                  </g>
                </svg>
                <h5>Развлечение</h5>
              </div>
            </div>
              <!-- Care -->
            <div v-if="showBox" class="col-6 col-md-6">
              <div @click="turnOn(care)" class="category-box" :class="{'disable': disable}">
                <svg enable-background="new 0 0 512 512" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg">
                    <g>
                    <circle cx="256" cy="60" r="60"/><path d="m181 255h150c8.284 0 15-6.716 15-15v-45c0-26.855-11.827-50.996-30.541-67.5-34 29.985-84.873 30.025-118.918 0-18.714 16.504-30.541 40.645-30.541 67.5v45c0 8.284 6.716 15 15 15z"/><path d="m226.206 360.33-47.604-47.1c-21.559-21.378-54.788-23.828-79.022-7.393-5.18 3.513-5.84 10.902-1.415 15.327l59.695 59.695c5.219 5.219 4.938 13.762-.612 18.627-5.074 4.447-12.732 4.179-17.482-.613l-63.766-64.335v-147.038c0-16.845-13.655-30.5-30.5-30.5-16.845 0-30.5 13.655-30.5 30.5v144.233c0 18.726 7.503 36.671 20.831 49.824l75.442 74.449v40.994c0 8.284 6.716 15 15 15h99.727c8.284 0 15-6.716 15-15v-101.166c0-13.334-5.326-26.115-14.794-35.504z"/><path d="m285.794 360.33 47.604-47.1c21.559-21.378 54.788-23.828 79.022-7.393 5.18 3.513 5.84 10.902 1.415 15.327l-59.695 59.695c-5.219 5.219-4.938 13.762.612 18.627 5.074 4.447 12.732 4.179 17.482-.613l63.766-64.335v-147.038c0-16.845 13.655-30.5 30.5-30.5 16.845 0 30.5 13.655 30.5 30.5v144.233c0 18.726-7.503 36.671-20.831 49.824l-75.442 74.449v40.994c0 8.284-6.716 15-15 15h-99.727c-8.284 0-15-6.716-15-15v-101.166c0-13.334 5.326-26.115 14.794-35.504z"/>
                    </g>
                </svg>
                <h5>Грижа</h5>
              </div>
            </div>
              <!-- Store -->
            <div v-if="showBox" class="col-6 col-md-6">
              <div @click="turnOn(store)" class="category-box" :class="{'disable': disable}">
                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512.005 512.005" style="enable-background:new 0 0 512.005 512.005;" xml:space="preserve">
                  <g>
                    <g>
                      <path d="M509.123,166.723l-80-112c-3.2-4.16-8-6.72-13.12-6.72h-320c-5.12,0-9.92,2.56-13.12,6.72l-80,112
                        c-0.96,2.88-1.92,5.76-2.88,8.64c-0.32,35.52,28.48,64.64,64,64.64c19.2,0,36.16-8.32,48-21.76c11.84,13.44,28.8,21.76,48,21.76
                        s36.16-8.32,48-21.76c11.84,13.44,28.8,21.76,48,21.76s36.16-8.32,48-21.76c11.84,13.44,28.8,21.76,48,21.76s36.16-8.32,48-21.76
                        c11.84,13.44,28.8,21.76,48,21.76c35.52,0,64.32-29.12,64-64.64C511.043,172.483,510.083,169.603,509.123,166.723z"/>
                    </g>
                  </g>
                  <g>
                    <g>
                      <path d="M448.003,272.003c-16.992,0-33.536-4.544-48-12.928c-28.928,16.736-67.072,16.736-96,0c-28.928,16.736-67.104,16.736-96,0
                        c-28.896,16.736-67.104,16.736-96,0c-24.032,13.952-53.792,15.744-80,6.688v166.24c0,17.664,14.336,32,32,32h256v-160h96v160h32
                        c17.664,0,32-14.336,32-32V266.147C469.827,269.763,459.107,272.003,448.003,272.003z M224.003,400.003h-128v-96h128V400.003z"/>
                    </g>
                  </g>
                </svg>
                <h5>Магазини</h5>
              </div>
            </div>
              <!-- Other -->
            <div v-if="showBox" class="col-6 col-md-6">
              <div @click="turnOn(other)" class="category-box" :class="{'disable': disable}">
                <svg enable-background="new 0 0 512.002 512.002" viewBox="0 0 512.002 512.002" xmlns="http://www.w3.org/2000/svg">
                  <g>
                    <path d="m44.47 55.076c1.465 1.464 3.385 2.197 5.304 2.197s3.839-.732 5.304-2.197c2.929-2.929 2.929-7.678 0-10.606l-42.273-42.272c-2.93-2.929-7.678-2.929-10.607 0s-2.929 7.678 0 10.606zm190.662 19.488c4.143 0 7.5-3.358 7.5-7.5v-35.393l26.528 38.414c2.202 3.183 5.875 4.533 9.358 3.446 3.555-1.11 5.852-4.437 5.852-8.547l-.557-57.556c-.04-4.117-3.39-7.427-7.498-7.427-.025 0-.05 0-.074 0-4.143.04-7.468 3.43-7.428 7.572l.35 36.12-27.859-40.343c-1.864-2.701-5.267-3.874-8.404-2.898-3.133.977-5.268 3.878-5.268 7.16v59.452c0 4.142 3.358 7.5 7.5 7.5zm70.516-32.94c38.409 8.858 73.849 28.035 102.485 55.456 28.563 27.35 49.241 61.818 59.802 99.679.926 3.316 3.938 5.487 7.221 5.487.667 0 1.345-.09 2.019-.278 3.99-1.113 6.322-5.25 5.21-9.239-11.284-40.452-33.372-77.273-63.877-106.483-30.588-29.289-68.448-49.773-109.489-59.238-4.034-.932-8.063 1.586-8.994 5.623-.931 4.035 1.587 8.062 5.623 8.993zm-293.899 244.72c.07.356.167.708.288 1.05 1.251 3.528 4.596 5.889 8.335 5.889h.058c3.764-.024 7.105-2.435 8.316-5.997.022-.065.044-.131.064-.196l10.955-35.394 10.906 35.401c.031.102.065.203.101.303 1.253 3.525 4.597 5.884 8.334 5.884h.058c3.761-.024 7.102-2.432 8.315-5.992.106-.313.191-.631.256-.955l11.65-58.542c.809-4.063-1.829-8.011-5.892-8.82-4.062-.807-8.011 1.83-8.819 5.892l-6.859 34.469-10.882-35.322c-1.22-3.959-5.417-6.179-9.376-4.959-2.685.827-4.565 3.024-5.12 5.587l-10.74 34.699-6.839-34.574c-.805-4.063-4.747-6.706-8.813-5.902-4.063.804-6.706 4.75-5.902 8.813zm450.48-229.071c1.919 0 3.839-.732 5.304-2.197l42.272-42.272c2.929-2.929 2.929-7.678 0-10.606-2.929-2.929-7.677-2.929-10.607 0l-42.273 42.272c-2.929 2.929-2.929 7.678 0 10.606 1.465 1.465 3.384 2.197 5.304 2.197zm42.272 176.718c4.143 0 7.5-3.358 7.5-7.5s-3.357-7.5-7.5-7.5h-24.868c-4.143 0-7.5 3.358-7.5 7.5v59.02c0 4.142 3.357 7.5 7.5 7.5h24.868c4.143 0 7.5-3.358 7.5-7.5s-3.357-7.5-7.5-7.5h-17.368v-14.51h15.534c4.143 0 7.5-3.358 7.5-7.5s-3.357-7.5-7.5-7.5h-15.534v-14.51zm-469.671-32.025c.674.188 1.352.278 2.019.278 3.282 0 6.296-2.171 7.221-5.487 10.63-38.112 31.496-72.757 60.34-100.191 28.932-27.518 64.703-46.634 103.447-55.282 4.043-.902 6.589-4.911 5.687-8.954-.903-4.043-4.914-6.592-8.954-5.686-41.398 9.241-79.615 29.661-110.518 59.052-30.806 29.3-53.093 66.311-64.451 107.03-1.114 3.99 1.218 8.127 5.209 9.24zm442.343 108.069c-3.99-1.114-8.127 1.22-9.239 5.209-10.56 37.861-31.238 72.329-59.801 99.678-28.636 27.421-64.074 46.597-102.483 55.456-4.036.931-6.554 4.958-5.623 8.994.801 3.469 3.888 5.816 7.302 5.816.559 0 1.125-.063 1.692-.193 41.04-9.465 78.9-29.949 109.487-59.237 30.504-29.21 52.592-66.031 63.875-106.482 1.113-3.992-1.22-8.129-5.21-9.241zm-9.64 146.891c-2.93-2.929-7.678-2.929-10.607 0s-2.929 7.678 0 10.606l42.272 42.272c1.465 1.464 3.385 2.197 5.304 2.197s3.839-.732 5.304-2.197c2.929-2.929 2.929-7.678 0-10.606zm-115.62-92.898c3.099 0 6.147-1.224 8.52-3.596 4.028-4.028 4.745-10.003 1.784-14.869l-34.938-57.435 8.804-2.144c4.024-.98 6.493-5.037 5.513-9.062-.98-4.024-5.041-6.494-9.062-5.512l-41.989 10.226c-4.419 1.077-7.832 4.49-8.907 8.908l-25.636 105.258-25.636-105.257c-1.075-4.419-4.488-7.833-8.908-8.909l-105.258-25.635 105.259-25.635c4.419-1.077 7.832-4.49 8.907-8.908l25.635-105.258 25.636 105.257c1.075 4.419 4.488 7.833 8.908 8.909l105.258 25.635-36.93 8.994c-4.024.98-6.493 5.038-5.513 9.062.979 4.023 5.035 6.49 9.062 5.512l48.42-11.792c5.533-1.348 9.252-6.081 9.251-11.777 0-5.695-3.718-10.427-9.252-11.775l-83.563-20.352 34.938-57.434c2.961-4.866 2.244-10.841-1.783-14.869-4.029-4.029-10.005-4.745-14.869-1.785l-57.435 34.938-20.352-83.562c-1.347-5.534-6.079-9.252-11.774-9.253-.001 0 0 0-.001 0-5.695 0-10.428 3.718-11.776 9.252l-20.351 83.562-57.434-34.937c-4.865-2.96-10.841-2.245-14.869 1.784-4.028 4.028-4.745 10.003-1.784 14.869l27.486 45.187c1.411 2.321 3.883 3.604 6.414 3.604 1.328 0 2.673-.353 3.891-1.093 3.539-2.153 4.663-6.767 2.51-10.305l-21.34-35.083 51.402 31.268-3.943 16.191-115.046 28.019c-5.533 1.348-9.252 6.081-9.251 11.777 0 5.695 3.718 10.427 9.252 11.775l83.563 20.352-34.938 57.434c-2.961 4.866-2.244 10.841 1.783 14.869 2.373 2.373 5.422 3.597 8.521 3.597 2.162 0 4.349-.595 6.348-1.812l57.435-34.938 20.352 83.562c1.347 5.534 6.079 9.252 11.774 9.253h.001c5.695 0 10.428-3.718 11.776-9.252l20.351-83.563 57.434 34.937c2 1.216 4.186 1.811 6.35 1.811zm-8.658-195.282-31.268 51.403-16.191-3.943-3.943-16.191zm-174.508 174.509 31.268-51.403 16.191 3.943 3.943 16.191zm123.106-31.268 3.943-16.191 16.191-3.943 31.268 51.402zm-26.667 156.165c-7.307-2.695-14.109-5.63-16.208-6.548-1.594-1.286-1.54-3.075-1.433-3.822.149-1.041.906-3.585 4.699-4.728 8.36-2.517 16.109 3.594 16.341 3.779 3.17 2.63 7.873 2.211 10.528-.947 2.665-3.171 2.256-7.902-.915-10.567-.563-.474-13.979-11.541-30.28-6.627-8.243 2.483-14.075 8.98-15.221 16.958-1.075 7.486 2.17 14.688 8.469 18.795.331.216.679.405 1.04.567.345.154 8.549 3.805 17.788 7.213 2.599.958 8.559 3.661 7.775 8.048-.591 3.307-4.624 6.728-10.352 6.728-5.905 0-11.587-2.38-15.199-6.366-2.783-3.07-7.526-3.301-10.594-.521-3.069 2.782-3.303 7.524-.521 10.594 6.409 7.071 16.246 11.292 26.314 11.292 12.579 0 23.143-8.029 25.117-19.091 1.489-8.326-2.288-19.202-17.348-24.757zm-220.716-11.226-42.272 42.272c-2.929 2.929-2.929 7.678 0 10.606 1.465 1.465 3.384 2.197 5.304 2.197 1.919 0 3.839-.732 5.304-2.197l42.272-42.272c2.929-2.929 2.929-7.678 0-10.606-2.929-2.93-7.677-2.93-10.608 0zm172.22 15.574c-83.738-15.102-151.832-78.066-173.476-160.411-1.054-4.006-5.154-6.399-9.16-5.347-4.007 1.053-6.4 5.154-5.348 9.16 23.122 87.964 95.864 155.226 185.321 171.359.45.081.897.121 1.34.121 3.56 0 6.718-2.544 7.372-6.17.736-4.076-1.973-7.977-6.049-8.712z"/>
                  </g>
                </svg>
                <h5>Други</h5>
              </div>
            </div>
          </div>
          <div v-if="first" class="text-left">
            <h4>Транспорт</h4>
            <select class="w-100" v-model="getType">
              <option v-for="(transport, i) in transports" :key="i" :value="`${transport.category},${transport.name}`">{{transport.name}}</option>
            </select>
          </div>
          <div v-if="second" class="text-left">
            <h4>Услуги</h4>
            <select class="w-100" v-model="getType">
              <option v-for="(service, i) in services" :key="i" :value="`${service.category},${service.name}`">{{service.name}}</option>
            </select>
          </div>
          <div v-if="third" class="text-left">
            <h4>Развлечение</h4>
            <select class="w-100" v-model="getType">
              <option v-for="(еntertainment, i) in еntertainments" :key="i" :value="`${еntertainment.category},${еntertainment.name}`">{{еntertainment.name}}</option>
            </select>
          </div>
          <div v-if="fourth" class="text-left">
            <h4>Грижа</h4>
            <select class="w-100" v-model="getType">
              <option v-for="(care, i) in cares" :key="i" :value="`${care.category},${care.name}`">{{care.name}}</option>
            </select>
          </div>
          <!-- <select class="w-100">
            <option value="none">Магазини</option>
          </select>
          <select class="w-100">
            <option value="none">Други</option>
          </select> -->
        </div>
        <div class="w-100">
          <button v-if="showFindBtn" @click="getObjects" class="findBtn mb-3">Find places</button>
          <button v-if="backBtn" @click="goBack" class="findBtn">GO BACK</button>
        </div>
      </div>
    </div>
    
    <div class="container custom-padding">
      <p v-if="!hide" class="txt">Здравей, добре дошъл в моето нелепо приложение, което се опитавам да напарвя вече от не знам колко дни или седмици, по принцип тук ще трябва да изпиша някакъв умен текст, който да впечети потребителя (теб), но все още не съм го измисли.</p>
      <img v-if="!hide" class="city-img" src="../city.png" alt="">
      <button @click="show = true" class="choose-city" :class="{'absolute': hide}"><span v-if="cityName == ''">Избери град</span> <span v-else>{{cityName}}</span></button>
      <div class="row">
        <div v-for="(object, i) in places" :key="i" class="col-12 col-md-4" :class="{'d-none': !object.photos}">
          <div v-for="(img, i) in object.photos" :key="i" class="box" @click="test(object)">
            <div class="working" :class="{'open': object.opening_hours}"><span v-if="object.opening_hours">Open</span><span v-else>Close</span></div>
              <img :src="`https://maps.googleapis.com/maps/api/place/photo?maxwidth=1000&photoreference=${img.photo_reference}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`" alt="">
            <div class="title">
              <h3>{{object.name}}</h3>
            </div>
            <div v-if="object.rating" class="rating">
              <p>{{object.rating}}</p>
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 19.481 19.481" xmlns:xlink="http://www.w3.org/1999/xlink" enable-background="new 0 0 19.481 19.481">
                <g>
                  <path d="m10.201,.758l2.478,5.865 6.344,.545c0.44,0.038 0.619,0.587 0.285,0.876l-4.812,4.169 1.442,6.202c0.1,0.431-0.367,0.77-0.745,0.541l-5.452-3.288-5.452,3.288c-0.379,0.228-0.845-0.111-0.745-0.541l1.442-6.202-4.813-4.17c-0.334-0.289-0.156-0.838 0.285-0.876l6.344-.545 2.478-5.864c0.172-0.408 0.749-0.408 0.921,0z"/>
                </g>
              </svg>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.category-box {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin-bottom: 30px;
  background-color: #fff;
  box-shadow: 0 1px 1px rgba(0,0,0,0.08), 
                0 2px 2px rgba(0,0,0,0.12), 
                0 4px 4px rgba(0,0,0,0.16), 
                0 8px 8px rgba(0,0,0,0.20);
  height: 100px;
  border-radius: 4px;

  &.disable {
    opacity: 0.5;
    pointer-events: none;
  }

  svg {
    flex-grow: 1;
    width: 50px;
    height: 50px;
  }

  h5 {
    color: #000;
    font-size: 14px;
    margin: -10px 0 10px 0;
  }
}
.txt {
  text-align: left;
  font-size: 13px;
}
select {
  height: 40px;
  background-color: #fff;
  margin-bottom: 20px;
}
.choose-city{
  width: 100%;
  height: 50px;
  border: 0;
  border-radius: 4px;
  background-color: #0986de;
  color: #fff;
  margin-top: -5px;

  &.absolute {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 1030;
    border-radius: 0;
  }
}
.city-img {
  width: 100%;
  margin-top: 15%;
}
.findBtn {
  width: 100%;
  border: 0;
  border-radius: 2px;
  height: 48px;
  background-color: #fff;

  &.absolute {
    position: fixed;
    bottom: 20px;
  }
}
.custom-padding {
  padding-top: 30%;
  padding-bottom: 20%;
}
.city-name {
  position: fixed;
  display: flex;
  top: 0;
  left: 0;
  right: 0;
  height: 50px;
  background-color: #0986de;
  z-index: 10;

  h1 {
    margin: 0;
    color: #fff;
    font-size: 20px;
  }
}
.showSearch {
  height: 50px;
  border: 0;
  border-radius: 99999px;
  background-color: #0986de;
  color: #fff;

  &.absolute {
    position: absolute;
    right: 0;
  }
}
.search-container {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #0986de;
  opacity: 0;
  visibility: hidden;
  transition: 0.6s;
  z-index: 1036;
  color: #fff;

  &.show {
    opacity: 1;
    visibility: visible;
    transition: 0.6s;
  }

  &.hide {
    opacity: 0;
    visibility: hidden;
    transition: 0.6s;
  }
}
.box {
  cursor: pointer;
  position: relative;
  overflow: hidden;
  height: 250px;
  border-radius: 15px;
  box-shadow: 0 1px 1px rgba(0,0,0,0.08), 
                0 2px 2px rgba(0,0,0,0.12), 
                0 4px 4px rgba(0,0,0,0.16), 
                0 8px 8px rgba(0,0,0,0.20);
  margin-bottom: 30px;
  
  .working {
    position: absolute;
    width: 60px;
    height: 20px;
    color: #fff;
    top: 10px;
    left: 15px;
    font-size: 12px;
    border-radius: 5px;
    background-color: #b51919;

    &.open {
      background-color: green;
    }
  }

  .rating {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 0;
    right: 0;
    width: 50%;
    height: 40px;
    background-color: #b51919;
    z-index: 5;
    transform: rotate(45deg) translate(30%, -50%);
    border: 1px solid gold;

    p {
      margin: 0;
      color: #fff;
    }

    svg {
      width: 15px;
      height: 15px;
      fill: gold;
      margin-left: 8px;
      position: relative;
      top: -2px;
    }

  }

  .title {
    position: absolute;
    text-align: left;
    bottom: 0;
    z-index: 2;
    padding: 0 15px 30px 15px;

    h3 {
      margin: 0;
      color: #fff;
      font-size: 18px;
    }
  }
  
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  &::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgb(4,4,4);
    background: linear-gradient(0deg, rgba(4,4,4,1) 0%, rgba(4,4,4,0) 100%);
    pointer-events: none;
  }
}
</style>

<script>
import axios from 'axios';
import city from '../bg'

export default {
  data() {
    return {
      showBox: true,
      first: false,
      second: false,
      third: false,
      fourth: false,
      fifth: false,
      sixth: false,
      transport: 'transport',
      service: 'service',
      entertainment: 'entertainment',
      care: 'care',
      store: 'store',
      other: 'other',
      disable: true,
      showFindBtn: false,
      backBtn: false,
      getType: '',
      typeName: '',
      show: false,
      hide: false,
      type: "",
      radius: "10",
      lat: 0,
      lng: 0,
      places: [],
      cities: [],
      choosenCity: '',
      cityName: '',
      transports: [
        { name: 'ЖП - Гара', category: 'train_station' },
        { name: 'Метро', category: 'subway_station' }, 
        { name: 'Летище', category: 'airport' }, 
        { name: 'Автогара', category: 'bus_station' }
      ],
      services: [
        {name: 'Банкомати', category: 'atm'},
        {name: 'Банки', category: 'bank'},
        {name: 'Пекарни', category: 'bakery'},
        {name: 'Доктори', category: 'doctor'},
        {name: 'Зъболекари', category: 'dentist'},
        {name: 'Автокъщи', category: 'car_dealer'},
        {name: 'Сервизи', category: 'car_repair'},
        {name: 'Автомивки', category: 'car_wash'},
        {name: 'Адвокати', category: 'lawyer'},
        {name: 'Бояджии', category: 'painter'},
        {name: 'Паркинги', category: 'parking'},
        {name: 'Ветеринари', category: 'veterinary_care'},
        {name: 'Бензиностанции', category: 'gas_station'},
        {name: 'Аптеки', category: 'pharmacy'},
        {name: 'Пощи', category: 'post_office'},
      ],
      еntertainments: [
        {name: 'Барове', category: 'bar'},
        {name: 'Кафета', category: 'cafe'},
        {name: 'Казина', category: 'casino'},
        {name: 'Нощни клубове', category: 'night_clubs'},
        {name: 'Паркове', category: 'park'},
        {name: 'Спа', category: 'spa'},
        {name: 'Боулинг', category: 'bowling_alley'},
        {name: 'Ресторанти', category: 'restaurant'},
        {name: 'Молове', category: 'shopping_mall'},
      ],
      cares: [
        {name: 'Фитнес', category: 'gym'},
        {name: 'Салони за красота', category: 'beauty_salon'},
        {name: 'Фризьорски салони', category: 'hair_care'},
      ],
      // stores: ['clothing_store', 'shoe_store', 'store', 'supermarket', 'book_store', 'bicycle_store', 'pet_store'],
      // others: ['fire_station', 'hospital', 'police', 'church', 'museum', 'school', 'stadium', 'tourist_attraction', 'zoo', 'art_gallery', 'library']
    }
  },
  created() {
    this.cities = city;
      navigator.geolocation.getCurrentPosition(position => {
        this.lat = position.coords.latitude.toFixed(6)
        this.lng = position.coords.longitude.toFixed(6)

        // city.filter( obj => {
        //   let currentLat = obj.lat
        //   let currentLng = obj.lng

        //   if(currentLat == this.lat && currentLng == this.lng) {
        //     console.log(123);
        //   }
        // })
      },
      error => {
        console.log(error);
      })
  },
  computed: {
    cordinates() {
      return `${this.lat}, ${this.lng}`
    },
  },
  methods: {
    getObjects() {
      let typeAndName = this.getType.split(',')
      this.type = typeAndName[0]
      this.typeName = typeAndName[1]

      setTimeout(() => {
        const URL = `https://cors-anywhere.herokuapp.com/https://maps.googleapis.com/maps/api/place/nearbysearch/json?location=${
          this.lat
        },${this.lng}&type=${this.type}&radius=${this.radius *
          1000}&key=AIzaSyB5QQ6LGOdx52-w-QKnYSpOrQaz2XKSyIE`;
        axios.get(URL).then(res => {
          this.places = res.data.results
        }).catch(err => {
          console.log(err.message);
        })
        this.show = false
        this.hide = true
      }, 100)

    },
    locator() {
      let splitCordinates = this.choosenCity.split(',')
      this.lat = splitCordinates[0]
      this.lng = splitCordinates[1]
      this.cityName = splitCordinates[2]

      this.disable = false
    },
    turnOn(option) {
      this.showBox = false
      this.showFindBtn = true
      this.backBtn = true

      if (option == 'transport') {
        this.first = true
        this.second = false
        this.third = false
        this.fourth = false
        this.fifth = false
        this.sixth = false
      } else if (option == 'service') {
        this.first = false
        this.second = true
        this.third = false
        this.fourth = false
        this.fifth = false
        this.sixth = false
      } else if (option == 'entertainment') {
        this.first = false
        this.second = false
        this.third = true
        this.fourth = false
        this.fifth = false
        this.sixth = false
      } else if (option == 'care') {
        this.first = false
        this.second = false
        this.third = false
        this.fourth = true
        this.fifth = false
        this.sixth = false
      } else if (option == 'store') {
        this.first = false
        this.second = false
        this.third = false
        this.fourth = false
        this.fifth = true
        this.sixth = false
      } else if (option == 'other') {
        this.first = false
        this.second = false
        this.third = false
        this.fourth = false
        this.fifth = false
        this.sixth = true
      }
    },
    goBack() {
      this.showFindBtn = false
      this.backBtn = false
      this.showBox = true
      this.first = false
      this.second = false
      this.third = false
      this.fourth = false
      this.fifth = false
      this.sixth = false
    },
    test(object) {
      window.open(`https://www.google.com/maps/place/?q=place_id:${object.place_id}`, "_blank");    
    }
  }
}
</script>