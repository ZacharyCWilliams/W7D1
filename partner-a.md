what is a class?

ruby is object oriented each object is part of a class

class is also an object

class Example
end

object_example = Example.new


=====

what does self mean?

self is always to refer to an object
  object_example <-- object
  object_example.self <--- object

  class Example
    self.blahblabFunction
    end

    object_example =Example.new
    object_example.blahblahFunction

    Example.blahblahFunction

================

what is the user of super?

class Animal

  def initialize ( name, whiskers)
    @name, @whiskers = name, whiskers
  end
end

class Dog < Animal
  def initialize(argumetns)
    super(*args)
  end
end

============

please deisgn a musical jukebox using objecto oriented principles

  asssume jukebox is virtual (not a phsyical location)
  assume operates free to charge ( dont have to pay to use it)

class Jukebox

  attr_reader :username

  def initialize(username)
    @username = username
    @tracks = []
    @original_playlist = []
    @premium_user = false
    @user = SpotifyUser.new
  end

  
end

class SpotifyUser

  attr_accessor :name, :location, :genre

  def initialize(name, location = "", genre = "")
    @name, location, genre = name, location, genre
  end

  def skip_track
    @tracks = @tracks.take(1) + @tracks.dup.shift
  end

  def add_playlist(new_playlist)
    @tracks.concat(new_playlist)
        #flatten it into a 1d array

  end

  def play_track

    @original_playlist += track.shift

  end

  def upgrade_premium
    @premium_user = true
  end

  def restart_playlist
    @tracks.concat(original_playlist)
  end



end 


=============

implemmnt a BFS breadth first search

    assume there is a node class
    the node class will take in a value as part of its initialization
    you will be monkey patching following method
    write a method bfs that does a BFS
      takes a target and a proc
  

#notes
  if this is in fact the queue search
    layer by layer

      target = 8
            5
        4       6
    3      1   2   8

    5 -> 4 -> 3 -> 1

    if it doesnt find it int he left tree, move to right

    5 -> 6 -> 2 -> 8

    dfs
    depth first search 



class Node

  def initialize(argumetns)
    @parent
    @children
  end

  def children
    @children.dup
  end

  def breadth_first_search(target, &prc)
    prc ||= Proc.new { |curr_node| curr_node == target }
    raise "error" if prc.nil?
    #return nil if target.nil? already covered in line 168, only saves performance time
    #assuming its the queue search 

    queue = [self]

      #loop thorugh the queue
      # keep adding new children into it
      #return that node if node == target

  

    until queue.empty?
      temp_curr_node = queue.shift
      return temp_curr_node if prc.call(temp_curr_node)
      queue.concat(temp_curr_node.children)
    end

    nil

  end

end

================
write a quicksort
@assuming its an array

class Array
def quicksort(arr, &prc)
  return arr if arr.length <= 2 
  prc ||= Proc.new ( |num1, num2| num1<=> num2 }

  pivot = arr.first
  remainder = arr.drop(1)

  first = remainder.select { |ele| prc.call(ele) == -1 }
  half  = remainder.select { |ele| prc.call(ele) != -1 }

  quicksort(first, &prc) + [pivot] + quicksort(last, &prc)
end