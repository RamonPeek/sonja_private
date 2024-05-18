<template>
  <div>
    <Chart :data="chartData" :options="chartOptions" :key="updateKey"></Chart>
  </div>
  
</template>

<script>
import { Chart } from 'vue-chartjs';
import {
Chart as ChartJS,
CategoryScale,
LinearScale,
PointElement,
LineElement,
Title,
Tooltip,
Legend,
TimeScale,
RadialLinearScale,
ArcElement
} from 'chart.js';

export default {
  components: {
    Chart
  },
  created() {
    ChartJS.register(
 CategoryScale,
 LinearScale,
 PointElement,
 LineElement,
 TimeScale,
 RadialLinearScale,
 ArcElement,
 Title,
 Tooltip,
 Legend
);
  },
  mounted() {
    let allLabels = [];
    let allData = [];
    let fullData = [];
    this.categories.forEach(category => {
      var colorToggle = true;
      category.parts.forEach(part => {
        allData.push(Math.floor(Math.random() * (5 - 1 + 1)) + 1);
        fullData.push(5);
        this.chartData.datasets[0].backgroundColor.push("rgba(0,0,0,0.5)");
        this.chartData.datasets[0].borderColor.push("rgba(0,0,0,1)");

        if(colorToggle) {
          this.chartData.datasets[1].backgroundColor.push("rgba(" + category.color.r + "," + category.color.g + "," + category.color.b + ", 1)");
          this.chartData.datasets[1].borderColor.push("rgba(" + category.color.r + "," + category.color.g + "," + category.color.b + ", 1)");
        }else{
          this.chartData.datasets[1].backgroundColor.push("rgba(" + category.color.r + "," + category.color.g + "," + category.color.b + ", .8)");
          this.chartData.datasets[1].borderColor.push("rgba(" + category.color.r + "," + category.color.g + "," + category.color.b + ", .8)");
        }

        allLabels.push(part.question);
        colorToggle = !colorToggle;    
      });
    });
    this.chartData.labels = allLabels;
    this.chartData.datasets[0].data = allData;
    this.chartData.datasets[1].data = fullData;

    this.chartOptions = {
      // Customize options as per your requirement
      // For example:
      responsive: true,
      elements: {
        point: {
          radius: 4,
          hoverRadius: 4, // ex.: to make it bigger when user hovers put larger number than radius.
        },
      },
      maintainAspectRatio: true,
      animation: {
                    animateScale: true
                },
      plugins: {
        legend: {
          display: false
        },
        tooltip: {
          callbacks: {
              label: function() {
                return "";
              }
          },
          displayColors: false,
          position: 'nearest'
        },
      },
      scales: {
        r: {
            max: 5,
            min: 0,
            ticks: {
                stepSize: 1,
                display: false
            },
        }
    },
    }
    this.updateKey++;
  },
  data() {
    return {
      updateKey: 0,
      categories: [
        {
          title: "Sociaal",
          color: {
            r: 229,
            g: 129,
            b: 39
          },
          parts: [
            {
              title: "Assertiviteit",
              question: "Houdt rekening met iedereen, maar is zelf moeilijk peilbaar en komt niet op voor zichzelf. Als dat nodig is, is de reactie overdreven heftig, verdedigend of volhardend in eigen gelijk.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Asynchroniteit",
              question: "Komt (veel) ouder of jonger over dan leeftijdgenoten en/of speelt met jongere/oudere kinderen. Loopt soms ver voor, maar kan andere dingen niet, die je op deze leeftijd moet kunnen.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Assertiviteit",
              question: "Houdt rekening met iedereen, maar is zelf moeilijk peilbaar en komt niet op voor zichzelf. Als dat nodig is, is de reactie overdreven heftig, verdedigend of volhardend in eigen gelijk.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Gebrek aan peers",
              question: "Vindt moeilijk aansluiting in de klas, is een buitenbeentje. Kán erbij horen, maar daarvoor moet hij/zij wel erg zijn best doen. Kind speelt een rol en relaties zijn niet gelijkwaardig.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Kopieergedrag",
              question: "Past zich (soms extreem) aan aan de kinderen waar het mee omgaat. Is heel hard bezig om in de groep niet op te vallen en kopieert gedrag dat niet echt bij het kind zelf past.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Conflicten",
              question: "Heeft snel ruzie met andere kinderen (soms heel onverwacht) en kan ruzies moeilijk rustig uitpraten. Kan anderen onterecht dingen verwijten, blijft oude koeien uit de sloot halen.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            }
          ]
        },
        {
          title: "Denk- en leerstijl",
          color: {
            r: 232,
            g: 85,
            b: 49
          },
          parts: [
          {
              title: "Asynchroon leren",
              question: "Kan soms grote leersprongen maken en in begrip verder zijn dan de lesstof. Oefent niet mee, maar beheerst het later wel. Denkt breder / verder vooruit en stelt verstorende vragen.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Leerhiaten",
              question: "Maakt soms vreemde fouten of lijkt oude stof/methodiek voor het eerst te horen. Wordt boos als je aanmoedigt (‘je kan/weet het wel’). Vindt alles ‘stom’ of ‘saai’ en doet het gewoon niet.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Topdown leren",
              question: "Begrijpt stof pas als het ‘hele plaatje’ wordt uitgelegd. Losse stukjes stof blijven niet hangen, het kind blijft vragen eromheen stellen - niet uit nieuwsgierigheid maar uit verwarring.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Beelddenken",
              question: "Doorziet nieuwe stof snel en intuïtief, maar valt uit op regels die niet logisch zijn, zoals klok kijken, links en rechts of spelling. Kan moeite hebben met verwerken van talige informatie.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Autonomie",
              question: "Doet nooit gewoon wat je vraagt (wil op eigen manier), onderhandelt over ruimte binnen de opdracht en wil weten waarop je beoordeelt (positief/negatief). Blokkeert op stappenplannen.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Creatief denken",
              question: "Is opvallend creatief met een grote fantasie, maar kan bij vakken ook vastlopen als het te origineel/associatief denkt. Kan vastlopen op meerkeuze-vragen of afhaken op herhaling.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
          ]
        },
        {
          title: "Fysiek",
          color: {
            r: 238,
            g: 59,
            b: 95
          },
          parts: [
          {
              title: "Motoriek",
              question: "Heeft een onleesbaar handschrift en levert onverzorgd werk af. Heeft een houterige motoriek, laat vaak dingen vallen en kan niet vangen. Spant bij het schrijven de tong aan.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Energieverdeling",
              question: "Kan het ene moment heel energiek zijn, op het andere moment afwezig en moe. Kan gedurende de dag niet op een gemiddeld niveau presteren, maar altijd met pieken en dalen.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Nachtrust",
              question: "Komt ‘s morgens al moe de klas in, kan bijna in slaap vallen als de stof niet prikkelend genoeg is. Kan zelf ook aangeven lang wakker te liggen. Na vakanties zie je een ander kind.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Overgevoeligheid",
              question: "Heeft zichtbare (rode ogen, hoesten) of onzichtbare allergieklachten (buikkrampen) of is overgevoelig voor voedingsstoffen. Probeert soms inspanning en situaties te vermijden.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Gemiste beperkingen",
              question: "Laat wisselende resultaten zien, afhankelijk van de plek in de klas of de situatie (drukte). Verstaat of leest dingen soms verkeerd en kan proberen beurten / bord lezen te vermijden.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Somatiseren/spanning",
              question: "Blijft vaak ziek thuis, klaagt ook op school over hoofdpijn, buikpijn of spierpijn (zonder oorzaak). Reageert fysiek op ruzies of toetsdruk. Kan emoties niet goed verwoorden.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
          ]
        },
        {
          title: "Fysiek",
          color: {
            r: 157,
            g: 80,
            b: 157
          },
          parts: [
          {
              title: "Onderprikkeling",
              question: "Kan ‘uit’ gaan in de les of erg druk worden, in elk geval niet normaal opletten. Soms zie je zelfregulatie (tekenen/wiebelen). Kan ongepaste prikkels zoeken, komt dan vaak jong over.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Overprikkeling",
              question: "Kan op ‘standby’ gaan om zich af te sluiten voor prikkels, en dan ook de les missen. Kan ook sterkere prikkels opzoeken en geluiden maken. Kan zo maar explosief reageren.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
            {
              title: "Lage drempel",
              question: "Heeft last van dingen die andere kinderen niet opmerken (krassen, tikken). Kan vreemd, boos of bang reageren in ‘normale’ situaties, vooral als je het niet serieus neemt.",
              answers: [
                {
                  order: 1,
                  text: "ja, en dit zorgt voor veel onbegrip en frustratie",
                  value: 1
                },
                {
                  order: 2,
                  text: "ik zie dit soms of in lichte mate",
                  value: 2
                },
                {
                  order: 3,
                  text: "nee, dit is me echt nog nooit opgevallen",
                  value: 3
                }
              ]
            },
          ]
        }
      ],
      chartData: {
        datasets: [{
          type: 'radar',
          data: [], // Sample data for progress in percentage
          labels: [],
          backgroundColor: [
          ],
          borderColor: [
          ],
          borderWidth: 2
        },
        {
          type: 'polarArea',
          data: [], // Sample data for progress in percentage
          labels: [],
          backgroundColor: [
          ],
          borderColor: [
          ],
          borderWidth: 1
        }]
      },
      chartOptions: {}
    };
  }
};
</script>
