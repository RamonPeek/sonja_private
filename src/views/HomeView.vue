<template>
  <Questionare :category="nextQuestionWithCategory.category" :currentQuestion="nextQuestionWithCategory.question" @answered="data => storeAnswer(data)"/>
</template>

<script>
// @ is an alias to /src
import Questionare from '@/components/Questionare.vue'

export default {
  name: 'HomeView',
  components: {
    Questionare
  },
  computed: {
    nextQuestionWithCategory() {
      for (const category of this.categories) {
        for (const part of category.parts) {
          part.answers = part.answers.sort((a, b) => (a.order > b.order) ? 1 : -1)
          if (!part.answerValue) {
            return {
              category: this.categoryWithoutQuestions(category),
              question: part
            };
          }
        }
      }
      return null; // Return null if all questions have been answered
    }
  },
  methods: {
    categoryWithoutQuestions(category) {
      var copy = JSON.parse(JSON.stringify(category));
      delete copy.parts;
      return copy;
    },
    storeAnswer(data) {
      var targetCategory = this.categories.find(x => x.id == data.categoryId);
      if(targetCategory) {
        var targetQuestion = targetCategory.parts.find(x => x.id == data.questionId);
        if(targetQuestion) {
          targetQuestion.answerValue = data.answerValue;
          console.log(targetQuestion);
        }
      }
    }
  },
  data() {
    return {
      categories: [
        {
          id: "xaKdnM5LjgVQ",
          title: "Sociaal",
          color: {
            r: 229,
            g: 129,
            b: 39
          },
          parts: [
            {
              id: "L4F7xD6z8qxn",
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
              id: "cQaUmYBtZe9g",
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
              id: "Vfbg1T0YWinc",
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
              id: "PuF3MgztVST6",
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
              id: "MqdARhH15dcy",
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
              id: "pJ2q9nDXrcMp",
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
          id: "huGjugQn5FCu",
          title: "Denk- en leerstijl",
          color: {
            r: 232,
            g: 85,
            b: 49
          },
          parts: [
          {
            id: "eXSx8MWQTjhy",
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
              id: "nZ74xV7YM1uu",
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
              id: "kTFRXuaNLRUB",
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
              id: "9RgCvdrphzeY",
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
              id: "RmkcNxyDiLd6",
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
              id: "iDH9HPASFct9",
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
          id: "4juaw6c1FGzk",
          title: "Fysiek",
          color: {
            r: 238,
            g: 59,
            b: 95
          },
          parts: [
          {
            id: "6YZfcHEX78Sf",
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
              id: "0TJfibHaiv5X",
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
            }
          ]
        }
      ]
    }
  }
}
</script>
