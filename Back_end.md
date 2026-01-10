# BACK END Development
---

### **Log :**
1. `Log` is just a message that my program writes when its running. It keeps record of every actions that are happening in my application. Think of it as a diary of your program keeps. 


### **Logger :**

> A logger is a tool (usually a Python object) that you use to create logs.

> Checking log is important and a logger helps in here. If there is a problem in your systme/program, you might want to know the cause of the problem, where the problem occurs and when does it occured. Log answer these questions. And, you can modify the log message for your benefits to track the bugs easily.

> Log = Faster debugging, Real-time visiblity, Detect hidden bugs easily.

```python
import logging

logger = logging.getLogger(__name__)  # create a logger

logger.info("Program started")
logger.warning("Something might be wrong")
logger.error("Something went wrong!")

```
```ruby
INFO:__main__:Program started  # Output looks like this
WARNING:__main__:Something might be wrong
ERROR:__main__:Something went wrong!

```
| Term     | Meaning                                  |
|----------|-------------------------------------------|
| Log      | A message written by a program            |
| Logger   | A tool to create/manage logs              |
| Logging  | The act of writing logs                   |
| logfire  | An advanced logging library for Python    |

---

### Fast Api

>  There are many kind of HTTP requests like `GET`, `POST`, `PUT` and `DELETE`. There are also `OPTIONS`, `HEAD`, `PATCH` and `TRACE`. But, these are not used much.

> `POST`: to create data.  
   `GET`: to read data.  
   `PUT`: to update data.  
   `DELETE`: to delete data.

> `@` This symbol is a python decorator. It is used to modify the behavior of a function or a class. In FastAPI, it is used to define routes and HTTP methods. When you see `@app.get("/")`, it means that the function below it will handle GET requests to the root URL.

> This is the "path operation function":  
   path: is `/`.  
   operation: is `get`.  
   function: is the function below the "decorator" (below `@app.get("/")`).

---

**Simple and basic Fast API code:**
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
```
---

**Fixed paths must come before dynamic ones.**
```python
@app.get("/users/me")       # Fixed
@app.get("/users/{user_id}") # Dynamic
```
> FastAPI matches routes in order, top to bottom.  
If /users/{user_id} comes first, it will also catch /users/me (treating "me" as user_id).  
✅ Always define specific paths first, then dynamic ones.  
❌ You can't define two functions for the same path and method.

---

**Enum**

> What is Enum?  
Enum = a class with fixed, constant values.  
Prevents invalid inputs.  
Built-in from Python 3.4.  

> 🔸 Why use Enum in FastAPI?  
✅ Accept only specific values in path/query.  
✅ FastAPI shows options in docs (Swagger UI).  
✅ Auto-validation (422 error on invalid input).

```python
class ModelName(str, Enum):
    alexnet = "alexnet"
    resnet = "resnet"
    lenet = "lenet"
```
> Here, `ModelName` is an Enum class with three fixed values: "alexnet", "resnet", and "lenet". A user can only use these values in the API request, ensuring valid input. Otherwise, FastAPI will return a 422 error. So, you can do some Enum manipulation in FastAPI to ensure that the user is using the correct values.

---

**Optioanal**
```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/items/{item_id}")
async def read_item(item_id: str, q: str | None = None):
    if q:
        return {"item_id": item_id, "q": q}
    return {"item_id": item_id}
```
> In this example, `q` is an optional query parameter. If the user provides it, the function returns both `item_id` and `q`. If not, it only returns `item_id`. The type hint `str | None = None` indicates that `q` can be a string or None (not provided). In recent versions of python (3.10+), you can use the `|` operator to indicate optional types, making it more concise instead of using `Optional[str] = None`.

---

**Request and Response Body**

> When data comes from a client to the API, it is called a request body.  
When data come from the API to the client, it is called a response body.

---

#### **Quick Basics**

> 1. `item.dict():` Converts a Pydantic model (Item) into a dictionary.  
> 2. Unpacking `(**item.dict()):`
Merges the fields of the item directly into the response dictionary.  
> 3. Why use it?
To create a flat JSON response instead of nested structure.

**without unpacking:**
```python
{
  "item_id": 42,
  "item": {
    "name": "Laptop",
    "price": 1200.50
  }
}
```
**With unpacking:**
```python
{
  "item_id": 42,
  "name": "Laptop",
  "price": 1200.50
}
```

**Override Order**
> { "item_id": 999, **item.dict() } → item_id from item.dict() overrides 999 if it exists.  
{ **item.dict(), "item_id": 999 } → Outer item_id (999) overrides the one inside.

**Type hints metadata for Query parameters**
> FastAPI uses type hints to validate request and response bodies.  
> You can add metadata to these type hints to provide additional information.  
```python
from fastapi import Query
from typing import Annotated

