De debug problemen:

Bug exercise 1: als het woord goed geraden is, verlies je alsnog
eerste tests:
code aangepast naar max 1 guess en 1 woordkeuze om sneller te kunnen testen.
in Gameover component bij return statement de win en looseResulkts omgedraaid:
nu komt ook de tweede keus naar voren:
Wordguessed is dus steeds FALSE  
 Wordguessed als variable {}in de <p> gezet<P>
Naar app.js gegaan om de props te checken : daar zie ik een typo : een s mist wordGuessed op (line 31)

Bug exercise 2: w
we kunnen geen letter raden
als eerste ga ik naar GuessLetterHandler en check in DEVtools of state binnenkomt bij „guessedLetters „
currentChosenLetters komt wel binnen bij State maar slaat niet op naar de state van [guessedLetters]
ik ga eerst kijken in App.js en TextINPUT via de props kom ik uit bij guessLetterHandler => de state komt niet binnen bij de IF statement van guessedLetters want hier mist een S
[...this.state.guesedLetters];

Bug exercise 3:
als we het spel starten is het meteen gewonnen
start gelijk met „gameover“ : gameover lijkt dus gelijk „true“
eerste idee: omdat het spel gelijk gewonnen is moet ook „wordGuessed“ ergens meteen op true staan :
getest door win en looseresult om te draaien : dit klopt! Dus code loopt goed door tot einde
ik comment de gameover component uit om te testen : if statement ( App.js regel 26 ) op false gezet en nu komt het beginscherm van de game wel gelijk tevoorschijn : dus 1e deel van probleem is gevonden
ik lees dat remaieing gelijk staat aan de guessedLetters en dat is bij begin een lege Array: [] de oplossing moet hier zijn is NIET gelijk : const remaining = word.filter(letter => !guessedLetters.includes(letter) );
code geïssoleerd door paar x te testen met alleen het woord “ vis “

Bug exercise 4:
als het input veld leeg is dan kunnen we alsnog die "letter" raden
t getest :
logica: eerst ga zoeken in de DEVtools : komen de letters binnen bij de wrongly guessed ? Letters in App container functie „guessLetterHandler “ mist de statement om dubbele keuzes te filteren : const inputGiven = this.state.currentChosenLetter.length > 0;
const newLetter = !this.state.guessedLetters.includes(
this.state.currentChosenLetter
);
if (inputGiven && newLetter) {
const newGuessedLetters = [...this.state.guessedLetters];
newGuessedLetters.push(this.state.currentChosenLetter);
this.setState({
guessedLetters: newGuessedLetters
});

Bug exercise 5:
je kan blijven raden tot -1 guesses
ik zoek eerst in de HTML daar de {} in de <p><p>waar deze berekeing wordt gedaan : ik zie dat de props {props.maxGuesses} en {props.wrongLetters.length} deze waarde maken
in de code gekeken naar de maxGuesses : ik heb de maxGuesses aangepast naar 1 en dan komt het zelfde resusltaat : -1 guesses:
omdat dit gebeurd ná voltooing van de guesses kijk ik als eerst in const isGameOver :
ook test ik weer met juiste woord : dan klopt het wel : dus het gebeurd alleen bij verliezen : dus wanneer maxGuesses wordt overschreden : ik zie bij de tweede if statement line29 in App.js dat true wordt gegeven wanneer guessedletters array GROTER mag zijn dan de maxGuesses: ik vermoed dat het ook isGelijk aan moet zijn dus op line 28 : if
(getWrongLetters (game.chosenWord, game.guessedLetters).length >=game.maxGuesses
dit klopt

Bug exercise 6:
je kunt dezelfde letter meerdere keren raden (let op: dit is een nieuwe feature!)
logischerwijs wordt de letter niet gecheckt bij het invoeren dus zit de fout in State en het ‚toelaten‘ van nieuwe letters
als eerst kijk ik bij de guessLetterHandler en lees zie in de code bij de if statement maar 1 const: if (inputGiven) en deze gaat alleen maar over de length van currentChosen letter.. hier mist code die ook moet zeggen dat hij niet gelijk is aan een andere letter : die haal ik uit de andere code die wel werkte..:) :const newLetter = !sthis.state.guessedLetters.includes(
this.state.currentChosenLetter) dan wordt de if statement op line 46 van AppContainer.js if(inputGiven && newLetter )
# deBugging_Hangman_game
