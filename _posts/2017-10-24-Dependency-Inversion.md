---
layout: post
title: Dependency Inversion Principle
tags: ["SOLID"]
---
![Dependency Inversion screen image](/images/di-solder.jpg)

There is a poster using the "motivational poster meme" for each one of the SOLID principles. Some of them are OK, but this one conveys the points of the Dependency Inversion Principle (DIP) very well. The DIP states that *high level modules should not depend on low level modules, they should both depend on abstractions. Abstractions should not depend on details. Details should depend upon abstractions.*

On the poster, you can imagine that you wouldn't hardwire or solder a lamp to the existing eletrical work. The higher level lamp shouldn't depend on a direct connection to the low level wiring. There should be an abstraction or an interface (like a 3 prong plug). If the wiring had to be replaced, we could simply work on the electrical components behind the plug (interface) and nothing on the lamp would have to change. Clients implementing that interface wouldn't have to worry about the low level details of the actual wiring in the wall.

Let's imagine a bit of code where we are creating a tic tac toe game. The game class will be responsible for creating two players, the board, and running the game.

{% highlight ruby %}

class Game
  attr_reader :player1, :player2, :current_player

  def initialize(player1, player2)
    @player1 = player1
    @player2 = player2
    @current_player = player1
    @board = Board.new
  end

  def toggle_player
    #changes the player turns
  end

  def game_over?
    #determines if the game should continue
  end

  def winner
    #returns the winner
  end

end
{% endhighlight %}

It makes sense that the game can do things like run the game by alternating player turns, tell us when the game is over, and tell us the winner. One small but subtle dependency that gets created is that when we initialize the game, we depend on the board. If there are any changes to the board, like if we added required parameters to the board, then the game class would have to change. The game (higher level module), shouldn't be dependent on the board (lower level module). We can resolve this by using dependency injection to remove the coupling between the game initialization and the board. When we initialize the game, we'll provide it with everything it needs to run the game including an instance of the board.


{% highlight ruby %}

class Game
  attr_reader :player1, :player2, :current_player

  def initialize(player1, player2, board)
    @player1 = player1
    @player2 = player2
    @current_player = player1
    @board = board
  end

{% endhighlight %}

This small but subtle change helps us remove the coupling between the game and the board and changes the direction of the dependency to comply with the DIP. Now the game can worry about running the game (taking turns and determining if the game is over) and not worry about lower level details like the board used for the game.