q: Annotated[str | None, Query(title="Search query", max_length=50, min_length = 3
)] = None
```
> This will restrict the query parameter `q` to a maximum length of 50 characters and provide a title for documentation purposes.  
Here, `Annotated` means that we are adding additional metadata to the type hint, which FastAPI will use for validation and documentation and `Query` is a function that allows us to define query parameters with additional constraints. For example: `max_length = 50` means that the query parameter `q` can have a maximum length of 50 characters and it is a constrain.


**Use of Alias in the Query**
```python
from fastapi import Query
from typing import Annotated

@app.get("/items/")
async def read_items(q: Annotated[str | None, Query(title="Search query", max_length=50, min_length=3)] = None):
    if q:
        return {"q": q}
    return {"message": "No search query provided"}
```
> In this example, we are using an alias for the query parameter `q`. The alias is the title we provided in the `Query` function. This means that in the documentation (Swagger UI), the query parameter will be displayed as "Search query" instead of just "q". This can make the API more user-friendly and self-explanatory.

**FastAPI `alias` কী এবং কেন লাগে?**

> URL এ কখনো কখনো এমন প্যারামিটার নাম থাকে যেটা Python ভেরিয়েবল নামে ব্যবহার করা যায় না।  
উদাহরণ: `item-query` → এখানে হাইফেন (`-`) আছে, যা Python ভেরিয়েবল নামে রাখা যাবে না।  
Python-এ এমন কিছু লিখতে গেলে SyntaxError হবে:
  ```python
  def read_items(item-query):  # ❌ এটা Python বুঝবে না
  ```
> Python-এ সেফ একটা ভেরিয়েবল নাম ব্যবহার করো (যেমন q, item_query ইত্যাদি)।  
তারপর FastAPI-এর alias ব্যবহার করে বলে দাও, URL এ ওই ভেরিয়েবল আসলে কোন নাম দিয়ে খুঁজতে হবে।

```python
from typing import Annotated
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/items/")
async def read_items(
    q: Annotated[str | None, Query(alias="item-query")] = None
):
    return {"q": q}
```
> কীভাবে কাজ করে:  
ব্রাউজারে কেউ রিকোয়েস্ট দিল:

```bash
/items/?item-query=foobar
```
> FastAPI দেখল:  
ফাংশনে ভেরিয়েবল আছে: q  
কিন্তু alias বলা আছে: "item-query"  
তাই URL এ item-query খুঁজে পাবে, মান নেবে (foobar)।  
`/items/?item-query=foobar`  
FastAPI দেখল:  
ফাংশনে ভেরিয়েবল আছে: q  
কিন্তু alias বলা আছে: "item-query"  
তাই URL এ item-query খুঁজে পাবে, মান নেবে (foobar)।  
FastAPI মানটা তোমার Python ভেরিয়েবল q তে ঢুকিয়ে দেবে।  
এখন ফাংশনের ভেতরে:

```python
def read_items(item_query: str | None = None):
    return {"item_query": item_query}
```
> `q == "foobar"`  
সহজ ভাষায়:  
ভিতরের নাম (Python): কোডের ভিতরে ব্যবহার হবে (যেমন q)।  
বাইরের নাম (URL): ক্লায়েন্ট বা ব্রাউজারে দেখা যাবে (যেমন item-query)।  
`alias` = এই দুই নামের মধ্যে কানেকশন বানায়।  
মনে রাখো:  
`alias` শুধু URL/query/body ইত্যাদির প্যারামিটার নাম ম্যাপ করার জন্য।  
বাইরের নাম যত অদ্ভুতই হোক, ভিতরে Python-এ সেফ নাম ব্যবহার করা যাবে।  

```yaml

তুমি চাইলে আমি এর সাথে **একটা ফ্লো ডায়াগ্রাম** বানিয়ে দিতে পারি, যেটা দেখলেই বোঝা যাবে কীভাবে alias কাজ করে।
```

**Meta data manipulation for Path parameters**
```python
from fastapi import Path
from typing import Annotated

@app.get("/items/{item_id}")
async def read_item(item_id: Annotated[int, Path(title="The ID of the item to retrieve")] = 0):
    return {"item_id": item_id}
```
> This is metadata manipulation for path parameters. The `Path` function allows us to add additional information to the path parameter `item_id`, such as a title for documentation purposes. This can make the API more self-explanatory and easier to use. We need to import the `Path` function from `fastapi`.  
We can use some element like `gt` and `le` to add additional constraints to the path parameter.  
`gt` means greater than  
`le` means less than or equal to  
`ge` means greater than or equal to  
`lt` means less than

**Basics**
> `model_config = {"extra": "forbid"}` -> This line forbids extra argument from client on the parameter. It will show a error message if a client pass more data than the parameter allows.  
`Literal` is a special type that allows you to specify a fixed set of values for a parameter. This can be useful for defining enums or other constrained values. For example:
```python
from fastapi import FastAPI
from typing import Literal

