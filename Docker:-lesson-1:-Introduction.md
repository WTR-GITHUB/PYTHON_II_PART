## Introduction

`Docker` is a popular containerisation platform that allows developers to **easily create, deploy, and run** applications in isolated containers. It uses operating system-level virtualisation to create lightweight and portable containers that can run on any system that supports `Docker`. Each container includes all the necessary dependencies and libraries required to run the application, making it easy to build and deploy applications across different environments. Docker also provides a centralised registry called Docker Hub, where developers can share and distribute their container images with the wider community. With Docker, developers can streamline the application development process, increase productivity, and reduce infrastructure costs.

## Installation 

### Linux 

For Linux users, please go there: https://docs.docker.com/engine/install/ubuntu/

### Windows

For Windows users , please go there: https://docs.docker.com/desktop/install/windows-install/

### macOS

For macOS users , please go there: https://docs.docker.com/desktop/install/mac-install/

## Images

**Docker images** are a key concept in Docker, a popular platform for building, packaging, and deploying software applications. In simple terms, a Docker image is a lightweight, standalone, and executable package that contains all the necessary files, dependencies, and configurations required to run an application.

An image is created by specifying a series of instructions in a Dockerfile, which is a text file that contains the commands to build the image. These instructions typically include things like installing packages, copying files, and setting environment variables. Once the Dockerfile is built, the resulting image can be stored in a Docker registry or repository, such as Docker Hub or a private registry.

Images are designed to be portable and can be run on any host that supports Docker. When an image is executed, it creates a container, which is a lightweight, isolated runtime environment that runs the application. Multiple containers can be created from the same image, each with its own isolated runtime environment, allowing applications to be easily scaled and managed.

Overall, Docker images provide a simple and efficient way to package, distribute, and run applications, making it easier to develop, deploy, and manage software in a variety of environments.

### Working with images

Open up a terminal or command prompt and type in the following command to download a Docker image:

```
docker pull <image_name>

```

Replace <image_name> with the name of the image you want to download. For example, if you want to download the official `nginx` image, you would type:

```
docker pull nginx

```

## Exercises: 
🧠 : Repeat the [OOP Part 2](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* **Task Nr.1**:
  
  Create a class `Person` that has two methods: `set_name` and `set_age`, which set the name and age attributes of the class, respectively.
  Modify these methods to return `self`, so that the calls can be chained together.
  

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1) 

* **Task Nr.2**:

  Create a class Currency that has the following properties:

    - code: A 3-letter currency code (e.g. "USD", "EUR", "GBP")
    - amount
    - exchange_rate

  Create the following methods:

    - set_code: A method that accepts a 3-letter currency code and sets the code attribute of the object
    - set_amount: A method that accepts a float number and sets the amount attribute of the object
    - set_exchange_rate: A method that accepts a float number and sets the exchange_rate attribute of the object
    - convert: A method that accepts a 3-letter currency code and a float number representing the new exchange rate, and calculates the new amount of 
      currency based on the exchange rate.
    - __str__: A method that returns a string representation of the Currency object in the following format "code: amount"

     Each method should return the instance of the class to allow method chaining.

* **Task Nr.3**:

  - Create a class Animal with a method speak that prints "Animal can't speak"

  - Create a class Dogs that inherits from Animals and overrides the speak method to print "Woof woof"

  - Create a class Cats that inherits from Animals and overrides the speak method. But in this new method call the speak method from the Animals class 
    using the super() function, after that print "Meow meow"

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3) 

* **Task Nr.4**: 

  Create a class Person that has the following properties:

   - name: A string representing the person's name
   - age: An integer representing the person's age

  Create the following methods:

   - get_name: A method that returns the person's name
   - get_age: A method that returns the person's age
   - __str__: A method that returns a string representation of the Person object in the following format: "name is age years old."

  Create a class Student that inherits from Person and adds the following properties:

   - student_id: An integer representing the student's id
   - major: A string representing the student's major

  Create the following methods:

   - get_student_id: A method that returns the student's id
   - get_major: A method that returns the student's major
   - __str__: A method that returns a string representation of the Student object in the following format: "name is a age years old student of major 
     major. Student id: student_id"

  Create a class GraduateStudent that inherits from Student and adds the following properties:

   - program: A string representing the graduate student's program
   - advisor: A string representing the graduate student's advisor

  Create the following methods:

   - get_program: A method that returns the graduate student's program
   - get_advisor: A method that returns the graduate student's advisor
   - __str__: A method that returns a string representation of the GraduateStudent object in the following format: "name is a age years old graduate 
     student of major major. Student id: student_id. program: program and advisor: advisor."
   - __init__: This method should take in the same parameters as Person's init, but also take in additional parameters student_id, major, program, 
     advisor and call the super's class init method with Person's parameters and set the additional parameters.

   Show examples with working code. 
   
 [Hint](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4) 

## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [QuanticDev - method chaining](https://quanticdev.com/articles/method-chaining/)
* [RealPhyton - super() function](https://quanticdev.com/articles/method-chaining/)
***