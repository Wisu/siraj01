<script>
  let name = '';
  let showButton = false;

  function handleClick() {
    // console.log('*1*');
    const img = document.getElementById('output');
    console.log('*2*', img);

    mobilenet.load().then(model => {
      // Classify the image.
      model.classify(img).then(predictions => {
        // console.log('Predictions: ', predictions);
        name = predictions[0].className
        showButton = false
      });
    });

    //  console.log('*3*');
  }

  function loadFile(event) {
   console.log('*loadFile.1*', event);
    showButton = true
    var output = document.getElementById('output');
    output.src = URL.createObjectURL(event.target.files[0]);
    console.log('*loadFile.2*');
  };

</script>

<hr />
<div class="file  has-name is-boxed">
  <label class="file-label">
    <input  class="file-input"
            type="file"
            name="resume"
            accept="image/*"
            on:change={loadFile} >
    <span class="file-cta">
      <span class="file-label">
        Choose a file…
      </span>
    </span>
  </label>
</div>

{#if showButton}
  <hr />
  <button on:click={handleClick}>
    Work on image
  </button>

{/if}

<hr />
<img id="output" alt=""/>


{#if name.length > 0}
    <h1>Image of: {name}!</h1>                 
{/if}

<hr />
