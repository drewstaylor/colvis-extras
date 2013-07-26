colvis-extras
=============

DataTables extension of the ColVis plugin (www.datatables.net/extras/colvis/) which allows for toggling button types and different menu layout integrations.


Button extensions are for Twitter Bootstrap buttons: <button class="btn">
For use with non-Bootstrap integrations add the following button classes to your CSS: 
"btn" (basic button class), "btn-group" (button class for button groups), "btn-primary" (Master menu button), 
"btn-danger" (red background button for closing the dropdown menu).

Extensions:  1) grid layout of colvis dropdown menu:
@property iMaxRows
@type     int
@default  -1
 
If you have a table with a lot of columns the user could get a scroll bar on the main ColVis 
dropdown menu, so it can be useful to get a grid layout the for menu items:

@example

    $(document).ready(function(){
        $("#example").dataTable({
            "sDom": "C<'clear'>lfrtip",
            "oColVis": { "iMaxRows": 3 } // Maximum of 3 buttons per column in menu items array. 
        });
    });

2) ColVis to "sDom":s text label insertion:
@property bLabel
@type     Array
@default  []
@property bLabelPost
@type     Array
@default  []
@property sLabel
@type     String
@default  Viewing options:

If colvis has it's own row in the sdom it can be nice to add a text label just outside of the <button>...</button> 
code. The label can get inserted before or after the ColVis menu button.  

@example

    $(document).ready(function(){
        $("#example").dataTable({
            "sDom": "C<'clear'>lfrtip",
            "oColVis": { "buttonText": "<span class='caret' />","sLabel": "Customize your view: ","bLabel": true } 
        }); 
    }); // "sLabel": define the text label 
        // "bLabel": true, displays sLabel before ColVis menu button, to display it after the menu button 
        // instead "bLabel" use "bLabelPost": true
        
3) Button to close the ColVis dropdown menu:
@property bClose
@type     Array
@default  []
@property sClose
@type     String
@default  "x"
 
To close the ColVis dropdown menu you click outside of the menu region, or by clicking the main button, or, 
to get nasty, by settting _fnCollectionHide() after the firing every menu action. This init param adds a button 
to close the dropdown menu, and it's always added as the last menu item.

@example

    // This option is turned on by default, to turn it off set bClose to false in your DataTables init:
    $(document).ready(function(){
        $("#example").dataTable({
            "sDom": "C<'clear'>lfrtip",
            "oColVis": { "bClose": false } 
        });
    });


    // Or, to change the text of the close button (default is "x"):
    $(document).ready(function(){
        $("#example").dataTable({
            "sDom": "C<'clear'>lfrtip",
            "oColVis": { "bClose": true, "sClose": "Close Menu" }	// Sets menu text to "Close Menu"
        });	// Alternatively, we could have injected html:
    });	// "sClose": "<i class="icon-search"></i>"

4) Add extra buttons section:
@property bExtras
@type     Array
@default  []

ColVis is a handy dropdown menu, so it can be useful to add extra buttons there to perform different operations 
than just showing and hiding columns in your DataTables. bExtras option allows you to create your own button 
sections. You'll need to do a little work defining the buttons and how many buttons you want inside bExtras, 
and you'll probably want to attach their sweet onclick functions.

@example

    //To get started you'll need to search colvis.extras.js for this string: "var arr = [ "button1", "button2", "button3"];"
    // Now if we change it  to: 
    var arr = [ "Public", "Hidden" ];
    // We set the button text as "Public" and "Hidden" and declare that these 2 buttons get added to our new menu section.


    //Then in our DataTables init:
    $(document).ready(function(){
        $("#example").dataTable({
            "sDom": "C<'clear'>lfrtip",
            "oColVis": { "bExtras": true } // Turns on new section
        });
        // Our "Public" and "Hidden" buttons get id attributes like this:
        $("#extrasbtn-1").click(function() {
            window.location.href = "start.php?page=inventory&filter=public";
        }); // example redirect 
        $("#extrasbtn-2").click(function() {
            window.location.href = "start.php?page=inventory&filter=hidden";
        }); // example redirect
    });		
    
5) Separator elements for the different button categories:
@param {object} 
@type function _fnColSeparate()

Html <hr> are automatically inserted between different button categories, i.e. bExtras, 
bClose, bShowAll, bRestore etc. as a visual aid to organizing the button types into categories.

To turn off <hr> separators comment out the lines like:

    nSpanHR = this._fnColSeparate();
    this.dom.collection.appendChild( nSpanHR );
