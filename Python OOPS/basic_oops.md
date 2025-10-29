## real world analogy why we  use oops 
      -- like we are making robot any body part we need to define the functionality , like head , eye 
      -- we can not give same def head() to many robot so here code reuseability is not there 
      -- so we can make class robot and define all the functionality inside it
      -- now we can make many robot using that class and all the functionality will be there
      -- so here code reuseability is there

## class
      -- class is a blueprint of object              example: car is a class
      -- it is a user defined data type 
      -- it is a way to group related data 
         and functionality together 
      -- it is a way to achieve code reuseability 
      -- syntax to define class 
          class ClassName:
              # class body
              # attributes
              # methods


## object
      -- object is an instance of class             example: audi , bmw are objects of car class
      -- it is a real world entity
      -- it has state and behavior
      -- it is created from class
      -- syntax to create object
          object_name = ClassName()


 ## attributes   
      -- attributes are the data members of class       example: color , model are attributes of car class
      -- they are used to store the state of object
      -- they are defined inside the class
      -- syntax to define attributes
          class ClassName:
              def __init__(self, attribute1, attribute2):
                  self.attribute1 = attribute1
                  self.attribute2 = attribute2 ## methods
      -- methods are the functions defined inside the class      example: start(), stop() are methods of car class
        -- they are used to define the behavior of object
        -- they are defined inside the class
        -- syntax to define methods
            class ClassName:
                def method_name(self, parameters):
                    # method body
## constructor
      -- constructor is a special method used to initialize the object
      -- it is called when the object is created
      -- it is defined using __init__() method
      -- syntax to define constructor
          class ClassName:
              def __init__(self, parameters):
                  # constructor body
    

## self keyword
        -- self is a reference to the current object
        -- it is used to access the attributes and methods of the class
        -- it is the first parameter of all the methods in the class
        -- syntax to use self keyword
            class ClassName:
                def method_name(self, parameters):
                    # method body
    
## example of class and object
        class Car:
            def __init__(self, color, model):
                self.color = color
                self.model = model

            def start(self):
                print(f"The {self.color} {self.model} is starting.")

            def stop(self):
                print(f"The {self.color} {self.model} is stopping.")

# creating objects of Car class
        car1 = Car("Red", "Audi")
        car2 = Car("Blue", "BMW")

        # accessing methods of Car class
        car1.start()
        car2.stop()

## advantages of oops
      -- code reusability
      -- data abstraction
      -- encapsulation
      -- inheritance
        -- polymorphism     
    

 ## disadvantages of oops
      -- more complex than procedural programming
        -- requires more memory
        -- slower execution due to additional features

## pillars of OOPS
    -- encapsulation
    -- inheritance
    -- polymorphism
    -- abstraction