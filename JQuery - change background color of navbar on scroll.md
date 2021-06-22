## Code:
```js
<script src="https://code.jquery.com/jquery-3.6.0.min.js" integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" crossorigin="anonymous"></script>
<script>
    $(document).ready(function(){
      $(window).scroll(function() { // check if scroll event happened
        if ($(document).scrollTop() > 50) { // check if user scrolled more than 50 from top of the browser window
			$(".navbar").css("background-color", "rgba(255,255,255,0.24)"); // if yes, then change the color of class "navbar" to your selected color
			$(".navbar").css("transition", "all 0.5s"); // setting transition time to get beautiful fadein / fadeout effect
		} else {
			$(".navbar").css("background-color", "transparent"); // if not, change it back to transparent
        }
      });
    });
</script>
```
## Demo:
<img src="https://github.com/mehediishere/FrontEnd-Development/blob/48522404d6b242b8de0c7e35af634ce782cf7db0/Images/navbar.gif" alt="navbar" width="100%" height="auto">
