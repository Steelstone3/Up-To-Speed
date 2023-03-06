# MVP

## Introduction

MVP stands for Model-View-Presenter and is a software architechture pattern. The pattern aims to separate the presentation layer of an application into three interconnecting components; the Model, the View, and the Presenter.

## Presenter

The Presenter is a "loosely coupled" mediator between the view and model. It contain the business logic and state management for the view. It provides the view with the data it needs by either retrieving it from model. Then the presenter updates the view according to the changed data, user inputs, and state control.

## View

The view is responsible for implementing the visual elements of an application such as buttons, text boxes, images, and graphical elements. It is also responsible for controlling how data is presented to the user, such as formatting and styling.

## Model

The model is where the actual data of the application resides. It typically consists of classes or objects that represent the data and provide methods for accessing and manipulating it. The model is responsible for enforcing the business rules of the application, such as data validation and authorization, and for performing any necessary calculations or transformations on the data.

## Example

An example of MVP in action can be seen here:

>
> Some example of the pattern or a project link here
>
