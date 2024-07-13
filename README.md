# YouTube Watch Later Playlist Cleaner
```js
const iterator = document.evaluate(
  `//*[@id="contents"]/ytd-playlist-video-renderer`,
  document,
  null,
  XPathResult.ORDERED_NODE_SNAPSHOT_TYPE,
  null);

console.log(`Found ${iterator.snapshotLength} videos in the WL playlist, removing...`)

function clickItem(index) {
  // Exit function if index is out of range
  if (index >= iterator.snapshotLength) return;
  
  // Find and click the menu action button
  iterator.snapshotItem(index).querySelector("button").click();
  
  // Find and click the "Remove from Watch later" (3rd button)
  document.querySelector("#items > ytd-menu-service-item-renderer:nth-child(3)").click();

  // Call the function recursively with the next index after 1 second
  setTimeout(() => clickItem(index + 1), 1000);
}

// Start clicking items with index 0 after 1 second
setTimeout(() => clickItem(0), 1000);
```

## Description
This script helps you clear all videos from your YouTube "Watch Later" playlist automatically.

## Usage
1. Go to your YouTube "Watch Later" playlist.
2. Open the developer console (F12 or right-click > Inspect > Console).
3. Paste the script into the console and hit Enter.
4. The script will start removing videos one by one.

## FAQ

### For Normal Users

**Q: What does this script do?**  
**A:** This script clears all videos from your YouTube "Watch Later" playlist automatically.

**Q: How do I use this script?**  
**A:** To use the script, open your browser's developer console while on the YouTube "Watch Later" playlist page, paste the script, and hit Enter.

**Q: Is it safe to use this script?**  
**A:** Yes, the script only interacts with your YouTube "Watch later" playlist and doesn't collect or transmit any data.

**Q: Will this script work on any browser?**  
**A:** The script should work on most modern browsers that support JavaScript and have a developer console, including Chrome, Firefox, and Edge.

**Q: What if the script stops working?**  
**A:** If the script stops working, it may be due to changes in YouTube's page structure. Please check for an updated version of the script on this repository.

### For Developers

**Q: How does the script identify videos in the "Watch Later" playlist?**  
**A:** The script uses an XPath expression to find all elements that represent videos in the playlist.

**Q: What is the purpose of the `clickItem` function?**  
**A:** The `clickItem` function recursively clicks the menu and remove buttons for each video in the playlist to remove them one by one.

**Q: Why is there a delay (setTimeout) in the script?**  
**A:** The delay ensures that each video is removed one at a time and allows the page to update between actions, preventing the script from overwhelming the browser or YouTube's servers.

**Q: Can the script be optimized or improved?**  
**A:** Yes, developers are welcome to suggest improvements or optimizations. Contributions can be made via pull requests.

**Q: What are potential issues with using this script?**  
**A:** Potential issues include changes in YouTube's HTML structure, which might break the XPath queries, and browser-specific limitations or restrictions on automated actions.
