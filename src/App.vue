<template>
  <div class="one-pager">
    <div class="content">
      <div v-if="currentPage !== 4">
        <div v-for="(question, index) in currentPageData.questions" :key="index">
          <h2>{{ question.question }}</h2>
          <ul>
            <li v-for="(option, i) in question.options" :key="i">
              <input type="radio" :name="'question_' + index" :value="option" v-model="question.selectedOption">
              {{ option }}
            </li>
          </ul>
        </div>
        <button v-if="currentPage !== 0" @click="prevPage">Zurück</button>
        <button v-if="currentPage !== pages.length - 1" @click="nextPage">Weiter</button>
      </div>
      <div v-else>
        <h2>Herzlichen Glückwunsch!</h2>
        <p>Dein Eignungstest hat eine Eignung von 93% ergeben.</p>
        <p>Empfohlene Karrierepfade: Wärmepumpeninstallateur</p>
        <button @click="goToLernbereich">Zum Lernbereich</button>
        <button @click="showInfo">Info</button>
      </div>
    </div>
    <footer>
      <nav class="breadcrumbs">
        <ul>
          <li v-for="(page, index) in pages" :key="index" :class="{ active: index === currentPage }">{{ index + 1 }}</li>
        </ul>
      </nav>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pages: [
        {
          "title": "Sprachkenntnisse Deutsch",
          "questions": [
            {
              "question": "Haben Sie Interesse daran, die deutsche Sprache zu lernen?",
              "options": {
                "a": "Ja, ich bin sehr daran interessiert.",
                "b": "Ich bin nicht sicher, ob es mir wichtig ist.",
                "c": "Nein, ich habe kein Interesse daran."
              },
              "selectedOption": null,
              "correctOption": "a"
            },
            {
              "question": "Haben Sie bereits Grundkenntnisse in der deutschen Sprache?",
              "options": {
                "a": "Ja, ich habe bereits Grundkenntnisse.",
                "b": "Nein, ich habe keine Vorkenntnisse.",
                "c": "Ich bin mir unsicher."
              },
              "selectedOption": null,
              "correctOption": "a"
            },
            {
              "question": "Welche Motivation treibt Sie an, Deutsch zu lernen?",
              "options": {
                "a": "Berufliche Weiterentwicklung",
                "b": "Persönliches Interesse an der deutschen Kultur",
                "c": "Verbesserte Kommunikation im Alltag"
              },
              "selectedOption": null,
              "correctOption": "a"
            }
          ]
        },
        {
          "title": "Erfahrung und Affinität zum Handwerk",
          "questions": [
            {
              "question": "Haben Sie bereits Erfahrung in handwerklichen Tätigkeiten?",
              "options": {
                "a": "Ja, ich habe bereits in handwerklichen Berufen gearbeitet.",
                "b": "Nein, ich habe bisher keine praktische Erfahrung gesammelt.",
                "c": "Ich habe einige Erfahrungen, aber keine professionelle Ausbildung."
              },
              "selectedOption": null,
              "correctOption": "a"
            },
            {
              "question": "Welche handwerklichen Fähigkeiten besitzen Sie?",
              "options": {
                "a": "Schreinern/Tischlern",
                "b": "Elektrik/Elektronik",
                "c": "Metallverarbeitung/Schweißen",
                "d": "Sanitärinstallation",
                "e": "Malerarbeiten/Streichen"
              },
              "selectedOption": null,
              "correctOption": ["a", "b", "c", "d", "e"]
            },
            {
              "question": "Welchen handwerklichen Bereich würden Sie gerne weiterentwickeln?",
              "options": {
                "a": "Holzbearbeitung",
                "b": "Metallverarbeitung",
                "c": "Elektrotechnik",
                "d": "Sanitärinstallation",
                "e": "Bauarbeiten"
              },
              "selectedOption": null,
              "correctOption": ["a", "b", "c", "d", "e"]
            }
          ]
        },
        {
          "title": "Motivation als Fachkraft in Deutschland zu arbeiten",
          "questions": [
            {
              "question": "Was reizt Sie besonders an einer Tätigkeit als Fachkraft in Deutschland?",
              "options": {
                "a": "Die vielfältigen Karrieremöglichkeiten",
                "b": "Die hohe Arbeitsqualität und Standards",
                "c": "Die Wertschätzung für Handwerksberufe in der Gesellschaft"
              },
              "selectedOption": null,
              "correctOption": ["a", "b", "c"]
            },
            {
              "question": "Welche Erwartungen haben Sie an das Arbeitsumfeld in Deutschland?",
              "options": {
                "a": "Eine gute Work-Life-Balance",
                "b": "Fortschrittliche Technologie und Ausstattung",
                "c": "Weiterbildungsmöglichkeiten und Aufstiegschancen"
              },
              "selectedOption": null,
              "correctOption": ["b", "c"]
            },
            {
              "question": "Wie wichtig ist Ihnen die Anerkennung Ihrer handwerklichen Fähigkeiten in Deutschland?",
              "options": {
                "a": "Sehr wichtig, sie motiviert mich zusätzlich.",
                "b": "Weniger wichtig, solange ich meine Arbeit gut mache.",
                "c": "Ich habe keine klare Meinung dazu."
              },
              "selectedOption": null,
              "correctOption": ["a"]
            },
            {
              "question": "Welche Rolle spielen für Sie die Arbeitsbedingungen und das Arbeitsklima in Deutschland?",
              "options": {
                "a": "Eine sehr wichtige Rolle, sie beeinflussen meine Zufriedenheit am Arbeitsplatz.",
                "b": "Eine eher unwichtige Rolle, solange ich meinen Job gut machen kann.",
                "c": "Ich bin mir unsicher."
              },
              "selectedOption": null,
              "correctOption": ["a"]
            }
          ]
        }
      ],
      currentPage: 0
    };
  },
  computed: {
    currentPageData() {
      return this.pages[this.currentPage];
    }
  },
  methods: {
    nextPage() {
      this.currentPage++;
    },
    prevPage() {
      this.currentPage--;
    }
  }
};
</script>

<style scoped>
/* Globale Stile */
* {
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

/* Stil für die Komponente */
.one-pager {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

header {
  background-color: #007bff;
  color: #fff;
  padding: 20px;
  border-radius: 10px 10px 0 0;
}

h1 {
  margin: 0;
  font-size: 24px;
}

nav ul {
  list-style: none;
  padding: 0;
  margin-top: 10px;
}

nav ul li {
  display: inline-block;
  margin-right: 10px;
}

nav ul li button {
  background: none;
  border: none;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  transition: color 0.3s ease;
}

nav ul li button:hover {
  color: #f0f0f0;
}

.header-menu {
  margin-top: 10px;
}

.header-menu li {
  display: inline-block;
  margin-right: 10px;
}

.header-menu li button {
  background: none;
  border: none;
  color: #fff;
  cursor: pointer;
  transition: color 0.3s ease;
}

.header-menu li button:hover {
  color: #f0f0f0;
}

.content {
  padding: 20px;
  color: #1a1a1a;

  ul {
    list-style: none;
    li {
      text-align: left;
    }
  }
}

ul {
  padding: 0;
}

h2 {
  margin-top: 20px;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

footer {
  background-color: #007bff;
  color: #fff;
  padding: 20px

;
  border-radius: 0 0 10px 10px;
}

.breadcrumbs {
  text-align: center;
}

.breadcrumbs ul {
  padding: 0;
}

.breadcrumbs ul li {
  display: inline-block;
  margin-right: 5px;
  color: #fff;
  font-weight: bold;
}

.breadcrumbs ul li.active {
  color: #f0f0f0;
}
</style>

