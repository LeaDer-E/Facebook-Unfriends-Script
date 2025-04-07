# Facebook-Unfriends-Script


```bash
// Delay function to pause execution after each step
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function unfriendPeople() {
  // Loop for up to 1000 friends
  for (let i = 1; i <= 1000; i++) {
    console.log(`Attempting to unfriend person number ${i}`);
    
    // Click on the person's menu button
    let personXPath = `/html/body/div[1]/div/div[1]/div/div[3]/div/div/div[1]/div[1]/div/div/div[4]/div/div/div/div/div/div/div/div/div[3]/div[${i}]/div[3]/div/div/div/i`;
    let personBtn = document.evaluate(personXPath, document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue;
    if (personBtn) {
      // Scroll the element into view before clicking
      personBtn.scrollIntoView({ behavior: "smooth", block: "center" });
      await delay(300); // Short delay to allow scrolling to finish
      personBtn.click();
    } else {
      console.log(`Could not find the person button for person number ${i}`);
      continue; // Move to the next person
    }
    
    // Short delay after clicking the person button
    await delay(500);
    
    // Click the "Unfriend" button
    let unfriendXPath = `/html/body/div[1]/div/div[1]/div/div[3]/div/div/div[2]/div/div/div[1]/div[1]/div/div/div/div/div/div/div[1]/div/div[3]/div[2]/div`;
    let unfriendBtn = document.evaluate(unfriendXPath, document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue;
    if (unfriendBtn) {
      unfriendBtn.scrollIntoView({ behavior: "smooth", block: "center" });
      await delay(300);
      unfriendBtn.click();
    } else {
      console.log(`Could not find the unfriend button for person number ${i}`);
      continue;
    }
    
    // Short delay after clicking the unfriend button
    await delay(500);
    
    // Click the "Confirm Unfriend" button
    let confirmXPath = `/html/body/div[1]/div/div[1]/div/div[4]/div/div/div[1]/div/div[2]/div/div/div/div/div/div/div[3]/div/div/div/div/div[1]/div`;
    let confirmBtn = document.evaluate(confirmXPath, document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue;
    if (confirmBtn) {
      confirmBtn.scrollIntoView({ behavior: "smooth", block: "center" });
      await delay(300);
      confirmBtn.click();
    } else {
      console.log(`Could not find the confirm button for person number ${i}`);
    }
    
    // Wait a little after confirmation to allow the interface to update
    await delay(1000);
  }
}

// Run the function
unfriendPeople();
```
