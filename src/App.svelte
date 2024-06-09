<script>
  let colorPrincipalRp = localStorage.getItem("colorPrincipalRp") || "#B59FDF";
  let colorWhiteFond = localStorage.getItem("colorWhiteFond") || "#FFFFFF";
  let colorBlack = localStorage.getItem("colorBlack") || "#000000";
  let fontPoppins = "Poppins, sans-serif";
  let fontSatisfy = "Satisfy, cursive";

  let imgPerso1 = localStorage.getItem("imgPerso1") || "https://zupimages.net/up/24/19/uxyx.png";
  let imgPerso2 = localStorage.getItem("imgPerso2") || "https://zupimages.net/up/24/19/4tp3.png";
  let imgHeader = localStorage.getItem("imgHeader") || "https://zupimages.net/up/24/19/e3y0.gif";

  let titleRp = localStorage.getItem("titleRp") || "Paumée dans la forêt.. vraiment ?";
  let featRp = localStorage.getItem("featRp") || "Feat Nana & Baryon";
  let texteRp = localStorage.getItem("texteRp") || `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla diam ipsum, cursus nec dictum sit amet, lacinia quis ex. Nullam a tortor eget nisl pretium viverra id vitae enim. Donec arcu turpis, tincidunt nec sem a, ultrices dictum lectus. Fusce lacinia sapien tellus, in molestie lacus gravida sit amet. Nullam sed justo et libero ultricies semper ut eget orci. Sed ut massa nec lorem rutrum luctus a in orci. Quisque ultrices tellus a nunc faucibus ultrices.`;

  let dynamicTextBlocks = JSON.parse(localStorage.getItem("dynamicTextBlocks")) || [
      { type: 'text', content: 'Praesent et felis enim. Morbi augue mi, fermentum in pretium vitae, euismod nec magna. Aenean sodales nisi lorem, sit amet sollicitudin neque dignissim non.' },
      { type: 'parole', content: 'un chaton se balade sur le bord du chemin fleuris suivit de ses deux frères et sœurs. Margarett leur petite maîtresse les suit en cueillant des pâquerettes.' },
      { type: 'text', content: 'Curabitur imperdiet id urna malesuada faucibus. Mauris ullamcorper, elit ut hendrerit porta, urna nibh vulputate justo, nec interdum orci magna ut sapien.' }
  ];

  let newText = '';
  let newParole = '';
  let editIndex = null;
  let editContent = '';

  function addTextBlock(type) {
      if (type === 'text' && newText.trim()) {
          dynamicTextBlocks = [...dynamicTextBlocks, { type, content: newText.trim() }];
          newText = '';
      } else if (type === 'parole' && newParole.trim()) {
          dynamicTextBlocks = [...dynamicTextBlocks, { type, content: newParole.trim() }];
          newParole = '';
      }
  }

  function removeTextBlock(index) {
      dynamicTextBlocks = dynamicTextBlocks.filter((_, i) => i !== index);
  }

  function editTextBlock(index) {
      editIndex = index;
      editContent = dynamicTextBlocks[index].content;
  }

  function saveEditTextBlock(index) {
      dynamicTextBlocks[index].content = editContent;
      editIndex = null;
      editContent = '';
  }

  function cancelEdit() {
      editIndex = null;
      editContent = '';
  }

  function saveAllChanges() {
      localStorage.setItem("colorPrincipalRp", colorPrincipalRp);
      localStorage.setItem("colorWhiteFond", colorWhiteFond);
      localStorage.setItem("colorBlack", colorBlack);
      localStorage.setItem("imgPerso1", imgPerso1);
      localStorage.setItem("imgPerso2", imgPerso2);
      localStorage.setItem("imgHeader", imgHeader);
      localStorage.setItem("titleRp", titleRp);
      localStorage.setItem("featRp", featRp);
      localStorage.setItem("texteRp", texteRp);
      localStorage.setItem("dynamicTextBlocks", JSON.stringify(dynamicTextBlocks));

      alert('Modifications sauvegardées');
  }

  // Fonction pour minifier le CSS
  function minifyCSS(css) {
      return css.replace(/\s+/g, ' ').replace(/\/\*[\s\S]*?\*\//g, '').trim();
  }

  // Génère le code à copier en fonction des couleurs actuelles
  $: codeToCopy = `
  <link href="https://fonts.googleapis.com/css2?family=Poppins&family=Satisfy&display=swap" rel="stylesheet">
  <style>
      :root {
          --color-principal-rp: ${colorPrincipalRp};
          --color-white-fond: ${colorWhiteFond};
          --color-black: ${colorBlack};
          --font-poppins: ${fontPoppins};
          --font-satisfy: ${fontSatisfy};
      }
      .fiche_rp {
          display: flex;
          flex-wrap: wrap;
          margin: auto;
          width: 680px;
          background-color: var(--color-principal-rp);
          height: 100%;
          padding: 15px 5px 5px;
      }
      .header_rp {
          background-color: var(--color-white-fond);
          width: 640px;
          height: 280px;
          margin: 5px auto;
          display: flex;
          flex-direction: row;
          flex-wrap: wrap;
      }
      .texte_rp {
          text-align: justify;
          background-color: var(--color-white-fond);
          margin: 15px auto;
          width: 640px;
          padding: 10px 10px 0 10px;
          font: 13px var(--font-poppins);
      }
      .bloc_header_left {
          display: flex;
          flex-wrap: wrap;
          width: 320px;
          height: 280px;
      }
      .bloc_header_right {
          margin-left: auto;
          width: 320px;
      }
      .title_rp {
          color: var(--color-black);
          font: 24px var(--font-poppins);
          padding: 5px;
          text-transform: uppercase;
          position: relative;
          left: -12px;
          top: 11px;
          font-weight: bold;
      }
      .feat_rp {
          padding: 20px;
          position: relative;
          top: -10px;
          text-align: center;
          right: 29px;
          font: 16px var(--font-satisfy);
      }
      .parole_rp {
          margin-top: 8px;
          padding: 10px;
          text-align: justify;
          font: 13px var(--font-poppins);
          background-color: var(--color-principal-rp);
          margin-bottom: 10px; /* Ajouter un espace après chaque parole_rp */
      }
      .bloc_header_right img {
          width: 276px;
          object-fit: cover;
          position: relative;
          right: 6px;
          bottom: 24px;
      }
      .img_perso_1 {
          width: 100px;
          position: relative;
          left: 40px;
          height: 260px;
      }
      .img_perso_2 {
          width: 100px;
          position: relative;
          left: 60px;
          height: 260px;
          top: 20px;
      }
      .credit {
          font-weight: bold;
          text-align: center;
          font: 11px var(--font-poppins);
          color: #5e4d81;
          width: 100%;
      }
      p, .parole_rp, .title_rp, textarea {
          font-family: var(--font-poppins);
      }
  </style>
  <div class="fiche_rp">
      <div class="header_rp">
          <div class="bloc_header_left">
              <img src="${imgPerso1}" class="img_perso_1">
              <img src="${imgPerso2}" class="img_perso_2">
          </div>
          <div class="bloc_header_right">
              <div class="title_rp">${titleRp}</div>
              <div class="feat_rp" style="font-family: var(--font-satisfy);">${featRp}</div>
              <img src="${imgHeader}"/>
          </div>
      </div>
      <div class="texte_rp">
          ${texteRp.split('\n').map(paragraph => `<p>${paragraph}</p>`).join('')}
          ${dynamicTextBlocks.map((block, index) => block.type === 'text'
              ? `<p>${block.content}</p>`
              : `<div class="parole_rp">${block.content}</div>`).join('')}
      </div>
      <div class="credit">Nana Pensionnat Kyoto</div>
  </div>`;

  // Minifie et compresse le code HTML et CSS
  $: minifiedCodeToCopy = minifyCSS(codeToCopy);

  const copyToClipboard = () => {
      navigator.clipboard.writeText(minifiedCodeToCopy).then(() => {
          alert('Le code est bien copié!');
      }).catch(err => {
          console.error('La copie est en erreur : ', err);
      });
  };
</script>

<style>
  :global(:root) {
      --color-principal-rp: {colorPrincipalRp};
      --color-white-fond: {colorWhiteFond};
      --color-black: {colorBlack};
      --font-poppins: {fontPoppins};
      --font-satisfy: {fontSatisfy};
  }
  .fiche_rp {
      display: flex;
      flex-wrap: wrap;
      margin: auto;
      width: 680px;
      background-color: var(--color-principal-rp);
      height: 100%;
      padding: 15px 5px 5px;
  }
  .header_rp {
      background-color: var(--color-white-fond);
      width: 640px;
      height: 280px;
      margin: 5px auto;
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
  }
  .texte_rp {
      text-align: justify;
      background-color: var(--color-white-fond);
      margin: 15px auto;
      width: 640px;
      padding: 10px 10px 0 10px;
      font: 13px var(--font-poppins);
  }
  .bloc_header_left {
      display: flex;
      flex-wrap: wrap;
      width: 320px;
      height: 280px;
  }
  .bloc_header_right {
      margin-left: auto;
      width: 320px;
  }
  .title_rp {
      color: var(--color-black);
      font: 24px var(--font-poppins);
      padding: 5px;
      text-transform: uppercase;
      position: relative;
      left: -12px;
      top: 11px;
      font-weight: bold;
  }
  .feat_rp {
      padding: 20px;
      position: relative;
      top: -10px;
      text-align: center;
      right: 29px;
      font: 16px var(--font-satisfy);
  }
  .parole_rp {
      margin-top: 8px;
      padding: 10px;
      text-align: justify;
      font: 13px var(--font-poppins);
      background-color: var(--color-principal-rp);
      margin-bottom: 10px; /* Ajouter un espace après chaque parole_rp */
  }
  .bloc_header_right img {
      width: 276px;
      object-fit: cover;
      position: relative;
      right: 6px;
      bottom: 24px;
  }
  .img_perso_1 {
      width: 100px;
      position: relative;
      left: 40px;
      height: 260px;
  }
  .img_perso_2 {
      width: 100px;
      position: relative;
      left: 60px;
      height: 260px;
      top: 20px;
  }
  .credit {
      font-weight: bold;
      text-align: center;
      font: 11px var(--font-poppins);
      color: #5e4d81;
      width: 100%;
  }
  p, .parole_rp, .title_rp, textarea {
      font-family: var(--font-poppins);
  }
</style>

<div style="--color-principal-rp: {colorPrincipalRp}; --color-white-fond: {colorWhiteFond}; --color-black: {colorBlack}; --font-poppins: {fontPoppins}; --font-satisfy: {fontSatisfy};">
  <div class="fiche_rp">
      <div class="header_rp">
          <div class="bloc_header_left">
              <img src={imgPerso1} class="img_perso_1">
              <img src={imgPerso2} class="img_perso_2">
          </div>
          <div class="bloc_header_right">
              <div class="title_rp">{titleRp}</div>
              <div class="feat_rp">{featRp}</div>
              <img src={imgHeader} />
          </div>
      </div>

      <div class="texte_rp">
          {#each texteRp.split('\n') as paragraph}
              <p>{paragraph}</p>
          {/each}
          {#each dynamicTextBlocks as block, index}
              {#if block.type === 'text'}
                  <p>
                      {#if editIndex === index}
                          <textarea bind:value={editContent} style="font-family: var(--font-poppins);"></textarea>
                          <button on:click={() => saveEditTextBlock(index)}>Save</button>
                          <button on:click={cancelEdit}>Cancel</button>
                      {:else}
                          {block.content}
                          <button on:click={() => editTextBlock(index)}>Edit</button>
                      {/if}
                      <button on:click={() => removeTextBlock(index)}>Remove</button>
                  </p>
              {:else if block.type === 'parole'}
                  <div class="parole_rp">
                      {#if editIndex === index}
                          <textarea bind:value={editContent} style="font-family: var(--font-poppins);"></textarea>
                          <button on:click={() => saveEditTextBlock(index)}>Save</button>
                          <button on:click={cancelEdit}>Cancel</button>
                      {:else}
                          {block.content}
                          <button on:click={() => editTextBlock(index)}>Edit</button>
                      {/if}
                      <button on:click={() => removeTextBlock(index)}>Remove</button>
                  </div>
              {/if}
          {/each}
      </div>
      <div class="credit">Nana Pensionnat Kyoto</div>
  </div>
</div>

<button on:click={copyToClipboard}>Copier le code</button>
<button on:click={saveAllChanges}>Sauvegarder</button>

<div>
  <label>
      Couleur du background/parole:  
      <input type="color" bind:value={colorPrincipalRp} />
  </label>
  <label>
      Partenaire 1: 
      <input type="text" bind:value={imgPerso1} />
  </label>
  <label>
      Partenaire 2: 
      <input type="text" bind:value={imgPerso2} />
  </label>
  <label>
      Gif de la fiche: 
      <input type="text" bind:value={imgHeader} />
  </label>
  <label>
      Titre du rp: 
      <input type="text" bind:value={titleRp} />
  </label>
  <label>
      Feat: 
      <input type="text" bind:value={featRp} />
  </label>
  <label>
      Texte principal du rp: 
      <textarea bind:value={texteRp} rows="10" cols="50"></textarea>
  </label>
  <label>
      Ajout de nouveau texte:
      <textarea bind:value={newText} rows="3" cols="50"></textarea>
      <button on:click={() => addTextBlock('text')}>Ajouter Texte</button>
  </label>
  <label>
      Ajout de nouvelles paroles:
      <textarea bind:value={newParole} rows="3" cols="50"></textarea>
      <button on:click={() => addTextBlock('parole')}>Ajouter Parole</button>
  </label>
</div>