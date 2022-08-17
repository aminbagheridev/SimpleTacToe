
![Logo](https://github.com/bagheriamin/SimpleTacToe/blob/main/simpletactoe%20banner.png?raw=true)


# SimpleTacToe

A simple TicTacToe game, with Multipeer framework connectivity, meaning two players can play against each other locally on two different devices!

## Technologies Used

**Tech Stack:** 
UIKit, Multipeer Connectivity, UserDefaults

**Architecture:**
MVC

**Swift:** Auto-Layout w/ Storyboards, Protocol+Delegate Pattern, Async/Sync Programming

**UIKIT:**
MCBrowserViewControllerDelegate, MCSessionDelegate, UIPanGestureRecognizer, UIPresentationController, MCAdvertiserAssistant


## Demo Of Local Multiplayer Mode
![Alt Text](https://github.com/bagheriamin/SimpleTacToe/blob/main/askajfkajfkjadfsf.gif?raw=true)



## Slide Up View Controller

To create the settings view controller, I wanted to have a cool slide up animation, and so I didn't opt for the standard 'segue to a new view controller', which would have been the easy way out.

![](https://github.com/bagheriamin/SimpleTacToe/blob/main/slideViewContrller.gif?raw=true)

In order to implement this feature, I did some digging and I found out I had to use Apples UIPresentationController. 

It is normally taken care of under the hood by apple, but as it says in the official apple documentation,
if we would like to have ***custom*** view controller presentations, we would have to use a custom style like so:
```
viewController.modalPresentationStyle = .custom
```

![](https://github.com/bagheriamin/SimpleTacToe/blob/main/appleDocumentationOnUIPresentationViewController.png?raw=true)
*Apple Official Documentation*

**Implementation Step One**

First thing I did was create a custom Implementation of the UIPresentationController, which I configured to achieve the task at hand.

Things such as the blur effect, the actual height of the view and rounded corners were all implemented via code.
```
class PresentationController: UIPresentationController {
    \\ Insert custom code here
    ...
}
```
**Implementation Step Two**

Then I created a XIB file, as seen below.

![](https://github.com/bagheriamin/SimpleTacToe/blob/main/xib.png?raw=true)

**Implementation Step Three**

I then connected this XIB file to the actual class that manages the button switch and the *slide down to dismiss* feature. 

**Implementation Final Step**

Finally, now that I have a custom way to present a view controller (*UIPresentationController*), and I have actually created the View Controller i want to present, all I need to do is implement this extension to my main, Single Player View Controller class.

![](https://github.com/bagheriamin/SimpleTacToe/blob/main/carbon-8.png?raw=true)

So, the moment we've been waiting for. To present the OverlayViewController (*The VC with the Easy Mode switch*), this is what we must implement:

![](https://github.com/bagheriamin/SimpleTacToe/blob/main/carbon-9.png?raw=true)

We set the modal presentation style to custom, we set the extension delegate we made earlier to self, and then we presented the OverlayViewController. Simple!







## Local Multipeer Connectivity Explanation

To implement the Local Multipeer Connectivity Framework, the real challenge was in making sure every device could only play when it was really their turns.

Lets walk through how the whole process works.

**Multipeer Part One**

When a user presses the connect button in the nav bar, the user get's presented with the option to either **host** a game, or **join** a game. If **join** is pressed, the user is presented with the device finder screen, where they can join their freinds. If they press **host**, they start sending out their signal for others to find.

![](https://github.com/bagheriamin/SimpleTacToe/blob/main/hostOrJoin.gif?raw=true)

**Multipeer Part Two**

Once two players are connected, I make sure that whenever the connected player (the device that joined) selects a square, it freezes his own screen and sends a signal through to the host, which causes his own screen to unfreeze.

When the host selects a square, it causes his screen to refreeze, and then sends a signal to the joined player, unfreezing his screen, allowing him to play.

Of course, after every button tap, the code that I've written goes through all the possible combinations of tictactoe wins (*and trust me, there's a LOT*), and then depending on who won (or didn't), either keeps the game playing or causes both players boards to freeze, displaying a *Player Won!* message.

## Single player and multiplayer?

Aside from the local multiplayer and the swipe up screen, the single player or 'same-device' multiplayer gamemodes aren't anything mind blowing. Just 9 buttons and a bunch of different if / else checks.

Some cool things however were the fact that I built the entire UI with Autolayout, which did end up turning into Constraint hell, leading me to learn how to do programmatic UI's later on.



## Installation

Download the project via Code > Download as ZIP

    
