# Smart-Getters
Data Access controle is one of the most complicated problems in big projects, we can easy controle the access over the modules, methods and API's but to controle the data returned to the user we must impliment a logic depending on the user, his role and many other criteria... Since that I hate impliment the same logic in every method I created this to impliment everything in one service and call one method that will give me the appropriate data based on the appropriate criteria.

SmartGetters is a service that will fetch the data from database based on specific criteria depending on every singles user, you can add criteria as you which and anytime you want, you will not have to do that in every single place where you called specific data, using SmartGetters you will impliment all that in one place, update your code and maintain it in one place and the most exciting part is that SmartGetters is generic !

The code in the file SmartGetters in this repository is a simple example that you can change and adapt it to your project.

Let's explain it :
Suppose that we have a project where a Super Admin can do everything, every Simple Admin have a list of agencies, clients, programs and products, and a Commercial can see clients that the admin gived to him, products and programs but he can't add or edit them (read only access)
Those are 3 user types : Super Admin - Simple Admin - Commercial 
and 3 roles : 
  Super Admin (can Edit, Add, Delete, Read everything)
  Simple Admin (can Edit, Add, Delete, Read only the data that he own)
  Commercial (Read-only the data that the Simple Admin gived to him)
Which give us those Tables :
  Users
  UserType
  Agencies
  Products
  Programs
  Clients
And to know what the Commercial must have access to :
  UserClients
  UserProducts
  UserPrograms
Now suppose that you there is 10 interfaces where you must show data to the connected user and everytime you have to check the UserType and the UserRole so you can know which data you have to show! Imagine that after 3 months a new UserType and UserRole is added, you must check all this code again and update it... Imagine that one of the UserRoles has changed, you will do that again... imagine that the logic of the data access has changed... again... this painful...

The solution is :

We create a service called SmartGetters, in this service we impliment a method that will call another method based on the entity type, for example we create a method called : GetAppropriateData(Type entityType)

then based ont the entity type we call another method for that model, for example:
  GetAppropriateProducts(ApplicationUser connectedUser)
  GetAppropriateClients(ApplicationUser connectedUser)
  GetAppropriateAgencies(ApplicationUser connectedUser)
And you can impliment as many methods as you want.... now you have all your data access logic in one place that you can call everywhere and change it whenever you want in one place.

Now let's suppose that the Simple admin can see all the data in the project but can Edit/Delete only the data that he created !

Easy, we just have to return a list of AccessData which contain the data he can access to (a list of Ids) and boolean variables which indicate if he can Edit/Delete that data Id and in the GetAppropriate(ModelName)() we check whenever he is the creator of that line or not. Simple ? yes yes yes, see the example in order to understand more.

See the file SmartGettersService for a full code example.

If you need any help or suggestions please contact me via : mabroukifakhri@gmail.com
