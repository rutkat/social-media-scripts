# Social Media Web Browser Scripts

In this article, I will teach you how to save time on social media platforms and boost your rankings with copy-and-paste scripts for the following:

## Table of Contents

[Youtube](#youtube)
[Facebook](#facebook)
[Quora](#quora)
[Twitter](#twitter)
[Medium](#medium)
[Soundcloud](#soundcloud)
[LinkedIn](#linkedin)
[Pinterest](#pinterest)

Original article regarding the use of these scripts [written here](http://runastartup.com/shortcuts-to-automate-your-likes-and-follows/).

## Youtube 
Like all the comments on video
```
// Click on a video to load its comments.
javascript:var inputs = document.getElementsByClassName('style-scope ytd-comment-action-buttons-renderer style-text size-default'); 
for (var i=0; i<inputs.length;i++) { 
	inputs[i].click(); 
}

```

## Facebook 
Like all visible posts in a group, not including comments and replies. 
```
// Navigate to a group https://www.facebook.com/groups/[groupname]
var inputs = document.querySelectorAll('[data-testid="UFI2ReactionLink"]')
for(var i=0; i<inputs.length; i++) { 
	if (inputs[i].children.length !== 0) {
	  //inputs[i].click(); 
	  console.log(i);
	}
}

// Auto-invite fan post
var buttons;
buttons = document.getElementsByClassName('_42ft');
for (var i = 0; i < buttons.length; i++) {
	if(buttons[i].getAttribute('ajaxify') != null){
		if(buttons[i].getAttribute('ajaxify').indexOf('invite') != -1){
			buttons[i].click();
		}
}
```

## Quora
Follow the followers of a given account and upvote all comments
```
// Follow followers
// Navigate to profile https://www.quora.com/profile/[username]/followers
var buttons = document.querySelectorAll('[role="button"]');
for (var i=0; i < 39; i++) {
	buttons[i].click();
}

// Upvote all comments
var buttons = document.querySelectorAll('[action_click="AnswerUpvote"]');
for (var i=0; i<buttons.length; i++) {
	buttons[i].click();
}
```

## Twitter 
Favorite tweets on a page, follow and unfollow accounts
```
// Favorite tweets on the page
a = setInterval(function () {
  window.scrollTo(0,document.body.scrollHeight);
  $('.ProfileTweet-actionButton.js-actionButton.js-actionFavorite:visible').click();
}, 1000)

// Follow daily limit 35
var FOLLOW_PAUSE = 1000;
var FOLLOW_RAND = 250; 
var PAGE_WAIT = 2000;
__cnt__ = 0; 
var f;
f = function() {
        var eles;
        var __lcnt__ = 0;
        eles = jQuery('.Grid-cell .not-following .follow-text').each(function(i, ele) {
                    ele = jQuery(ele);
                    if (ele.css('display') != 'block') {
                        console.trace('Already following: ' + i);
                        return;
                    }
                    setTimeout(function() {
                              console.trace("Following " + i + " of " + eles.length);
                            ele.click();
                            if ((eles.length - 1) == i) {
                                console.trace("Scrolling...");
                                window.scrollTo(0, document.body.scrollHeight);
                                setTimeout(function() {
                                    f();
                                }, PAGE_WAIT);
                            }
                    }, __lcnt__++ * FOLLOW_PAUSE + Math.random()*(FOLLOW_RAND) - FOLLOW_RAND/2);
                    __cnt__++;
        });
}
f();

// Unfollow
$('.ProfileCard-content').each(function() {
    var status = $(this).find('.FollowStatus').text();
    var unfollowButton = $(this).find('.user-actions-follow-button');
    if (status != 'follows you') {
        unfollowButton.click();
    }
});
```

## Medium 
Follow the followers of a given author
```
// Navigate to an author page
var inputs = document.getElementsByClassName('button--follow');
for (var i=0; i < 150; i++) { inputs[i].click(); }
```

## Soundcloud 
Follow users on a given user. Like all tracks on a given playlist
```
// Follow people of a Profile or Audio Track - daily limit 40
var inputs = document.getElementsByClassName('sc-button-follow sc-button sc-button-small sc-button-responsive'); 
for(var i=0; i < 39; i++) { inputs[i].click(); }

// Like all songs on playlist
var inputs = document.getElementsByClassName('sc-button-like sc-button sc-button-small sc-button-icon sc-button-responsive');
for(var i=0; i < inputs.length; i++) { inputs[i].click(); }
```

## LinkedIn 
Connect with people in the "people you may know" section
```

var currentSuccesfulConnections = 0;
var totalConnections = 0;
var totalInvitations = 0;
var inviteText = "";


function addConnection(connection) {
	var btn_type=connection.text().trim().split(' ')[0].trim();
	if (btn_type!=inviteText) {
		connection.trigger('click');
		currentSuccesfulConnections+=1;
	} else {
		totalInvitations+=1;
	}
}

function createConnections(text_invite,max_succesful_connections) {
	inviteText = text_invite;
	var connections=jQuery('.button-secondary-small');
	totalConnections=connections.size();
	if (max_succesful_connections==0) {
		max_succesful_connections=totalConnections;
	}
	connections.each(function(index, value) {
		if(currentSuccesfulConnections<max_succesful_connections){
			setTimeout(addConnection($(this)), index * 1000);
		} else {
			return false;
		}
	});
	
	console.log("Possible total connections: " + totalConnections);
	console.log("Succesful total connections: " + currentSuccesfulConnections);
	console.log("Total invitations avoided: " + totalInvitations);
} 
```


## Pinterest 
Follow accounts in a given category
```
var buttons = document.getElementsByClassName('RCK Hsu mix');
for(var i=0; i < 39; i++) { buttons[i].click(); }
```
