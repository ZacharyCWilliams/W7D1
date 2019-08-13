parking lot with OOP principles
many floors
motorcycle, car, bus


class Parkinglot
  def initialize(floors, spaces, ticket_price)
    @floors = floors
    @spaces = spaces
    @ticket_price = ticket_price
  end

  def charge_customer(vehicle)
    if car.type == motorcycle && !@spaces.empty?
      vehicle.money -= 5
    elsif car.type == car && !@spaces.empty?
      vehicle.money -= 10
    end
  end



  private
  attr_accessor :ticket_price
end

class Lot_floor

    def self.generate_spots
      parking_spots = []
        rand(1..100).each do |spot|
          Parking_space.new
        end
      parking_spots
  end


  def initialize(available_spots = self.generate_spots, floor)
    @available_spots = available_spots
    @floor = floor
  end
end

class Parking_space
  def initialize(location, size)
    @location = location
    @size = size
  end
end

class Vehicle
  def initialize(wheels, make, model, gas_tank, size)
    @wheels = wheels
    @make = make
    @model = model
    @gas_tank = gas_tank
    @running = false
    @size = size
  end

  def start
    @running = true
  end

  def stop
    @running = false
  end

  def park
    if parking_space.size >= @size
      park
    else
      keep_looking
    end
  end

  private
  attr_accessor :running, :size
end

class Motorcycle < Vehicle
  def initialize(size, money)
    super(running)
    @size = compact
    @money = money
  end
end

class Car < Vehicle
   def initialize(size, money)
    super(running)
    @size = compact
    @money = money
  end
end

=====
class Vehicle
  attr_reader :spots_needed, :size

  def initialize(license_plate)
    @parking_spots = []
    @license_plate = license_plate
  end

  def park_in_spot(spot)
    # ...
  end

  def clear_spots
    # ...
  end

  def can_fit_in_spot(spot)
    # ...
  end
end

class Bus < Vehicle
  def initialize
    super
    @spots_needed = 5
    @size = :large
  end

  def can_fit_in_spot(spot)
    # Checks if spot is :large
  end
end

class Car < Vehicle
  def initialize
    super
    @spots_needed = 1
    @size = :compact
  end

  def can_fit_in_spot(spot)
    # Check if spot is :compact or :large
  end
end

class Motorcycle < Vehicle
  def initialize
    super
    @spots_needed = 1
    @size = :compact
  end
end

class ParkingLot
  def initialize
    @levels = # generate_levels
  end

  def park_vehicle(vehicle)
    # Park the vehicle in a spot or multiple spots. Return false if failed.
  end
end

class Level
  def initialize(floor, num_spots)
    @spots = # generate spots
    @available_spots = num_spots
    @floor = floor
  end

  def park_vehicle(vehicle)
    # Find a place to park vehicle or return false.
  end

  def park_starting_at(spot_num, vehicle)
    # Park a vehicle starting at spot number and continue until vehicle.spots_needed.
  end

  def find_available_spots(vehicle)
    # Find a spot to park the vehicle. Return index of spot or -1.
  end

  def spot_freed
    @available_spots += 1
  end
end

class ParkingSpot
  attr_reader :row, :spot_num

  def initialize(size, level, row, spot_num)
    @vehicle = nil
    @spot_size = size
    @level = level
    @row = row
    @spot_num = spot_num
  end

  def is_free?
    !@vehicle
  end

  def can_fit_vehicle?(vehicle)
    # Check it will fit.
  end

  def park(vehicle)
    # Park in spot
  end

  def unpark
    # Remove vehicle from spot and notify level that a new spot is available.
  end
end
=====


DFS (node class: value)

root node
target, prc

def dfs(target, &prc)

  return self if prc.call(self)

  self.children.each do |child| 
    node = child.dfs(target, &prc)
    return node if node
  end
  
  nil
end
===
class Node

  # -- Assume nodes have a value, and a attr_reader on value
  # -- Also, assume there are working parent/child-related methods for Node
  def dfs(, &prc)
    raise "Must give a proc or target" if prc.nil?

    return self if prc.call(self)

    self.children.each do |node|
      result = node.dfs(target, &prc)
      return result if result
    end

    nil
  end
end