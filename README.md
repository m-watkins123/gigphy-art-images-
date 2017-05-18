# gigphyy
<html lang="en">

<head>
  <meta charset="utf-8">
  <title> Giphtastic</title>
</head>
<h1><strong>GIFS</strong></h1>
  <button data-person="Bill Gates">Success is a lousy teacher. It seduces smart people into thinking they can't lose.
</button>
  <button data-person="Albert Einstin">
    Creativity is contagious pass it on
  </button>

  <button data-person="Donald Trump">
   Sometimes by losing a battle you find a new way to win the war.
  </button>

  <button data-person="Kurt Cobain">
    Wanting to be someone else is a waste of the person you are.

  </button>

  <button data-person="Bruce Lee">
    Knowledge will give you power, but character respect.

  </button>

  <div id="gifs-appear-here">
  </div>

  <script src="http://code.jquery.com/jquery-2.1.3.min.js"></script>
  <script type="text/javascript">
    // Event listener for all button elements
    $("button").on("click", function() {
      // In this case, the "this" keyword refers to the button that was clicked
      var person = $(this).attr("data-person");
      var queryURL = "http://api.giphy.com/v1/gifs/search?q=" +
        person + "&api_key=dc6zaTOxFJmzC&limit=10";
     
      $.ajax({
          url: queryURL,
          method: "GET"
        })
       
        .done(function(response) {
          
          var results = response.data;
          
          for (var i = 0; i < results.length; i++) {
            
            if (results[i].rating !== "r" && results[i].rating !== "pg-13") {
              
              var gifDiv = $("<div class='item'>");
              
              var rating = results[i].rating;
             
              var p = $("<p>").text("Rating: " + rating);
             
              var personImage = $("<img>");
              
              personImage.attr("src", results[i].images.fixed_height.url);
              gifDiv.append(p);
              gifDiv.append(personImage);
              
              $("#gifs-appear-here").prepend(gifDiv);
            }
          }
        });
    });
  </script>
</body>

</html>
