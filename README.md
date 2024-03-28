# SubScene Reference Helper
A script that will assist with storing reference to the Registered classes for ease of access between them.

####  ${\color{lightgreen}Hope \space this \space helps!}$ Please let me know what you think and or if you have any questions or suggestions!

To use this script simply download or copy the ***SoReferenceManager*** script and add it to your project.
Once done, follow these steps to use it:
- Right click on your a project folder and select Create -> CVeinStudio -> ReferenceManager
- This will create a Scriptable Object asset
- To use this asset, simply create a variable in any class you would like to "register" and access its functions, as such:
  
```cpp
  public class SomeClass{

        private SoReferenceManager referenceManager; // assign this in the inspector
        private SomeClass self;

        // on your START or AWAKE
        private void Start()
        {
            self = this; // in order to pass a reference ("without duplicating") we need to store this class then pass it to the function.

            referenceManager.Register(ref self, self.GetInstanceID());
        }

  }
``` 
- Now the `SomeClass` class will be registered and stored in the collection for access
- ${\color{red}NOTE}$  Make sure you also `UnRegister` the class in the OnDestroy function
  
 ```cpp
  public class SomeClass{

        private SoReferenceManager referenceManager; // assign this in the inspector
        private SomeClass self;

       //... prev code

        private void OnDisable()
        {
            referenceManager.UnRegister(self.GetInstanceID());
        }
  }
```

- Finally, in order for you to retrieve objects of a specific Type, you would do this:
  
 ```cpp
  public class SomeClass{

        private SoReferenceManager referenceManager; // assign this in the inspector

        //... prev code
        List<EnemyList> enemyList = new List<EnemyList>();

        private void GetReferences()
        {
              // the GetObjectOfType reuturns an IEnumerable<T>, so you can convert it or do whatever from the data you get back
             enemyList = referenceManager.GetObjectOfType<EnemyController>().ToList();
        }
  }
```

#### CHEERS! Keep on keeping on!
