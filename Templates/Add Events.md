<%*
const plannerHeader = "## Day Planner"
const file = tp.file.find_tfile(`Journal/${tp.date.now("dddd, MMMM Do YYYY")}`)
 
var rxLogItem = /^([0-2][0-9]:[0-5][0-9] [a-zA-Z0-9]).*/
var rxTaskItem = /^- \[[ |x]\] [0-2][0-9]:[0-5][0-9] [a-zA-Z0-9].*/
var rxTime = /[0-2][0-9]:[0-5][0-9]/
var insertPosition = -1
var positionFound = -1
var index = 0
 
function isEarlier(t1, t2) {
    const r = t1 < t2 ? true : false
    return r
}
 
function isSame(t1, t2) {
    const r = t1.toString() == t2.toString() ? true : false;
    return r;
}
 
async function executeCommand(name) {
    const commandName = name;
    // Get command
    const commands = app.commands.listCommands();
    const collatorCompare = new Intl.Collator(["en"], {sensitivity: "base", usage: "search", ignorePunctuation: true}).compare;
    const command = commands.find(c => collatorCompare(c.name, commandName) === 0);
    // Execute
    await  app.commands.executeCommandById(command.id);
}
 
console.log('file: ' + file.path);
 
if (file) { // Does the file exist ?
    logItem = await tp.system.prompt("Event for Day Planner: (HH:mm event)")
 
    if (rxLogItem.test(logItem)) { // User input in correct format ?
        const content = (await app.vault.read(file)).split("\n")
        const rowNumberHeader = content.indexOf(plannerHeader)
 
        if (rowNumberHeader >= 0) { // Does the day planner header exist ?
            index = rowNumberHeader // then start checking from here
 
            // Find positionItem - Where to insert the log item
            let timeLogItem = rxTime.exec(logItem)
            do {
                positionFound = -1;
                index++
                let row = content[index]
                
                if (rxTaskItem.test(row)) {
                    let timeTask = rxTime.exec(row)
 
                    if (isSame(timeLogItem, timeTask)) {
                        console.log('same.')
                        new Notice("Entry already exists.")
                        positionFound = -1
                        break;
                    } else {
                        if (isEarlier(timeLogItem, timeTask)) {
                            positionFound = index
                        }
                    }
                } else {
                    positionFound = index
                    break;
                }
    
            }
            while (positionFound < 0)
    
            console.log('positionFound: ' + positionFound)
        
            if (positionFound > 0) {
                // insert entry
                let addContent = "- [ ] " + logItem
                content.splice(positionFound, 0 , addContent)
                await app.vault.modify(file, content.join("\n"))
                console.log('Task ' + logItem + ' added ' + ' in file ' + file.path + ' at position ' + positionFound)
 
                executeCommand()
            }
        } else {
            new Notice("Day Planner header not found");
        }
    } else {
        new Notice("Wrong task format (HH:mm event)")
    }
} else {
    new Notice("Todays daily note does not exist.")
}   
-%>