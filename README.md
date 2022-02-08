# Monty-Hall
A demo where you can try the Monty Hall problem. Copy and paste the code to your browser's devtools to try it out !

```javascript
let winTime = 0
const attempts = 1000

const doors = [
  { position: "left", hasCar: false, chosen: false, open: false },
  { position: "mid", hasCar: true, chosen: false, open: false },
  { position: "right", hasCar: false, chosen: false, open: false }
]

function chooseADoor() {
  const choice = Math.floor(Math.random() * doors.length)
  doors[choice].chosen = true
}

function openADoorThatIsNotChosenAndHasNoCar() {
  const remainingDoors = doors.filter(door => { return !door.chosen && !door.hasCar })
  const randomDoor = Math.floor(Math.random() * remainingDoors.length)
  const doorThatWillBeOpened = doors.indexOf(remainingDoors[randomDoor])
  doors[doorThatWillBeOpened].open = true
}

function chooseTheDoorThatIsNotOpened() {
  return doors.filter(door => { return !door.chosen && !door.open })[0]
}

function resetDoors(doors) {
  doors.forEach(door => {
    door.chosen = false
    door.open = false
  })
}

for (let i = 0; i < attempts; i++) {
  chooseADoor()
  openADoorThatIsNotChosenAndHasNoCar()
  const changedDoor = chooseTheDoorThatIsNotOpened()
  winTime += changedDoor.hasCar
  resetDoors(doors)
}

console.log("You won", winTime, "of", attempts, "attempts.")
```
