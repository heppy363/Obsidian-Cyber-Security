### Grafico uso dei tag in percentuale
```dataviewjs
const tags = {};
dv.pages().file.tags.forEach(t => { tags[t] = (tags[t] || 0) + 1; });

const sorted = Object.entries(tags).sort((a, b) => b[1] - a[1]);
const labels = sorted.map(t => t[0]);
const counts = sorted.map(t => t[1]);

const chartConfig = {
    type: 'bar',
    data: {
        labels: labels,
        datasets: [{
            label: 'Uso dei Tag',
            data: counts,
            backgroundColor: 'rgba(153, 102, 255, 0.5)',
            borderColor: 'rgb(153, 180, 255)',
            borderWidth: 1
        }]
    },
    options: {
        indexAxis: 'y', // Barre orizzontali per leggere meglio i nomi
        scales: {
            x: { beginAtZero: true }
        }
    }
};

window.renderChart(chartConfig, this.container);
```


### Grafico Radar
```dataviewjs
// 1. Definiamo quali tag vogliamo ESCLUDERE (perché sono stati, non argomenti)
const tagDaEscludere = ["#Completed", "#TO-DO", "#In-Progress", "#immagini", "#Immagini"];

const tagsMap = {};
dv.pages().file.tags.forEach(t => {
    // Filtriamo: carichiamo il tag solo se non è nella lista nera
    if (!tagDaEscludere.includes(t)) {
        tagsMap[t] = (tagsMap[t] || 0) + 1;
    }
});

// 2. Prendiamo i Top 8 (più di 10 in un radar creano confusione visiva)
const topTags = Object.entries(tagsMap)
    .sort((a, b) => b[1] - a[1])
    .slice(0, 8); 

const labels = topTags.map(t => t[0].replace("#", "")); // Togliamo il # per pulizia
const data = topTags.map(t => t[1]);

// 3. Configurazione estetica migliorata
const chartConfig = {
    type: 'radar',
    data: {
        labels: labels,
        datasets: [{
            label: 'Distribuzione Conoscenza',
            data: data,
            backgroundColor: 'rgba(0, 255, 187, 0.2)', // Colore neon più moderno
            borderColor: 'rgba(0, 255, 187, 1)',
            borderWidth: 3,
            pointBackgroundColor: '#fff',
            pointRadius: 4
        }]
    },
    options: {
        scales: {
            r: {
                grid: { color: 'rgba(255, 255, 255, 0.1)' }, // Griglia sottile
                angleLines: { color: 'rgba(255, 255, 255, 0.1)' },
                suggestedMin: 0,
                ticks: { 
                    display: false, // Nascondiamo i numeri ammassati al centro
                    stepSize: 5 
                },
                pointLabels: {
                    font: { size: 14, weight: 'bold' },
                    color: '#e0e0e0'
                }
            }
        },
        plugins: {
            legend: { display: false } // Pulizia totale
        }
    }
};

window.renderChart(chartConfig, this.container);
```

