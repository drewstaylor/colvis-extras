colvis-extras
=============

colvis-extras.js is an extension of the ColVis plugin for DataTables (www.datatables.net/extras/colvis/)
Among other things, it allows for toggling button types and different menu layout integrations.


Button extensions are based on Twitter Bootstrap buttons. For use with non-Bootstrap integrations add these button 
classes to your ColVis CSS: "btn" (basic buttons), "btn-group" (groups of buttons), "btn-primary" (ColVis menu button, 
sShowAll, bRestore), "btn-danger" (bClose).

<strong><b>Grid menu layout</b></strong>

If you have a table with a lot of columns the user could get a scroll bar on the main ColVis 
dropdown menu so it can be useful to get a grid layout for the menu items

@example

    $(document).ready(function(){
        $("#example").dataTable({
            "sDom": "C<'clear'>lfrtip",
            "oColVis": { "iMaxRows": 3 } // Maximum of 3 buttons per column in menu items array. 
        });
    });

<hr />

<strong><b>ColVis to "sDom":s text label insertion</strong></b>

If colvis has it's own row in the sdom it can be nice to add a text label just outside of the button node. This text label can get inserted before or after the ColVis menu button.  

@example

    $(document).ready(function(){
        $("#example").dataTable({
            "sDom": "C<'clear'>lfrtip",
            "oColVis": { "buttonText": "<span class='caret' />","sLabel": "Customize your view: ","bLabel": true } 
        }); 
    }); // "sLabel": define the text label 
        // "bLabel": true, displays sLabel before ColVis menu button, to display it after the menu button 
        // instead "bLabel" use "bLabelPost": true

<hr />

<strong><b>Button to close the ColVis dropdown menu</b></strong>

To close the ColVis dropdown menu you click outside of the menu region, or by clicking the main button, or, 
to get nasty, by settting _fnCollectionHide() after every menu action is triggered. These init param will add a button 
to close the dropdown menu. It's always added as the last button in the array.

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
    });	// "sClose": "<i class="icon-close"></i>"

<hr />

<strong><b>Add an extra buttons section</b></strong>

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

<hr />
    
<strong><b>Separator elements for button categories</b></strong>

Html hr tags are automatically inserted between different button categories, i.e. bExtras, 
bClose, bShowAll, bRestore etc. as a visual aid to organizing the button types into categories.

To turn off hr tag separators comment out the lines like these:

    nSpanHR = this._fnColSeparate();
    this.dom.collection.appendChild( nSpanHR );
