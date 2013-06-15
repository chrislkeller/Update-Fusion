### Script to sync a Google SpreadSheet to a Fusion Table

* Head to Google docs, create a spreadsheet and add some data to it. Simple enough right? Just make sure that Column A has data in it. It seems blank or null values will break the update function. Though if other columns are without data the script appears to work fine. At some point, I'll learn to add an error message if Column A is blank, but for now, Column A wants data.

![Google spreadsheet](http://archives.chrislkeller.com/blog-images/2012/01/37380956-2012-01-31_11h24_34.png)

* Now I'm going to create a Fusion Table based off my spreadsheet. I do this either by importing from Google Docs or downloading the spreadsheet as a csv and uploading it to Fusion Tables. **It is important to note** from the outset that the column names must match between the spreadsheet and the table. Remember, if you change a column name or add a column to the spreadsheet, be sure to change it/add it to the Fusion Table as well. For good measure I make sure any new columns are also in the same order.

![Fusion Table Import](http://archives.chrislkeller.com/blog-images/2012/01/37380957-2012-01-31_11h25_24.png)

* After my Fusion Table is created, I need to get the Encrypted Table ID in order to make sure the spreadsheet can access it. To find the Encrypted Table ID I click File --> About this table. I'll copy this somewhere in a text file until I need it.

* I'm almost ready to make this happen, but I'm going to need one other piece of information - a Google Fusion Tables API key. I need to turn on access to the Fusion Tables API in Google's API console, and get an authentication key. Don't worry, this is much easier than it sounds.

* First, head to the [API Console dashboard](https://code.google.com/apis/console/) and log in with your Google account if prompted. The first screen you see if an overview. If it's your first time here, you might not see a lot. On the left-side of the screen you'll see a dropdown where you can create a new project. Go ahead and create one and give it a name.

![Fusion Table Import](http://archives.chrislkeller.com/blog-images/2013/apis-console.png)

* Next click on Services on the left-side of the screen and you will see a heck of a lot of toggles that can turn on various Google APIs. Scroll down a bit until you find Fusion Tables API, and flip to toggle to the 'On' position.

![Fusion Table Import](http://archives.chrislkeller.com/blog-images/2013/apis-services.png)

* Finally, click on API Access on the left-side of the screen. You will see two main areas: Authorized API Access and Simple API Access. We're interested in the API Key shown under Simple API Access. I'll copy this somewhere in a text file next to my Encrypted Table ID.

![Fusion Table Import](http://archives.chrislkeller.com/blog-images/2013/api-console-key.png)

* Now we're ready to add our script to our spreadsheet. Back at your spreadsheet, go to Tools --&gt; Script Editor and paste the [script code](https://gist.github.com/3013360). I add my Fusion Table's encrypted table ID to the top of the script...

		// Add the encrypted table ID of the fusion table here
		var tableIDFusion = '17xnxY......';

* Then I add my API key.

		// key needed for fusion tables api
		var fusionTablesAPIKey = '17xnxY......';

* Click save. You will be prompted to give the project a name. "Update Fusion Tables" works. Click the save icon or go to File --&gt; Save.

* Reload the spreadsheet and you will see a new menu item next to help. Mine says "Data Update Functions." Click the menu item and you will see three options, though the names may differ at this point: "Change Range of Data to be Sent (Include Headers)", "Update Fusion Table" & "Change Email Information."

![](http://archives.chrislkeller.com/blog-images/2012/01/37380960-2012-01-31_11h30_49.png)

9. First choose "Change Email Information." This will authenticate your gmail account to access the Fusion Table. **Note**: I HAVE NOT had success using this with a Google Apps account going to a private Gmail account. Click the couple of confirmation buttons that appear.

10. Second you should select all of the data -- columns and rows -- you wish to sync and choose Change Range of Data to be Sent (Include Headers)". I usually just click the rectangle in the upper-left corner to sync everything. The beauty -- in my experience -- is that blank rows and columns can be synced but they won't be reflected on the Fusion Table. Click the two confirmation buttons that appear.

![](http://archives.chrislkeller.com/blog-images/2012/01/37380963-2012-01-31_11h35_44.png)

11. Now just add some information to your spreadsheet and click "Update Fusion Table." Your spreadsheet data should be synced with your Fusion Table.

![](http://archives.chrislkeller.com/blog-images/2012/01/37380965-2012-01-31_11h40_29.png)

12. Sit back and enjoy this moment … unless it didn't work. Perhaps you received an error message like:

		Request failed for https://www.googleapis.com/fusiontables/v1/query?key=ajhdndna8282n29& returned code 403. Server response: { "error": { "errors": [ { "domain": "usageLimits", "reason": "accessNotConfigured", "message": "Access Not Configured" } ], "code": 403, "message": "Access Not Configured" } }

Which might just mean that your API key isn't active yet… Or you might receive an error because you didn't authenticate with the application when prompted. There are a lot of moving parts and little details to pay attention to, and I'm sure I've overlooked something in this walkthrough.

If you get stuck and things just aren't working, let me know and I'll see what I can do.