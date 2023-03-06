# MVVM

## Introduction

MVVM stands for Model-View-ViewModel and is a software architechture pattern. The pattern aims to separate view logic (View) from business logic (ViewModel) and data (Model).

## View Model

The ViewModel is "loosely coupled" to the view (through events) comminicating the change to the model and therefore acts as a mediator between the View and Model.

## View

The view is responsible for implementing the visual elements of an application such as buttons, text boxes, images, and graphical elements. It is also responsible for controlling how data is presented to the user, such as formatting and styling.

## Model

The model is where the actual data of the application resides. It typically consists of classes or objects that represent the data and provide methods for accessing and manipulating it. The model is responsible for enforcing the business rules of the application, such as data validation and authorization, and for performing any necessary calculations or transformations on the data.

## Example

An example of MVVM in action can be seen here:

>
> <https://github.com/Steelstone3/Bubbles-Dive-Planner>
>
