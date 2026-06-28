# Quran
<!DOCTYPE html>
<html>
<head>
<title>Quran App</title>
</head>

<body>

<h1>📖 Quran App</h1>

<button onclick="loadSurahs()">Show 114 Surahs</button>

<div id="quran"></div>


<script>

async function loadSurahs(){

let response = await fetch("https://api.alquran.cloud/v1/surah");

let data = await response.json();

let output = "";

data.data.forEach(surah => {

output += `
<h2>${surah.number}. ${surah.englishName}</h2>

<button onclick="openSurah(${surah.number})">
Read Surah
</button>

<hr>
`;

});

document.getElementById("quran").innerHTML = output;

}



async function openSurah(number){

let arabic = await fetch(
"https://api.alquran.cloud/v1/surah/"+number+"/ar.alafasy"
);

let english = await fetch(
"https://api.alquran.cloud/v1/surah/"+number+"/en.asad"
);


let arData = await arabic.json();
let enData = await english.json();


let text = "<h1>"+arData.data.name+"</h1>";


arData.data.ayahs.forEach((ayah,index)=>{

text += `

<p>
<b>${ayah.numberInSurah}</b><br>

${ayah.text}

<br>

Translation:
<br>

${enData.data.ayahs[index].text}

<br>

<audio controls>
<source src="${ayah.audio}" type="audio/mpeg">
</audio>

</p>

<hr>

`;

});


document.getElementById("quran").innerHTML=text;

}


</script>
<fooster>
    <h1>Created by Awwal Smith Adedapo</h1>
</fooster>
<img src="one.png" alt="My Photo">


</body>
</html>
