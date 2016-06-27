# like-dislike

A simple jQuery plugin that allows you to create a rating bar with two buttons: Like and Dislike.

- See [demos](http://uagrace.github.io/like-dislike)


## Installation

If you use [Bower](http://bower.io/search/?q=like-dislike), you can type into the command line prompt in your project folder:

`$ bower install like-dislike` 

Or press "Download ZIP" button on the main GitHub page to get all the files and manually add them to your project.


## Preparation

Add the jQuery and like-dislike into your document:

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js"></script>
<script src="like-dislike-master/js/like-dislike.min.js"></script>
```


## Usage

```html
<div id="rating">
  <button class="like">Like</button>
  <span class="likes">0</span>
  <button class="dislike">Dislike</button>
  <span class="dislikes">0</span>
</div>

<script type="text/javascript">
  $('#rating').likeDislike({
    reverseMode: true,
    initialValue: 0,
    click: function(value, btnType, event) {
      var self = this;

      // locks the buttons
      self.readOnly(true);

      $.ajax({ // sending data to the server
        url: '/url',
        type: 'post',
        data: 'id=1&value=' + value,
        dataType: 'json',
        success: function (data) {
          $(self).find('.likes').text(data.likes);
          $(self).find('.dislikes').text(data.dislikes);
          
          // unlocks the buttons
          self.readOnly(false);
        }
      });
    }
  });
</script>
```


## Options

```javascript

// the callback function 'click' called when you press on one of the buttons
click: null, // function(value, btnType, event) {}

// the callback function 'beforeClick' called before 'click'
beforeClick: null, // bool function(event) {}

// sets initial value (0, 1 or -1)
initialValue: 0, // integer

// initializes the plugin with locked or unlocked buttons
readOnly: false, // boolean

// allows to cancel the vote
reverseMode: false, // boolean

// sets the class name of the Like button
likeBtnClass: 'like', // string

// sets the class name of the Dislike button
dislikeBtnClass: 'dislike', // string

// sets the class name of the active button
activeClass: 'active', // string

// sets the class name of the disabled button
disabledClass: 'disabled', // string

```

## Methods

`readOnly(state)` locks or unlocks buttons, depending on the `state` param.