<!-- index.html -->
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Music & Concentration Test</title>
  <style>
    body {
      background-color: #999;
      font-family: 'Comic Sans MS', cursive, sans-serif;
      color: black;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
    #app {
      text-align: center;
      padding: 20px;
    }
    .button, .age-button {
      background-color: transparent;
      border: 2px solid black;
      border-radius: 30px;
      padding: 10px 20px;
      font-size: 1.2em;
      margin: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div id="app">
    <h1 id="title">Does Music Affect<br>Memory & Concentration?</h1>
    <button class="button" id="startButton"><strong>HELP ME GATHER INFO</strong></button>
    <div class="subtitle center">
      <p>Please respond accurately. This means not to guess. Your result will be used as data for a project for OCSEF, which requires precise and accurate information to prove further research.</p>
    </div>
  </div>

  <script>
    const app = document.getElementById('app');

    const paragraph1 = `Bees are small flying insects known for their role in pollination and honey production. They live in organized colonies, with a queen, worker bees, and drones each having specific roles. The queen lays eggs, while worker bees gather nectar, make honey, and care for the hive. Bees use their fuzzy bodies to transfer pollen from flower to flower, helping plants reproduce. Their buzzing sound comes from rapidly beating wings that also allow them to hover and change direction mid-air. Bees communicate through a special waggle dance that shows the direction and distance to food. Despite their tiny size, they are vital to ecosystems and agriculture. Without bees, many fruits, vegetables, and nuts would become scarce. Bees face threats from pesticides, habitat loss, and climate change. Protecting them means supporting a balanced and healthy environment for all living things. There are over 20,000 known species of bees, ranging from the common honeybee to solitary species like the mason bee. Each species plays a unique role in its ecosystem, with some specializing in pollinating specific types of plants. Bumblebees, for example, are especially good at pollinating crops like tomatoes through a process called buzz pollination. Bees have excellent memory and can recognize human faces and specific flowers. Their sense of smell is incredibly sensitive, allowing them to find nectar even in low concentrations. Honeybees produce wax from glands on their abdomen to construct intricate honeycombs for storing honey and raising young. A single bee can visit thousands of flowers in a day. Despite their hard work, honeybees only produce about a twelfth of a teaspoon of honey in their lifetimes. Many plants depend entirely on bees for pollination, making these insects essential for biodiversity. Urban beekeeping has become popular in recent years, helping increase awareness about the importance of bees. Beekeepers must monitor hives for diseases like colony collapse disorder, which has caused major bee population declines. Some governments have introduced bans on harmful pesticides to help protect pollinators. Flower-rich gardens and wildflower strips along fields offer bees safe feeding areas. Education about bees in schools and communities helps encourage conservation. By planting native flowers and reducing chemical use, individuals can contribute to the survival of bee populations.`;

    const paragraph2 = `Lena, a clever inventor, and Kai, a daring sky-pilot, lived in a floating city above the clouds. One morning, Lena discovered a map hidden inside an old mechanical bird she'd been repairing. The map pointed to the lost island of Aerith, said to hold the secrets of ancient sky energy. Eager for adventure, Kai fueled up his airship, and they set off into the unknown. Storms battered their path, forcing Lena to jury-rig a broken wing with a lightning rod and spare brass gears. Wind howled through the rigging as Kai fought the controls, his eyes fixed on the swirling horizon. They passed through pockets of strange weather—sudden hail, eerie calm, and even flashes of green lightning. At night, Lena studied the map by lantern light, tracing forgotten symbols etched in silver ink. They encountered a flock of iron-feathered sky-crows, which nearly shredded their balloon canopy before Kai veered into a tunnel of clouds. As they reached the storm’s eye, a massive cloud serpent rose from the mist, guarding the entrance to Aerith. Lena distracted it with a flash bomb while Kai dove through a narrow canyon of clouds. The serpent’s roar echoed through the sky, shaking the airship’s hull. Safely inside, they found Aerith glowing with bioluminescent vines and levitating stones. Strange birds with translucent wings circled above, singing haunting melodies in the wind. The island’s gravity shifted unpredictably, forcing Lena and Kai to tread carefully across floating platforms. In the heart of the island, a temple pulsed with power, sealed by an ancient puzzle. Lena deciphered the symbols while Kai kept watch for danger. Each symbol glowed as it clicked into place, releasing a hum that vibrated the very air. Just as they solved the final piece, the serpent returned enraged. It crashed through the outer walls of the temple, shattering columns of crystal. Kai fought it off with aerial maneuvers, while Lena retrieved a crystal humming with energy. She clung to the deck as the ground trembled and Aerith began to collapse into itself. With the island collapsin,g they escaped moments before it vanished into the clouds. A wave of wind pushed them higher, and they soared silently for a moment in the open blue. Back home, the crystal powered their city for a generation. The city’s engines sang a new song, brighter and steadier than before. The two friends stood at the edge of the skyport, already dreaming of the next adventure. As the sun dipped behind the clouds, their silhouettes stood tall against the orange light, hearts alight with discovery.`;

    function showAgeSelection() {
      app.innerHTML = '<h2>Select Your Age Group</h2>';
      const ageGroups = ['<10', '11–14', '15–18', '19–25', '26–35', '36-39', '40+'];
      ageGroups.forEach(age => {
        const btn = document.createElement('button');
        btn.className = 'age-button';
        btn.textContent = age;
        btn.onclick = showFirstParagraph;
        app.appendChild(btn);
      });
    }

    function showFirstParagraph() {
      app.innerHTML = `
        <h2>Please read the paragraph</h2>
        <p>${paragraph1}</p>
        <button class="button" onclick="showUntitled()">Finished</button>
      `;
    }

    function showUntitled() {
      app.innerHTML = `
        <h2> Quiz Time! </h2>
   <p>The quiz is in this form. Please fill it out: <a href="https://forms.gle/kHMc6pUioEaJ1YB48" target="_blank">https://forms.gle/kHMc6pUioEaJ1YB48</a></p>
        <button class="button" onclick="showMusicInput()">Continue</button>
      `;
    }

    function showMusicInput() {
      app.innerHTML = `
        <h2>Enter a YouTube Link for music</h2>
        <input id="songInput" type="text" placeholder="Paste YouTube video link">
        <button class="button" onclick="playMusicAndShowParagraph()">Submit</button>
      `;
    }

    function playMusicAndShowParagraph() {
      const url = document.getElementById('songInput').value.trim();
      const videoId = extractYouTubeID(url);
      if (!videoId) {
        alert("Please enter a valid YouTube link.");
        return;
      }
      const embedUrl = `https://www.youtube.com/embed/${videoId}?autoplay=1`;

      app.innerHTML = `
        <h2>Please read the paragraph</h2>
        <p>${paragraph2}</p>
        <iframe width="300" height="180" src="${embedUrl}" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
        <br><br>
        <button class="button" onclick="showUntitled2()">Finish</button>
      `;
    }

    function showUntitled2() {
      app.innerHTML = `
        <h2>Quiz Time!</h2>
   <p>The quiz is in this form. Please fill it out: <a href="https://forms.gle/yv8Eh8jJyBjKx5LHA" target="_blank">https://forms.gle/yv8Eh8jJyBjKx5LHA</a></p>
        <button class="button" onclick="showResults()">Finish</button>
      `;
    }

    function showResults() {
      app.innerHTML = `
        <h2>Thank You!</h2>
        <p>Your results have been recorded. Please fill out this Google Form as a reflection: <a href="https://forms.gle/oB5qqu6SjsipHaNt8" target="_blank">https://forms.gle/oB5qqu6SjsipHaNt8</a></p>
        <p>Your result will help us understand the effect of music on concentration and memorization.</p>
        <br>
        <button class="button" onclick="goToMainMenu()">Back to Main Menu</button>
      `;
    }

    function goToMainMenu() {
      app.innerHTML = `
        <h1 id="title">Does Music Affect<br>Concentration?</h1>
        <button class="button" id="startButton"><strong>HELP ME GATHER INFO</strong></button>
        <div class="subtitle center">
          <p>Please respond accurately. This means not to guess. Your result and response will be used as data for a project for OCSEF, which requires precise information to prove further research.</p>
        </div>
      `;
      document.getElementById('startButton').onclick = showAgeSelection;
    }

    function extractYouTubeID(url) {
      const regex = /(?:youtube\.com.*(?:\?|&)v=|youtu\.be\/)([^&]+)/;
      const match = url.match(regex);
      return match ? match[1] : null;
    }

    document.getElementById('startButton').onclick = showAgeSelection;
  </script>
</body>
</html>
