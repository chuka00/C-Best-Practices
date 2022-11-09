```c#

Below are some very important best practices we need to adopt inorder to become world class programmers
1. Use searchable names
I am sure that more than once you forget where something is and you start looking for that something but you can’t find it because you don’t remember what name you gave to the variable or directly, you don’t remember if you named that constant. For your better understanding:

Bad way:

// In the future we will not remember what 86400000 means.
clearBacklog(backlog, 86400000);
Good way:

// Declare constants with a searchable name
var MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;

clearBacklog(backlog, MILLISECONDS_PER_DAY);
This small practice, although it may not seem like it at the time, will save us many hours of searching and quite a few headaches (both for us, the current developers, and for potential future developers).

2. Use variable names that are easy to remember
    This malpractice is one of the most common. Many times we — the .NET developers — want to complicate a lot when in most of the occasions it is not necessary.

When declaring a variable, we should use a name that makes sense, that is easy to remember and that is easy to pronounce.

Bad way:
var yyyymmdstr = DateTime.Now.ToString("YYYY/MM/DD");

Good way:
var currentDate = DateTime.Now.ToString("YYYY/MM/DD");

This does not seem to be important, but once the project develops and becomes larger, the number of variables will be very large. And we all know that when we open a project after a long time without opening it, many times we don’t know what some part of the code does.

3. Use variable names with the same structure
Many times it has happened to us that we declare variables but we declare each one with a different structure or — lexically speaking — with a different vocabulary. Let me explain:

We should always look for the greatest simplicity. We should always use the same word and not vary it — I mean synonyms. Let’s see a practical example.

Bad way:
getUserInfo();
getClientData();
getCustomerRecord();


Good way:
getUser();
view rawcsharptips4.cs hosted with ❤ by GitHub
In that example, we can clearly see that in the bad way we are using different synonyms for the same word. This may cause confusion in the future, both for the current developer and for the (possible) future developer who will have to understand the code.

4. Don’t repeat yourself (DRY)
This error is very common because we unconsciously repeat names or words. This bad practice in the long run makes you have a very dirty code since there will be many things that will be repeated. Let’s get down to practice:

Bad way:
Bike MountainBike = new(){
   bikeBrand = "Trek",
   bikeModel = "MX Mountain",
   bikeColor = "Green"
};

void paintBike(Bike mountainBike, string color){
     mountainBike.bikeColor = color;
}


Good way:
Bike MountainBike = new(){
   brand = "Trek",
   model = "MX Mountain",
   color = "Green"
};

void paintBike(Bike mountainBike, string color){
     mountainBike.color = color;
}
In this way we can see that by spending less time thinking and writing, we get a much cleaner and easier to read code (which we will thank ourselves in the future for having done)

5. Uses highly descriptive variable names
Another bad practice is to send functions directly as an argument of another function. This only causes a lot of confusion and makes our heads hotter than an old AMD FX series processor.

Bad way:
const address = "One Infinite Loop, Cupertino 95014";
var cityZipCodeRegex = new Regex(@"/ ^[^,\\] +[,\\\s] + (.+?)\s * (\d{ 5 })?$/").Matches(address);
saveCityZipCode(
  cityZipCodeRegex[0].Value,
  cityZipCodeRegex[1].Value
);


Good way:
var address = "One Infinite Loop, Cupertino 95014";
var cityZipCodeRegex = new Regex(@"/ ^[^,\\] +[,\\\s] + (.+?)\s * (\d{ 5 })?$/").Matches(address);
var city = cityZipCodeRegex[0].Value;
var zipCode = cityZipCodeRegex[1].Value;
saveCityZipCode(city, zipCode);

The solution, as we can see, is to add the resulting values in variables and then send those variables to the function. This will allow us to understand in a simpler way the information that you are sending to it and besides, we will save a Noctua heatsink for our head.

6. Always encapsulate conditionals
Encapsulation is a way that helps isolate implementation details from the behavior exposed to clients of another class.

Bad way:
if (website.state == "down")
{
    // ...
}

Good way:
if (website.IsDown())
{
    // ...
}

Also, encapsulation allows for greater control over the coupling of the code being written.

7. Don’t use magic chains
For those who do not know this, magic strings are string values that must be specified in the code. They always generate an impact on the code. In most cases, magic strings end up almost always duplicating themselves and because they cannot be updated automatically, they are susceptible to being a source of errors.

Bad way:
if (userRole == "Admin")
{
    // logic in here
}


Good way:
const string ADMIN_ROLE = "Admin"
if (userRole == ADMIN_ROLE)
{
    // logic in here
}

In this way, we will prevent these strings from being duplicated and causing errors in case of making any change in any of them.

I know these little tips are pretty simple (although I’m sure not all of you will follow them😏). The number of ways to write cleaner code in C# is more infinite than the universe. So, I’m going to make a list of Cleaner C# Code articles, in which, we will touch on more advanced tips and some other tricks to improve the quality of our code.

8. Name the functions with what they do
Another bad practice is to name functions with incorrect or incomplete names. Just by reading the name of the function we should know almost 100% of what EXACTLY it does, otherwise this only causes confusion.

Bad way:
public class SlackNotification
{
    //...

    public void Handle()
    {
        SendMessage(this._to, this._files, this._body);
    }
}


var message = new SlackNotification(...);
// What is this? A handle for the message? Are we writing to a file now?
message.Handle();


Good way:
public class SlackNotification
{
    //...

    public void Send()
    {
        SendMessage(this._to, this._files, this._body);
    }
}

var message = new SlackNotification(...);
// Clear and obvious
message.Send();
The best recommendation is to spend a little more time thinking of a name that is very descriptive for the function. If you don’t do this good practice — just to save a couple of seconds in defining a good name, you will waste 


9. Never save unused code
This bad practice reminds me of when we keep or collect “stuff” at home but never make use of it. This is the same, if you have code that is not used, delete it. There is no point in having it taking up space and bothering you.

Bad way:
public void OldRequestMethod(string url)
{
    // ...
}

public void NewRequestMethod(string url)
{
    // ...
}

var request = NewRequestMethod(requestUrl);
SlackChannel("bytehide", request, "get users");


Good way:
public void RequestMethod(string url)
{
    // ...
}

var request = RequestMethod(requestUrl);
SlackChannel("bytehide", request, "get users");
Remember: Don’t bite off more than you can chew. If you haven’t used that code, there’s no point in keeping it there. You can still check it again in the version history in case you ever need it.

10. Never write in global functions
This bad practice consists of “contaminating” the globals. This is not a good thing because you could have problems and even crash with another library. Any user could run into this problem and would not realize it until the exception occurred.

Bad way:
public Dictionary<string, string> Config()
{
    return new Dictionary<string,string>(){
        ["product"] = "shield"
    };
}


Good way:
class Configuration
{
    private Dictionary<string, string> _configuration;

    public Configuration(Dictionary<string, string> configuration)
    {
        _configuration = configuration;
    }

    public string[] Get(string key)
    {
        return _configuration.ContainsKey(key) ? _configuration[key] : null;
    }
}

After this, we load the configuration and when it is ready, we create an instance of the Configurationclass

var configuration = new Configuration(new Dictionary<string, string>() {
    ["product"] = "shield"
});

Now yes, in the application, we should use one instance of Configuration

11. One level of abstraction per function
If you are developing and you find that a function does not have only one level of abstraction, but has several, this means that the function is doing too many things by itself.

This bad practice, apart from in the future generating questions like: What is this? What exactly does it do? It makes it difficult to reuse code because it does many things at the same time.

Bad way:
public string ParseBetterJSAlternative(string code)
{
    var regexes = [
        // ...
    ];

    var statements = explode(" ", code);
    var tokens = new string[] {};
    foreach (var regex in regexes)
    {
        foreach (var statement in statements)
        {
            // ...
        }
    }

    var ast = new string[] {};
    foreach (var token in tokens)
    {
        // lex...
    }

    foreach (var node in ast)
    {
        // parse...
    }
}


Good way:
class Tokenizer
{
    public string Tokenize(string code)
    {
        var regexes = new string[] {
            // ...
        };

        var statements = explode(" ", code);
        var tokens = new string[] {};
        foreach (var regex in regexes)
        {
            foreach (var statement in statements)
            {
                tokens[] = /* ... */;
            }
        }

        return tokens;
    }
}

class Lexer
{
    public string Lexify(string[] tokens)
    {
        var ast = new[] {};
        foreach (var token in tokens)
        {
            ast[] = /* ... */;
        }

        return ast;
    }
}

class BetterJSAlternative
{
    private string _tokenizer;
    private string _lexer;

    public BetterJSAlternative(Tokenizer tokenizer, Lexer lexer)
    {
        _tokenizer = tokenizer;
        _lexer = lexer;
    }

    public string Parse(string code)
    {
        var tokens = _tokenizer.Tokenize(code);
        var ast = _lexer.Lexify(tokens);
        foreach (var node in ast)
        {
            // parse...
        }
    }
}
This, apart from leaving the code cleaner, will allow you to reuse code and test it (which you could not do properly before due to the large amount of things the function does).

12. Limiting function arguments
It is very important to limit the number of parameters that a function has. Remember: The simpler, the better. The problem comes when a function has more than 3 arguments, because it can cause many problems in understanding what it does.

Bad way:

public void ProtectApplication(string path, string configurationPath, string outPutPath, CancellationToken cancellationToken)
{
    // ...
}


Good way:
public class ProtectionConfig
{
    public string Path { get; set; }
    public string ConfigurationPath { get; set; }
    public string OutPutPath { get; set; }
    public CancellationToken cancellationToken { get; set; }
}

var config = new ProtectionConfig
{
    Path = "./app.exe",
    ConfigurationPath = "./shield.config.json",
    OutPutPath = "./app_protected.exe",
    CancellationToken = source.Token;
};

public void ProtectApplication(ProtectionConfig config)
{
    // ...
}

The best option is to use 1 or 2 arguments. Can you use more? Of course you can, but only if you are aware that in a couple of months you will have to figure out what is supposed to do what. The ideal would be to group when there are 3 or more.

13.Composition is better than inheritance
Although many do not know whether to use inheritance or composition, let me tell you that it is better to choose to use composition.

At first, many programmers think that inheritance is better but, you always have to ask yourself if composition could somehow model the problem better.


Bad way:
class Car
{
    private string Model { get; set; }
    private string Brand { get; set; }

    public Car(string model, string brand)
    {
        Model = model;
        Brand = brand;
    }

    // ...
}

// Bad because Car "have" engine data.
// CarEngineData is not a type of Car

class CarEngineData : Car
{
   private string Model { get; set; }
   private string Brand { get; set; }

   public CarEngineData(string model, string brand, string displacement, string horses)
    {
         // ...
    }

    // ...
}


Good way:
class CarEngineData
{
    public string Displacement { get; }
    public string Horses { get; }

    public EmployeeTaxData(string displacement, string horses)
    {
        Displacement = displacement;
        Horses = horses;
    }

    // ...
}

class Car
{
    public string Model { get; }
    public string Brand { get; }
    public CarEngineData EngineData { get; }

    public Car(string model, string brand)
    {
        Model = model;
        Brand = brand;
    }

    public void SetEngine(string displacement, double horses)
    {
        EngineData = new CarEngineData(displacement, horses);
    }

    // ...
}
To know when it is best to use which one, let’s look at a quick example:

Relationship “is-a” (Human-Animal)
Relationship “has-a” (User-UserDetails)


14. Learn to use setters and getters
Many times we do not set public, private or protected methods. This prevents us from better controlling the modification of the object’s properties.


Bad way:
class BankAccount
{
    public double Balance = 5000;
}

var bankAccount = new BankAccount();

// Buy a cappuccino ☕️ ...
bankAccount.Balance -= 15;


Good way:
class BankAccount
{
    private double _balance = 0.0D;

    pubic double Balance {
        get {
            return _balance;
        }
    }

    public BankAccount(balance = 1000)
    {
       _balance = balance;
    }

    public void WithdrawBalance(int amount)
    {
        if (amount > _balance)
        {
            throw new Exception('Amount greater than available balance.');
        }

        _balance -= amount;
    }

    public void DepositBalance(int amount)
    {
        _balance += amount;
    }
}

var bankAccount = new BankAccount();

// Buy a cappuccino ☕️ ...
bankAccount.WithdrawBalance(price: 15);

balance = bankAccount.Balance;
Also, when inheriting that class, by default, there is the possibility to override that functionality. The possibilities that this allows you are many.


3. Use Camel/Pascal Case Notation
Apart from choosing an appropriate name for your variables, also maintain how you write the names. Ideally, we use Camel Case and Pascal Case Notation as best code practices. Do not use random Capitals throughout your variables. That just doesn’t look pretty!

Camel Case Notation
Basically, the first letter of the first word of the variable will be in lower case, and the first letter of every other word that follows should be in upper case. You will have to use this notation while naming your local variables and method arguments.

Bad Practice
int RandomInteger;
string FirstName;


Good Practice
int randomInteger;
string firstName;


Reference for Task: https://blog.dotnetsafer.com/5-important-tips-to-writing-clean-c-code-in-2022/
                :https://codewithmukesh.com/blog/write-clean-csharp-code/
