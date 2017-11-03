---
layout: post
title: "Art of Programming"
categories:
- blog
tags:
- android
author: Prinsu Kumar
---


## SOLID Principles for Android Developers

## S is for Single Responsibility Principle
## O is for Open/Close Principle
## L is for Liskov Substitution Principle
## I is for Interface Segregation Principle
## D is for Dependency Inversion Principle

## History

The term was introduced by Robert C. Martin in an article by the same name as part of his Principles of
Object Oriented Design, made popular by his book Agile Software Development, Principles, Patterns and
Practices.
It helps reshape how you think about working with old code and making it maintainable again.
Most important, it helps you reformulate what `legacy` actually means.
Hint - does your code have tests? No!?! Well, your code might already be … you guessed it … legacy.


## Single Responsibility Principle

Single Responsibility is really encapsulation plus some aspects of inheritance and polymorphism.
Single Responsibility is more of a basic principle or tenet of how to decompose a problem into
cooperating objects and define the classes of those objects.
`Your class should have only one well-defined responsibility`.
That means that for example, a Person class should only worry about the domain problem regarding the person itself,
and not for example, its persistence on the database. For that, you may want to use a PersonDAO for example.
A Person class may want to keep its responsibilities the shortest it can.
If a class is using too many external dependencies (that is, other classes), that's a symptom that
the class is having too many responsibilities. This problem often comes when developers try to model the real world using objects and take it too far.
Loosely coupled applications often are not very easy to navigate and do not exactly model how the real world works.

* violation of single responsibility principle

public class MovieRecyclerAdapter extends RecyclerView.Adapter<MovieRecyclerAdapter.ViewHolder> {

  private List<Movie> movies;
  private int itemLayout;   

    public MovieRecyclerAdapter(List<Movies> movies, int itemLayout)
    {
         this.movies = movies;
         this.itemLayout = itemLayout;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType)
    {
      View v = LayoutInflater.from(parent.getContext())
                             .inflate(itemLayout, parent, false);         
      return new ViewHolder(v);
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
     final Movie movie = movies.get(position);  
     holder.itemView.setTag(movie);
     holder.title.setText(movie.getTitle());  
     holder.rating.setText(movie.getRating());
     String genreStr = "";  
     for (String str: movie.getGenre()) {
           genreStr += str + ", ";        
     }     
     genreStr = genreStr.length() > 0 ?
            genreStr.substring(0, genreStr.length() - 2) : genreStr;  
     holder.genre.setText(genreStr);           
     holder.releaseYear.setText(movie.getYear());
     Glide.with(holder.thumbNail.getContext())
          .load(movies.get(position)
          .getThumbnailUrl())
          .into(holder.thumbNail);
    }

    @Override
    public int getItemCount() {
        return movies.size();
    }

    public static class ViewHolder extends RecyclerView.ViewHolder {
      @Bind(R.id.title) TextView title;
      @Bind(R.id.rating) TextView rating;        
      @Bind(R.id.genre) TextView genre;
      @Bind(R.id.releaseYear) TextView releaseYear;   
      @Bind(R.id.thumbnail) ImageView thumbNail;

      public ViewHolder(View itemView) {
        super(itemView);
        ButterKnife.bind(this, itemView);            
      }
    }
}

The code above violates the Single Responsibility Principle. Because the adapter’s onBindViewHolder method is not only mapping from an Movie object to the view, but is also performing data formatting as well. This violates the Single Responsibility Principle. The adapter should only be responsible for adapting an order object to its view representation. The onBindViewHolder is performing extra duties that it should not be. An updated onBindViewHolder method could look like this:

* single responsibility principle - Fix it example

public class MovieRecyclerAdapter extends RecyclerView.Adapter<MovieRecyclerAdapter.ViewHolder> {

  private List<Movie> movies;
  private int itemLayout;

    public MovieRecyclerAdapter(List<Movie> movies, int itemLayout)
    {
         this.movies = movies;
         this.itemLayout = itemLayout;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType)
    {
      View v = LayoutInflater.from(parent.getContext())
                             .inflate(itemLayout, parent, false);       
      return new ViewHolder(v);
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
     final Movie movie = movies.get(position);  
     holder.itemView.setTag(movie);
     holder.title.setText(movie.getTitle());  
     holder.rating.setText(movie.getRating());
     holder.genre.setText(  
            ArraysUtil.convertArrayListToString(movie.getGenre()));           
     holder.releaseYear.setText(movie.getYear());
     Glide.with(holder.thumbNail.getContext())
          .load(movies.get(position)
          .getThumbnailUrl())
          .into(holder.thumbNail);
    }
* Glide provides two built in implementations of PreloadSizeProvider:
    1. ViewPreloadSizeProvider
    2. FixedPreloadSizeProvider

