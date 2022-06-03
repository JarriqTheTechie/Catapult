
  
# Catapult  
A framework to create reusable server rendered view components with low coupling and easy testability.    
    
    
    
    
## Requirements    
 1. Python 3.6+    
2. Flask or Masonite Framework  
    
## Installation    
    
     pip install CatapultComponents
     or 
     https://github.com/JarriqTheTechie/catapult.git    

   
## How to Add to your Project  (Flask)  
    
    from catapult import Catapult, render_inline

	app = Flask(__name__)
	Catapult(app)
	CATAPULT_ANNOTATE = True

## How to Add to your Project  (MasoniteFramework)  
In your `app/providers/__init__.py` file add the following import

    from catapult.CatapultProvider import CatapultProvider
<br>
In your `config/providers.py` file add the following import and add `CatapultProvider` to your list of **PROVIDERS**

    from app.providers import CatapultProvider
   


## Making Components 
Components are read from the following directory of your project.    
`templates/components`    

Components require two files to be created.     
1. FooComponent.html eg. `NameComponent.html` 
2. FooComponentComponent.py eg. `NameComponent.py` 
<hr> 
*templates/components/NameComponent.py*    

     class NameComponent:      
	     def __init__(self, name):      
	         self.name= name    

<hr> 
   
*templates/components/NameComponent.html*    
 

    <h1>{{ name }}</h1>    

 
      
## Using the Components    
Catapult Components can be used in any of the following ways.     
    
Calling the render method from Jinja template. eg.    
*templates/index.html* 

    {{ render("NameComponent", name="Jane Doe") }} 

   
 <hr>    
    
In a controller you can render the Catapult Components by returning the component using the following syntax.    

    from catapult import render_inline
    return render_inline('{{ render("NameComponent", name="Jane Doe") }}')    

 
## Parameters 
### Passing Parameters    
Underneath the hood, components are simply python classes with a matching html template. Parameters are passed to the __init__ function of the component class.     
    
For example, lets use our NameComponent which has the "name" instance variable. Here's how we would pass a name to the component.     
    
    {{ render("NameComponent", name="James Blunt") }}

    
    
## Properties    
Catapult Components passes data to instance variables of the component class.    
    
 

    import random    
    class ButtonComponent: 
	    def __init__(self, text, variant="danger"): 
		    self.text = text 
		    self.variant = random.choice(["primary", "success", "danger", "warning", "info", "secondary"])    
    
    
## Nested Components 
Component nesting is supported and doesn't require subclassing in the .py file. This can be done entirely in the .html component file.    
    
## API    
#**render()** Render a component in a template    
    
`{{ render("ProductComponent", name="Gatorade", price=2.25) }}`  
<hr>    
    
#**render_inline()** Returning the string representation of a component    
    
 `render_inline('{{ render("ProductComponent", name="Gatorade", price=2.25) }}')`  
<hr>     
    
#**render_with_collection()** Render a component for each element in a collection    
*sample collection*  
 
 `fruit = [{"name": "apple", "vendor": "Super Value"}, {"name": "grapes", "vendor": "Buy for Less"}, {"name": "banana", "vendor": "Cost Right"}]`    
    
 

    {{ render_with_collection("FruitPickerComponent", "fruit", fruit=fruit)|safe }}  

  
This replaces `{% for fruit in fruits %}{% endfor %}`    
<hr>     
    
#**render_if()** Determine whether the component should render    
If the result of the .render_if() method is False then the component will not render.     
    
    class ListComponent:       
	    with_collection_parameter = "fruit"      
              
		def __init__(self, fruit, fruit_counter=int):        
			self.fruit = fruit      
            self.fruit_counter = ""      
              
	        def render_if(self):      
	            return self.fruit["name"] == "grapes"   
<hr> 
 
 ## Roadmap 
TODO