app = FastAPI()

@app.get("/items/")
async def read_items(item_type: Literal["book", "electronics", "clothing"]):
    return {"item_type": item_type}
```
> This is a simple example of using `Literal` in FastAPI. The `item_type` parameter can only accept one of the specified values ("book", "electronics", "clothing"). If a client tries to pass a different value, FastAPI will return a validation error. This can help ensure that your API only accepts valid input and can make it easier to work with enums or other constrained values.

> `Field` is a function that allows you to add additional metadata and validation to your schemas fields. You can use it to specify things like default values, title, description, and more. For example:
```python
from fastapi import FastAPI
from pydantic import BaseModel, Field

app = FastAPI()

class Item(BaseModel):
    id: int
    name: str = Field(..., title="The name of the item", max_length=100)
    description: str | None = Field(None, title="The description of the item", max_length=300)

@app.post("/items/")
async def create_item(item: Item):
    return {"item": item}
```

```python
from fastapi import FastAPI
from pydantic import BaseModel, HttpUrl

app = FastAPI()


class Image(BaseModel):
    url: HttpUrl
    name: str


class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None
    tags: set[str] = set()
    images: list[Image] | None = None


class Offer(BaseModel):
    name: str
    description: str | None = None
    price: float
    items: list[Item]


@app.post("/offers/")
async def create_offer(offer: Offer):
    return offer
```
> We can also do this.

---

**examples = ["fahim@example.com"]**
> This is an example of using the `examples` parameter in FastAPI. By providing a list of example values, you can help users understand the expected format and content of the input data. FastAPI will include these examples in the generated API documentation, making it easier for clients to know what to send in their requests.
```python
class Student(BaseModel):
    student_id: str
    student_name: str
    student_email: EmailStr = Field(examples=["student@example.com"])
    student_cgpa: float = Field(gt=0, le=4.0, examples = ["3.75"])
```
---

**Extra Data Types**
>   1. `UUID.uuid`: A universally unique identifier, often used for unique IDs. In requests and responses represented as str.  
>   2. `datetime.datetime` : A date and time representation. In requests and responses represented as str in ISO 8601 format, like: 2008-09-15T15:53:00+05:00.    
> 3. `datetime.date` : A date representation. In requests and responses represented as str in ISO 8601 format, like: 2008-09-15.  
> 4. `datetime.time` : A time representation. In requests and responses represented as str in ISO 8601 format, like: 15:53:00.  
> 5. `Decimal` : A fixed-point decimal representation. In requests and responses represented as str, like: 3.14.  
> 6. `datetime.timedelta` : A duration representation. In requests and responses represented as str, like: P1DT12H30M5S.  
> 7. `frozenset` : An immutable set representation. In requests and responses represented as str, like: frozenset([1, 2, 3]).In a request body, if its find a list then it will convert it into sets and remove duplicate value and in the response body it will turn the set into list.  
> 8. `bytes` : A byte representation. In requests and responses represented as str, like: b"hello".

---

**Cookie**
```python
from typing import Annotated

from fastapi import Cookie, FastAPI

app = FastAPI()


@app.get("/items/")
async def read_items(ads_id: Annotated[str | None, Cookie()] = None):
    return {"ads_id": ads_id}
```
> This is how we use cookie in our programs.

**Response Model limiting**
> In the response model we can also apply the same principles of validation and serialization as we do in request models. This means we can use Pydantic models to define the structure of our responses, ensuring that they adhere to the expected format and data types. So, we use schemas for validating the request body and we will going to use a small code for validating the response body as well.  
`@app.post("/with_response_model", response_model=Item)` we use `response_model = Item`. This will validate the response body against the `Item` schema.
```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

# ❌ Without response_model
@app.post("/no_response_model")
async def create_item_no_response_model(item: Item):
    # Add internal info that shouldn't go to the client
    return {
        "name": item.name,
        "price": item.price,
        "internal_id": 1234,   # Sensitive / unnecessary
        "status": "ok"         # Extra info
    }

# ✅ With response_model
@app.post("/with_response_model", response_model=Item)
async def create_item_with_response_model(item: Item):
    # Same data as above
    return {
        "name": item.name,
        "price": item.price,
        "internal_id": 1234,   # Will be removed automatically
        "status": "ok"         # Will be removed automatically
    }