    @Override
    public int getItemCount() {
        return movies.size();
    }

    public static class ViewHolder extends RecyclerView.ViewHolder {
      @Bind(R.id.title) TextView title;
      @Bind(R.id.rating) TextView rating;        
      @Bind(R.id.genre) TextView genre;
      @Bind(R.id.releaseYear) TextView releaseYear;   
      @Bind(R.id.thumbnail) ImageView thumbNail;

      public ViewHolder(View itemView) {
        super(itemView);
        ButterKnife.bind(this, itemView);            
      }
    }
}

*In the context of the Single Responsibility Principle (SRP) we define a responsibility as “a reason for change”. If you can think of more than one motive for changing a class, then that class has more than one responsibility.*


## O is for Open/Close Principle

Similarly, Open/Closed is a language feature, usually implemented via inheritance. But it can be done via monkeypatching. All design patterns should illustrate this.
Your class should be open for extension, but closed for modification.
Classes should be extensible, but not modifiable. That means that adding a new field to a class is fine,
but changing existing things are not. Other components on the program may depend on said field.

What we are basically talking about here is to design our modules, classes and functions in a way that when a new functionality is needed, we should not modify our existing code but rather write new code that will be used by existing code. let’s dive to it, and show some code:

* violation of Open closed principle

public class Rectangle {
    private double length;
    private double height;
    // getters/setters ...
}

public class Circle {
    private double radius;
    // getters/setters ...
}

public class AreaFactory {

    public double calculateArea(ArrayList<Object>... shapes) {
        double area = 0;
        for (Object shape : shapes) {
            if (shape instanceof Rectangle) {
                Rectangle rect = (Rectangle)shape;
                area += (rect.getLength() * rect.getHeight());                
            } else if (shape instanceof Circle) {
                Circle circle = (Circle)shape;
                area +=
                (circle.getRadius() * cirlce.getRadius() * Math.PI);
            } else throw new RuntimeException("Shape not supported");                    
        }

        return area;
    }
}

As we see above, this code seems like if we have a shape like Triangle or any other polygone, we’re going to be modifying the AreaFactory class over and over. And that’s violate the open closed principle. It is not closed for modification and it is not open to extension. And that’s really bad, so let’s fix that:

* Open closed principle: good example

public interface Shape {
    double getArea();
}

public class Rectangle implements Shape {
    private double length;
    private double height;
    // getters/setters ...

    @Override
    public double getArea() {
        return (length * height);
    }
}

public class Circle implements Shape {
    private double radius;
    // getters/setters ...
   @Override
    public double getArea() {
        return (radius * radius * Math.PI);
    }
}

public class AreaFactory {

    public double calculateArea(ArrayList<Shape>... shapes) {
        double area = 0;
        for (Shape shape : shapes) {
            area += shape.getArea();
        }

        return area;
    }
}

Now, if we need to add a new shape, the AreaFactory will not need to be changed because it is open for extension through the Shape interface.

## L is for Liskov Substitution Principle

Liskov Substitution, also, is usually a language feature. We often implement this with well-design
polymorphic classes. Some folks argue that duck-typing breaks this principle, other say that duck-typing
manifests it. There are numerous design patterns which rely on Liskov Substitution. Anything with
polymorphism will exhibit Liskov Substitution.
A class that expects an object of type animal should work if a subclass dog and a subclass cat are passed.
That means that Animal should NOT have a method called bark for example, since subclasses of type cat
won't be able to bark.
Classes that use the Animal class, also shouldn't depend on methods that belong to a class Dog. Don't do things like "If this animal is a dog, then (casts animal to dog) bark. If animal is a cat then (casts animal to cat) meow".

`Child classes should never break the parent class’ type definitions`.

As simple as that, a subclass should override the parent class’ methods in a way that does not break functionality from a client’s point of view. Here is a simple example to demonstrate the concept.

* violation of Liskov's Substitution principle

public interface Car {
  public void startEngine();
}

public Ferrari implements Car {
  ...
  @Override
  public double startEngine() {
         //logic ...
  }
}

public Tesla implements Car {
  ...
  @Override
  public double startEngine() {
         if (!IsCharged)
            return;
       //logic ...
  }
}

* Make the call
public void letStartEngine(Car car) {
   car.startEngine();
}

As you can see in the code above, there are two classes of cars. One fuel car and one electric car. The electric car can only start if it’s charged .The LetStartEngine method will not work if a car is electric and not charged. This breaks the LSP principle since it must be Charged to be able to start as the IsCharged (which also is part of the contract) won’t be set as in the base class.

