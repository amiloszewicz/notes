# angularstart-quicklist

angular, angularstart

## Module Outline

 0. Source Code
 1. Lesson 1: Introduction
 2. [Lesson 2: Getting Started](#lesson-2-getting-started)
 3. [Lesson 3: The Architecture](#lesson-3-the-architecture)
 4. Lesson 4: Creating a Declarative Modal
 5. [Lesson 5: Creating a Form Modal Component](#lesson-5-creating-a-form-modal-component)
 6. Lesson 6: Creating a Checklist Service
 7. Lesson 7: Creating a Checklist List Component
 8. Lesson 8: The Checklist Detail Page
 9. Lesson 9: Creating Checklist Items
 10. Lesson 10: Toggling Item State
 11. Lesson 11: Persisting Data in Local Storage
 12. Lesson 12: Editing and Deleting Data
 13. Lesson 13: Styling and Theming
 14. Lesson 14: Conclusion and Challenges

## Main concepts we will cover are

- Complex Lists
- Data Types / Interfaces
- Forms and User Input
- Simple Navigation
- Passing Data Between Pages
- Creating, Reading, Updating and Deleting Data
- Data Storage and Retrieval
- Theme and Styling
  
### [Lesson 2: Getting Started](#lesson-2-getting-started)

#### Getting Started

There are a few things that we will do at the beginning of every application build, these are things like:

- Generating the application
- Installing extra packages (if necessary)
- Restructuring the generated application to our liking

### [Lesson 3: The Architecture](#lesson-3-the-architecture)

The application will be broken up into two main parts:

- Viewing all checklists
- Interacting with individual checklists

These features will be represented by the two routed/smart components in our application:

- home (for viewing all checklists)
- checklist

Home & checklist are a *feature* and they will contain most of the code.

feature (omitted in this case because we have just one smart component per feature)
data-access
ui
utils
For example, our checklist feature will contain the following:

data-access: checklist-item.service.ts
ui: checklist-item-header and checklist-item-list (dumb components)
There will also be some shared functionality that we will store in a shared folder:

data-access: checklist.service and storage.service
interfaces: checklist-item and checklist
ui: form-modal and modal (a generic form and modal dumb component used by both features)

### [Lesson 5: Creating a Form Modal Component](#lesson-5-creating-a-form-modal-component)

```
handleSubmit(){
  this.save.emit();
  this.close.emit();

  // trigger some other thing here
}
```

The author of StateAdapt, Mike Pearson, describes callback functions like this as:
> The curly braces of functions that don’t return anything are like open arms inviting imperative code.
