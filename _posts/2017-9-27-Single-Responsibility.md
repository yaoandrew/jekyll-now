---
layout: post 
title: Applying the Single Responsibility Principle 
tags: ["solid"] 
---
![Multi Tool image](/images/multitools.jpg)


The Single Responsibility Principle says things that change for the same
reasons should be grouped together and things that change for different
reasons should be separated. Responsibility in this context should be
thought of as a reason for change. Prior to reading more about the SRP,
I assumed it meant that my class has one function. Instead, we should be
asking ourselves- what is the single reason why our class would change?

Given this construct, when examining the structure of my tic tac toe game,
there are a number of things I would change. When I first began, it made
sense that we needed a board class whose responsibility it would be to
keep state and tell me things about the board. Turns out using the word
"and" was a smell I should have picked up on. My board looked like this:

{% highlight ruby %} 
class Board 

  EMPTY_CELL = '-'

  attr_accessor :cells, :turn

  def initialize(cells=nil, turn= "X")
    @size = 3
    @cells = cells || Array.new(@size**2, EMPTY_CELL)
    @turn = turn
  end 

  def length
    @cells.length
  end

  def display_cell(cell)
    @cells[cell]
  end

# some more methods

end
{% endhighlight %}

I had a data structure to hold the contents of the board, keep track of who's turn it was, and some other methods to change the state of the board. The mistake I made was including the `display_cell` method on the board instead of placing it in the UI class. I had assumed that the board class would tell me all sorts of things about the board including displaying the cell contents. We can clean this up by moving the responsibility of displaying what is on the board to the UI class. 

Additionally, my board class tells me things about the board. Here are some more methods in the board class:

{% highlight ruby %} 

  def rows
    @cells.each_slice(@size).to_a
  end

  def columns
    @cells.each_slice(@size).to_a.transpose
  end

  def main_diagonal
    0.step(@cells.length - 1, @size + 1 ).map { |x| @cells[x] }
  end

  def anti_diagonal
    (@size - 1).step(@cells.length - @size, @size - 1).map { |x| @cells[x] }
  end

  def diagonals
    [main_diagonal, anti_diagonal]
  end

  def row_winner?
    rows.any? { |row| row.all? { |x| row[0] == x && x != EMPTY_CELL }}
  end

  def column_winner?
    columns.any? { |column| column.all? { |x| column[0] == x && x != EMPTY_CELL }}
  end

  def diagonal_winner?
    diagonals.any? { |diagonal| diagonal.all? { |x| diagonal[1] == x && x != EMPTY_CELL }}
  end

  def tied?
    @cells.all? { |cell| cell != EMPTY_CELL } && !any_winner?
  end

  def any_winner?
    row_winner? || column_winner? || diagonal_winner?
  end

  def who_won
    if column_winner?
      columns.find { |column| column.all? { |x| column[0] == x } }.first
    elsif row_winner?
      rows.find { |row| row.all? { |x| row[0] == x } }.first
    elsif diagonal_winner?
      diagonals.find { |diagonal| diagonal.all? { |x| diagonal[0] == x } }.first
    end
  end

{% endhighlight %}

There are some methods to give me a collection of the rows, columns, and diagonals. There are also some methods that analyze those collections to see if there are winning rows, columns, or diagonals. You could definitely make the argument that some of this logic could be contained in a BoardEvaluator class. I could see this looking something like this:

{% highlight ruby %}
class BoardEvaluator
  
  def row_winner?(board)
    board.rows.any? { |row| row.all? { |x| row[0] == x && x != EMPTY_CELL }}
  end

  def column_winner?(board)
    board.columns.any? { |column| column.all? { |x| column[0] == x && x != EMPTY_CELL }}
  end

  def diagonal_winner?(board)
    board.diagonals.any? { |diagonal| diagonal.all? { |x| diagonal[1] == x && x != EMPTY_CELL }}
  end

end
{% endhighlight %}

I'll definitely be cleaning up this class in the next refactor. We can see a clear violation of the Single Responsibility Principle with the display logic being in the class. We can also extract any evaluation of the state of the board into a BoardEvaluator class so that reason for change in the board class has to do with the state of the board. The reasons for changing how we determine a winner can be encapsulated in the BoardEvaluator class.