To solve this you can do something like this:

* Make the call
public void LetStartEngine(Car car) {

  if (car instanceof Tesla) ((Tesla)car).TurnOnCar();  
   car.startEngine();
}

But this violates the Open/Closed Principale, so the proper way is to automatically turn on the car in the StartEngine method like below:

* Fix of Liskov's Substitution principle

public interface Car {
  public void startEngine();
}

public Ferrari implements Car {
  ...
  @Override
  public double startEngine() {
         //logic ...
  }
}

public Tesla implements Car {
  ...
  @Override
  public double startEngine() {
         if (!IsCharged)
            TurnOnCar();
       //logic ...
  }
}

// Make the call
public void letStartEngine(Car car) {
   car.startEngine();
}


## I is for Interface Segregation Principle

Interface Segregation can be language feature. Java has it.
Python -- by most accounts -- doesn't do this. However, you'll note that many Python projects try to formalize their interface definitions with super classes and unit tests.
Keep your interfaces the smallest you can. A teacher that also is a student should implement both the
IStudent and ITeacher interfaces, instead of a single big interface called IStudentAndTeacher.

This principle states that once an interface becomes too fat, it needs to be split into smaller interfaces so that client of the interface will only know about the methods that pertain to them. As you know, the Android View class is the root superclass for all Android views. You name it, if it’s a Button, the root superclass is View. Let’s dive to it, and show some code:

public interface OnClickListener {
    void onClick(View v);
    void onLongClick(View v);
    void onTouch(View v, MotionEvent event);
}

As you can see, this interface contains three diffrent methods,
assuming that we wanna get click from a button:

* Violation of Interface segregation principle
Button valid = (Button)findViewById(R.id.valid);
valid.setOnClickListener(new View.OnClickListener {
    public void onClick(View v) {
       // TODO: do some stuff...

    }

    public void onLongClick(View v) {
        // we don't need to it
    }

    public void onTouch(View v, MotionEvent event) {
        // we don't need to it

    }
});

The interface is too fat because it’s forcing to implement all the methods, even if it doesn’t not need them. Let’s trying to fix them using ISP:

* Fix of Interface Segregation principle

public interface OnClickListener {
    void onClick(View v);
}

public interface OnLongClickListener {
    void onLongClick(View v);
}

public interface OnTouchListener {
    void onTouch(View v, MotionEvent event);
}

know we can use the interface without implement some messy methods.


## D is for Dependency Inversion Principle

Dependency Inversion(depend on abstractions) is often a language feature. Not many design pattern
insist on this. However, many of us like to use the abstractions in Java collections library so
that we can use Liskov Substitution among the concrete classes.
Objects should not instantiate their dependencies, but they should pass to them.
For example, a Car that has an Engine object inside should not do engine = new DieselEngine(),
but rather said engine should be passed to it on the constructor.
This way the car class will not be coupled to the DieselEngine class.

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.
2. Abstractions should not depend upon details. Details should depend upon abstractions.

Let’s start from the code. Many of us probably seen (or written) code like this:

* violation of Dependency's inversion principle

class Program {

	public void work() {
		// ....code
	}
}

class Engineer {

	Program program;

	public void setProgram(Program p) {
		program = p;
	}

	public void manage() {
		program.work();
	}
}

The problem with the above code is that it breaks the Dependency Inversion Principle ; namely item (1.) from above: High-level modules should not depend on low-level modules. Both should depend on abstractions. We have the Engineer class which is a high level class, and the low level class called Program.

Let’s assume the Engineer class is quite complex, containing very complex logic. And now we have to change it in order to introduce the new SuperProgram. Let’s see the disadvantages:

    we have to change the Engineer class (remember it is a complex one and this will involve time and effort to make the changes).
    some of the current functionality from the engineer class might be affected.
    the unit testing should be redone.


    // Dependency Inversion Principle - Good example
    interface IProgram {
    	public void work();
    }

    class Program implements IProgram {
    	public void work() {
    		// ....code
    	}
    }

    class SuperProgram implements IProgram {
    	public void work() {
    		//....code
    	}
    }

    class Engineer {
    	IProgram program;

    	public void setProgram(IProgram p) {
    		program = p;
    	}

    	public void manage() {
    		program.work();
    	}
    }

    In this new design a new abstraction layer is added through the IProgram Interface. Now the problems from the above code are solved(considering there is no change in the high level logic):

*   Engineer class doesn’t require changes when adding SuperProgram.
*   Minimized risk to affect old functionality present in Engineer class since we don’t change it.
*   No need to redo the unit testing for Engineer class.
