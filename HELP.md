# Dependencies

markdownlint Extension For Linting Markdown files

VSCode Extension: <https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint>

PlantUML Extension For Creating UML Diagrams

VSCode Extension: <https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml>

## Documentation

Command Platte:

> - PlantUML: Preview Current Diagram
>
> - PlantUML: Export Current Diagram
>
> - Select .svg file format then insert the diagram into the markdown

<https://plantuml.com/class-diagram>

## Example

@startuml

abstract class Creator {
    +createProduct(): Product
}

class ConcreteCreator1 {
    +createProduct(): Product
}

class ConcreteCreator2 {
    +createProduct(): Product
}

abstract class Product

class ConcreteProduct1
class ConcreteProduct2

Creator <|-- ConcreteCreator1
Creator <|-- ConcreteCreator2
Product <|-- ConcreteProduct1
Product <|-- ConcreteProduct2
ConcreteCreator1 -> ConcreteProduct1
ConcreteCreator2 -> ConcreteProduct2

@enduml