```

> `async def create_user(user: UserIn) -> UserIn:` and `async def create_item_with_response_model(item: Item):` are the same thing. They limit the response body. But, Response model is better in most of the scenario.

**Core Basics**
> You may ask, where is the init constructor in the Pydantic model? In regular python you need to write `__init__` constructor for your classes, but with Pydantic, this is handled automatically. you just need to define the class attributes and their types. Pydantic creates the `__init__` method for you, along with other useful methods like `__repr__`, `__eq__`, and `dict()`. After creating the init constructor, it initialize all the attribute by itself under the hood.

```python
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()


class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: str | None = None


class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None


class UserInDB(BaseModel):
    username: str
    hashed_password: str
    email: EmailStr
    full_name: str | None = None


def fake_password_hasher(raw_password: str):
    return "supersecret" + raw_password


def fake_save_user(user_in: UserIn):
    hashed_password = fake_password_hasher(user_in.password)
    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)
    print("User saved! ..not really")
    return user_in_db


@app.post("/user/", response_model=UserOut)
async def create_user(user_in: UserIn):
    user_saved = fake_save_user(user_in)
    return user_saved
```
> In this code `user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)` this line may confuse you. Here, `user_in_db` is just a regular python variable. `UserInDB()` is a constructor of the `UserInDB` class or you can say UserInDB pydantic model.pydantic autometiaclly creates the `__init__` method for you.So here, I am creating a object of the `UserInDB` class.By calling the constructor, I am initializing all the attributes with the values from the dictionary. By using the `UserInDB.dict()` method we are turning a Pydantic model information into a dictionary. `**UserInDB.dict()` unpack thee dictionary and passes the values as keyword arguments to the constructor. At the end, the hashed password is stored in the `hashed_password` variable of the `UserInDB` instance.

**Status code**
> 100 - 199 are for "Information". You rarely use them directly. Responses with these status codes cannot have a body.  
200 - 299 are for "Successful" responses. These are the ones you would use the most.  
200 is the default status code, which means everything was "OK".  
Another example would be 201, "Created". It is commonly used after creating a new record in the database.  
A special case is 204, "No Content". This response is used when there is no content to return to the client, and so the response must not have a body.  
300 - 399 are for "Redirection". Responses with these status codes may or may not have a body, except for 304, "Not Modified", which must not have one.  
400 - 499 are for "Client error" responses. These are the second type you would probably use the most.
An example is 404, for a "Not Found" response.  
For generic errors from the client, you can just use 400.  
500 - 599 are for server errors. You almost never use them directly. When something goes wrong at some part in your application code, or server, it will automatically return one of these status codes.

**Form()**
> `Form()` method collect data from `HTML forms`. It tells the fastapi to look fro data in the form body not in the JSON body. To use `Form()` we need to download `python-multipart` library.
```python
from typing import Annotated
from fastapi import FastAPI, Form

app = FastAPI()

@app.post("/login/")
async def login(username: Annotated[str, Form()], password: Annotated[str, Form()]):
    return {"username": username, "password": password}
```
> This is how we apply form in our code. This `Form()` tells us to collect data from Request form body.

**File**
> To use file we also need to install `python-multipart` library. Then we need to import File and UploadFile.
```python
from typing import Annotated

from fastapi import FastAPI, File, UploadFile

app = FastAPI()


@app.post("/files/")
async def create_file(file: Annotated[bytes, File()]):
    return {"file_size": len(file)}


@app.post("/uploadfile/")
async def create_upload_file(file: UploadFile):
    return {"filename": file.filename}
```
> This is the basic code of file upload in FastAPI. Both `uploadfile` and `file(byte)` does the same thing. They take a file but `uploadfile` is better than the other one because it allows smooth memory management for large file.   

> *Use Form() for plain form fields (text, numbers, etc.).  
Use File() or UploadFile for file fields.  
UploadFile is preferred for large files (less memory use + metadata).  
bytes is fine for small files (raw content in RAM).  
Can’t mix JSON Body() with Form()/File() in the same request.  
You can upload multiple files using list[UploadFile] or list[bytes].  
File() can take extra arguments like description, example, etc., which are useful for API docs.  
When you submit an HTML <form>the data is encoded differently from JSON.*

> Two common encodings:
> 1. application/x-www-form-urlencoded → Used for forms without files.
> 2. multipart/form-data → Used for forms with file uploads.  
FastAPI will read the right place in the request depending on whether it’s plain form data or file uploads.

**fileb: Annotated[UploadFile, File()] means**
> here,fileb is a variable and UploadFile is a typehint or datatype that represents a file uploaded by the client. The variable will store the data in the memory. The `File()` method is used to indicate that this data is coming from the **multipart/form-data** request body not from the JSON request body. Python and FastAPI read the JSON as request body and that `File()` prevent it.

**HTTPExeption**
```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

items = {"foo": "The Foo Wrestlers"}


@app.get("/items/{item_id}")
async def read_item(item_id: str):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item": items[item_id]}
```
> Basic code for the HTTPException handling in FastAPI.