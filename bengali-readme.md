# পাইথনে প্যাকেজ তৈরি 

- লেখক এবং উৎস : Elise Olson, [The Hitchhiker's Guide to Packaging](http://the-hitchhikers-guide-to-packaging.readthedocs.org/en/latest/quickstart.html), [Bill Mills](https://github.com/BillMills)
- গবেষণা ক্ষেত্র : যেকোনো 
- বিষয় :  পাইথনে অন্তত একটি প্যাকেজ তৈরি করা  , দৃঢ়তার সাথে ।
- অনুবাদক  : [Bolaram Paul](https://github.com/bolaram)

# কেন আমরা এটা করছি ?

বিজ্ঞানের ক্ষেত্রে কোডিং  করার ক্ষেত্রে সবচেয়ে গুরুত্ব পূর্ণ বিষয় হল  আমরা আমাদের কোড পুনরায় ব্যবহার  করতে পারি  নতুন তৈরি ছাড়া , এটা আমাদের নতুন প্রজেক্টের ক্ষেত্রে পুরনো  কাজের কোড ব্যবহারে সুযোগ দেয় ।  আমাদের কোডকে প্যাকেজে সমন্বিত করলে এটা কোডের পুনরায় ব্যবহার সহজ করে দেয় -  যখন আমরা এটা করব ,  আমরা আমদের সকল কঠিন কাজের কোড শুধু একটি মাত্র কমান্ড দ্বারা অ্যাক্সেস করতে সফল হব ,অনেকটা বিখ্যাত  নুম্পি বা ম্যাটপ্লোটলিব প্যাকেজের মত । 

## সেটআপ পদ্ধতি 

এই টিউটোরিয়াল তোমাকে নিয়ে যাবে    [demo Python package](https://github.com/BillMills/python-package-example) এর মধ্য দিয়ে ,  এবং  তোমার নতুন প্যাকেজ তৈরিতে বিস্তারিত ব্যাখ্যা দিবে . এই ডেমো টা সম্পূর্ণ ফাংশনাল , তাই তুমি এটা তোমার প্যাকেজের জন্য টেমপ্লেট হিসেবে ব্যবহার করতে পার । 

আমরা এই লিসনে আমরা নিজেদের প্যাকেজ তৈরি করব ,  কিন্তু তুমি উপরের এই ডেমো তা উদাহরন হিসেবে দিতে পার । 

## 1. মূল বিষয় 

একটি সাধারন পাইথন প্যাকেজের মুল গঠন এরকম হয় :

```
project
|
|
|__ myPackage
|     |
|     |__ somePython.py
|     |__ __init__.py
|
|__ tests
      |__ test.py
```

এগুলো ব্যবহার করে তৈরি শুরু কর  ( লক্ষ্য রাখতে হবে যে  `init` in `__init__.py` এর পূর্বে ও পরে দুইটি  underscores হবে  ). এটা করে ফেললে , তুমি  পাইথনের যে ক্লাস ও ফাংশন পুনঃ ব্যবহার করতে চাও  সেগুলো `somePython.py` এখানে বসাও :

```
import numpy

def fahrToKelv(temp):
    '''
    takes a temperature `temp` in fahrenheit and returns it in Kelvin
    '''

    kelvin = 5./9. * (temp - 32.) + 273.15

    return kelvin
``` 

তোমার পাইথন মডিউল ইম্পোরট কর  (তুমি জত খুশি ততগুলি করতে পার )      in `__init__.py`:

```
import somePython
```

এবং সবসময় প্রত্যেক ফাংশনের জন্য  সবসময়  `test.py` তৈরি করবে :

```
from myPackage import somePython

def test_fahrToKelv():
    '''
    make sure freezing is calculated correctly
    '''
    
    assert somePython.fahrToKelv(32) == 273.15, 'incorrect freezing point!'
```

তোমার কাছে আগে থেকেই উদাহরন বা টেস্ট থাকতে পারে ; এগুলো ভিন্ন নয় ,  শুধু যথাযথ ভাবে সাজানো আছে . এখন আমরা পাইথনের পাকেজিং এ বিস্তারিত যা ঘটে তা দেখতে পারি । 

## 2. অনুমোদন 

পাকেজিং কোড পুনরায় ব্যবহার করা যাবে এবং  শেয়ার করা যাবে -  এবং তোমার কঠিন কাজের সম্মান ও সবাইকে তোমার কাজ বুঝতে সাহায্য করার জন্য  ও তোমার কাজ ব্যবহারের অনুমুতির জন্য , তোমার একটি লাইসেন্স প্রয়োজন ।   লক্ষ্য রাখ , যদি লাইসেন্স না থাকে তাহলে যে যা খুশি তাই করতে পারবে না ! অনুমোদিত কোড থাকে সন্দেহজনক ধূসর এলাকায় অনেকটা মহামারির মত । 

এখানে  [ অসংখ্য ওপেনসোর্স লাইসেন্স ]  (http://opensource.org/licenses/) আছে ; তোমার যেটা খুশি নিতে পার , কিন্তু  ** তোমার নিজের নামে লিখনা **, যদিনা তুমি একজন উকিল হও ; উপরের লাইসেন্স গুলো উকিল দ্বারা  পঠিত  তোমার স্বার্থ সংরক্ষনের জন্য ।  

যদি তুমি নিশ্চিত না হও কোন লাইসেন্স নিবে তাহলে , এটা নাও  [MIT](http://opensource.org/licenses/MIT) ।  এই MIT লাইসেন্সের অধিনে কেউ তোমার কোড ব্যবহার করতে পারবে ,কিন্তু কোডে তোমার মালিকানা থাকবে ।

যে লাইসেন্স তা তুমি নিবে সেটা , সেটার  **সম্পূর্ণ**  টেক্সট কাট করে নতুন  LICENSE.txt ফাইলে পেস্ট কর তোমার প্রোজেক্ট ফোল্ডোরে  (`project` উপরে উদাহরন দেখ ), এবং কপিরাইট লাইনে তোমার নাম ও তারিখ দাও  ।

## 3. তোমার প্যাকেজ বর্ণনা কর 

প্যাকেজ বর্ণনা করা থাকে  ডিরেক্টরির `setup.py` ফাইলে ।  এই উদাহরন টি তোমার নিজের  `setup.py` তে কপি কর , এবং সকল ফিল্ড পরিবর্তন কর ; বাতিক্রম গুলো টেবিলে দেউয়া হল .

```
from setuptools import setup, find_packages

setup(
    name='python-package-example',
    version='0.1',
    packages=find_packages(exclude=['tests*']),
    license='MIT',
    description='An example python package',
    long_description=open('README.txt').read(),
    install_requires=['numpy'],
    url='https://github.com/BillMills/python-package-example',
    author='Bill Mills',
    author_email='myemail@example.com'
)
```

This table contains descriptions of the parameters you may consider changing; others can be left as is.

Parameter | মন্তব্য 
----------|---------
name      | তোমার প্যাকেজের নাম হিসেবে ব্যবহার হবে , যেমন  `numpy` বা  `matplotlib` । 
version   | তোমার বর্তমান প্যাকেজের ভার্শন ; এখানে দেখ  [pep440](https://www.python.org/dev/peps/pep-0440/) ব্যাখ্যার জন্য । 
license   | তোমার লাইসেন্সের নাম 
description | তোমার প্যাকেজের বর্ণনা 
install_requires | এই প্যাকেজের জন্য ব্যবহৃত সকল প্যাকেজের লিস্ট ;  প্যাকেজ মানেজার সেগুলো প্রয়োজন অনুযায়ী ইন্সটল করে নিবে 
url | তোমার প্যাকেজের ওয়েবসাইট । 
author | এটা তুমি 
author_email | তোমার ইমেইল ঠিকানা 

এই `setup.py` ফাইলটি  তোমার প্যাকেজের জন্ন মেশিন রিডেবল  বর্ণনা ;  মানুষের জন্য , একটি  README.txt ফাইল আছে , প্রজেক্ট ডিরেক্টরিতে ।  , তোমার প্যাকেজ কিভাবে ব্যবহার করবে , কিভাবে অবদান রাখবে , এটার বর্ণনা সমস্ত লিখ এখানে । 

## 4. অতিরিক্ত ডেটা 

যদি তোমার প্যাকেজে কোন অতিরিক্ত ডেটা ফাইল রাখতে হয় তাহলে , তোমার প্রয়োজন হবে একটি  MANIFEST.in ফাইল  তোমার প্রজেক্ট ডিরেক্টরীতে।  প্রথমে, তোমার ডেটা রাখ  `packageData` এই  ফোল্ডারের ভিতর যা আছে  `myPackage` এর ভিতর ; তোমার প্রজেক্ট দেখতে এরকম হউয়া উচিত :

```
project
|
|
|__ myPackage
|     |
|     |__ packageData
|     |     |
|     |     |__ myData.dat
|     |__ somePython.py
|     |__ __init__.py
|
|__ tests
|     |__ test.py
|
|__ setup.py
|
|__ LICENSE.txt
|
|__ MANIFEST.in
|
|__ README.txt
```

যেখানে তোমার ডেটা থাকবে  `myData.dat` তে ; পুনরায় , তোমার জত খুশি ততগুলি ফাইল থাকতে পারে । প্রত্যেক ডেটা ফাইলের জন্য , একটি লাইন  যোগ কর  `MANIFEST.in` এটা তোমার ডেটার জন্য একটি পাথ তৈরি করবে :

```
include myPackage/packageData/myData.dat
```

সকল ফাইল   `MANIFEST.in` এর  , প্যাকেজ ইন্সটলের সময় যোগ হবে ।

## 5. এটিকে বন্ধ কর ও পাঠাও 

এত তুকুই , সব হয়ে গেছে , এখন তুমি ব্যবহার করতে পার 

```
python setup.py sdist
```

পাইথন তোমার প্যাকেজ গুলো কে একত্র করবে  `dist`(ribution) ফোল্ডারে । 

### GitHub এ বণ্টন 

git এর ক্ষেত্রে , উপরের চিত্রের মত সব যোগ কর  নতুন এই  `dist` ফোল্ডারে   ,git repository থাকে প্রজেক্টের উপরে  (`project`), এতাকে চালু কর  GitHub এ ।  এখন , পৃথিবীর যে কেউ তোমার প্যাকেজ ইন্সটল করতে পারবে  (  মনে রেখ  তোমার নাম দিতে `yourName` GitHub এর user name এ  এবং `repoName` হবে তোমার ইউজার নেম অনুযায়ী ):

```
sudo pip install git+git://github.com/yourName/repoName.git#egg=repoName
``` 

### PyPI এ বণ্টন 

PyPI এ  বণ্টন  Git এ বণ্টনের চেয়ে সহজ , কিন্তু তোমাকে দুই জাইগায় প্যাকেজ টা দেখতে হবে যদি তুমি    GitHub এ  ডেভোলপ করতে চাও এবং  PyPI এ বণ্টন করতে চাও ।  প্রথমে PyPI এ প্যাকেজ চালু করার জন্য , [  PyPI এ নতুন  একাউন্ট তৈরি কর  ](https://pypi.python.org/pypi), এবং ফিরে যাও তোমার প্যাকেজ এ  `package` ফোল্ডারে ।

```
python setup.py register
```

তোমার প্যাকেজ নাম পেতে  - সেগুলো অবশ্যই একক হতে হবে ।  তারপর , তোমার প্যাকেজ আপলোড কর ; যখন তুমি তোমার কোডের নতুন ভার্শন বের করবে তখন  প্রতিবার তোমাকে এটা করতে হবে :

```
python setup.py sdist upload
```

এখন , তুমি  এবং পৃথিবীর যে কেউ  তোমার প্যাকেজ ইন্সটল করতে পারবে  এমনভাবে :

```
sudo pip install your-package-name
```

## 6. উদাহরণ চেষ্টা কর 

উপরে বর্ণনা কৃত ডেমো প্যাকেজ তুমি ইন্সটল করতে পার , চালু করার মাধ্যমে :

```
sudo pip install git+git://github.com/billmills/python-package-example.git#egg=python-package-example
```

PyPI থেকে :

```
sudo pip install python-package-example
```

এই ডেমো প্যাকেজ এর উপরের মত সমান কোড আছে । চালু করার পর নিচের স্ক্রিপ্ট দিয়ে চালু কর :

```
import myPackage

print myPackage.somePython.fahrToKelv(32)
```

এই সাধারন  `import` কমান্ডের দ্বারা , আমরা  (এবং আমাদের সকল বন্ধুরা )  `fahrToKelv`  ফাংশন ব্যবহার করতে পারব  যা আমরা আগে টেস্ট করেছি । প্যাকেজের ভিতর তুমি যত খুশি ফাংসন আইডিয়া দিতে পার  ; শুধু এই  `somePython.py` ফাংশন টি  যোগ করতে থাক  (  এবং সেগুলো  টেস্ট কর `test.py`!), অথবা আরও পাইথন ফাইল অ্যাড কর  `somePython.py` (এটা যোগ করতে ভুলোনা  in `__init__.py`), অথবা  অনেক ফোল্ডার যোগ কর এতে  `myPackage` একপই নিয়মে , এবং তুমি নিজের পছন্দ ম টুলস তৈরি করতে পার । 




