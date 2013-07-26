colvis-extras
=============

DataTables extension of the ColVis plugin (www.datatables.net/extras/colvis/) which allows for toggling button types and different menu layout integrations.

/*
 * 				Button extensions are for Twitter Bootstrap buttons; i.e.  <button class="btn">
 * 				For use with non-Bootstrap integrations add the following button classes to your CSS: 
 * 				"btn" (basic button class), "btn-group" (button class for button groups), "btn-primary" (Master menu button), 
 * 				"btn-danger" (red background button for closing the dropdown menu).
 *
 * Extensions:	- grid layout of colvis menu (via iMaxRows param):
 * 
 * 				$(document).ready(function(){
 *			    	$('#example').dataTable({
 *				        "sDom": 'C<"clear">lfrtip'
 * 						"oColVis": { "iMaxRows": 3 } // Gives a layout of 3 buttons per column in ColVis dropdown menu. 
 *				    });
 *				});
 * 
 * 				- colvis text label (via sLabel and bLabel params):
 * 
 * 				If colvis has it's own row in the sdom it can be nice to add a text label outside of the button <span>. 
 * 				By default text label appears before menu button. Move lines 398-402 down to line 410 if you want text label 
 * 				to appear after the button or create a new instance of _fnTextLabel(). 
 * 				 
 * 				$(document).ready(function(){
 *			    	$('#example').dataTable({
 *				        "sDom": 'C<"clear">lfrtip'
 * 						"oColVis": { "buttonText": "<span class='caret' />" "sLabel": "Customize your view: ","bLabel": true } 
 *				    }); // Creates a textless button with only a caret down arrow inside and prefixes it with the text strting 
 * 						// from the sLabel param
 *				});		// "sLabel" param is how to define what the text label says 
 * 						// "bLabel": true is how you turn on the feature 
 * 
 * 				- close button (via bClose param)
 * 
 * 				It's not always intuitive to close the ColVis dropdown menu by clicking outside the menu region or by
 * 				settting _fnCollectionHide() to close the main menu after every menu action. This is especially true for large
 * 				tables when a user wishes to turn on/off column visibilty of many columns without re-opening the main menu after
 * 				each show/hide action. The bClose extension adds a red close button as the very last (i.e. bottom-right) menu item 
 * 				enabling the user to close the ColVis menu via a button.
 * 
 * 				This option is turned on by default. To turn it off set bClose to false:
 * 				
 * 				$(document).ready(function(){
 *			    	$('#example').dataTable({
 *				        "sDom": 'C<"clear">lfrtip'
 * 						"oColVis": { "bClose": false } 
 *				    });
 *				});
 * 
 * 				By default the close button is a red button containing a lowercase "x"
 * 				To change the button text for the close button:
 * 				
 * 				$(document).ready(function(){
 *			    	$('#example').dataTable({
 *				        "sDom": 'C<"clear">lfrtip'
 * 						"oColVis": { "bClose": true,  } 
 *				    });
 *				});
 * 				
 * 
 * 				- extra developer buttons (via bEtxras param):
 * 
 * 				Colvis is a handy dropdown and it can be useful to add extra buttons there to perform different operations than
 * 				simply showing and hiding columns. The bExtras extension allows developers to do this by offering the template. 
 * 				You'll need to a little work defining the button text and how many buttons you want (see line 625 of this file),
 * 				and to attach their onclick functions.
 * 				
 * 				In line 625 of this file:
 * 
 * 				var arr = [ "Public", "Hidden" ]; // Sets button text for bExtras and declares how many buttons get added
 * 				
 * 				In DataTables init file:
 * 
 * 				$(document).ready(function(){
 *			    	$('#example').dataTable({
 *				        "sDom": 'C<"clear">lfrtip'
 * 						"oColVis": { "bExtras": true } // Turns on extra buttons section
 *				    });
 * 					
 * 					// extras buttons always get id attributes like this: <button id="extrasbtn-1" />
 * 					$("#extrasbtn-1").click(function() {
 * 						window.location.href = "index.php?page=inventory&filter=public";
 *					}); // example redirect to public inventory 
 *					
 *					$("#extrasbtn-2").click(function() {
 * 						window.location.href = "index.php?page=inventory&filter=hidden";
 *					}); // example redirect to hidden inventory
 *				});		
 * 
 * 				- sectional separators (uses _fnColSeparate() function)
 * 
 * 				Extension will automatically insert <hr> separators between different button categories; i.e. bExtras, 
 * 				bClose, bShowAll, bRestore etc. for an overall neater and more organized look.
 * */

