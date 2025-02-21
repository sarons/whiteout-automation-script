# Gift Code Automation Script Guide

This guide will help you run a script to automatically redeem gift codes for alliance members or friends (multiple player IDs).

## Opening Chrome Console

1. Open Google Chrome browser and go to https://wos-giftcode.centurygame.com/
2. Press `Ctrl + Shift + J` (Windows/Linux) or `Cmd + Option + J` (Mac) to open the console<br />
   Alternatively, you can:
   - Right-click anywhere on the webpage
   - Select 'Inspect' from the menu
   - Click on the 'Console' tab at the top of the panel
4. When pasting the script, if Chrome shows "Allow paste" message, type `allow pasting` and press Enter then paste the script again. If no message appears, you can paste directly

## Customizing the Script

### To change Player IDs:
```js
playerIds = [123456789, 123456666, 1234567777, 123456788, 123456999]
```
Replace numbers with your Player IDs, keeping commas between them. Example: [111111, 222222, 333333]

### To change Gift Code:
```js
giftCode = 'woshjm25'
```
Replace 'woshjm25' with your code, keeping the quotes. Example: 'newcode123'

## Running the Script

1. Copy the entire script below:
```js
playerIds = [123456789, 123456666, 1234567777, 123456788, 123456999]
giftCode = 'woshjm25'

const setInput = (id,val) => { 
    input = document.querySelector(`[placeholder="${id}"]`)
    input.value = val
    input.dispatchEvent(new Event('input', {
        bubbles: true,
        cancelable: true
    }))
}

async function executeSequence(playerId, giftCode) {
    console.log('Processing playerId:', playerId)
    // Set player ID and wait briefly for input to register
    setInput('Player ID', playerId);
    await new Promise(resolve => setTimeout(resolve, 1000));

    // Click login and wait for login to complete
    document.querySelector('.login_btn')?.click();
    await new Promise(resolve => setTimeout(resolve, 2000));

    // Set gift code and wait briefly for input to register
    setInput('Enter Gift Code', giftCode);
    await new Promise(resolve => setTimeout(resolve, 1000));

    // Click each button sequentially with delays
    for (const button of ['.exchange_btn', '.confirm_btn', '.exit_icon']) {
        document.querySelector(button)?.click();
        await new Promise(resolve => setTimeout(resolve, 1500));
    }
    console.log('Completed playerId:', playerId)
}

async function processAll() {
    // Process each playerId sequentially
    for (const playerId of playerIds) {
        await executeSequence(playerId, giftCode);
    }
}

processAll()
```
2. Paste it into the Chrome Console
3. Press Enter to run then sit back and watch the magic happen
4. Watch the console for progress messages:
   - You'll see "Processing playerId: (number)" when it starts processing an ID
   - You'll see "Completed playerId: (number)" when it finishes processing an ID

## Important Notes

- Don't close or switch tabs while the script is running
- The script will process one player ID at a time
- Wait until you see all "Completed" messages before closing the console
- If you need to stop the script, refresh the page

## Troubleshooting

If the script isn't working:
- Make sure you're on the correct webpage
- Check that you haven't accidentally removed any commas or brackets
- Try refreshing the page and running the script again
- Ensure all player IDs are correct and valid
