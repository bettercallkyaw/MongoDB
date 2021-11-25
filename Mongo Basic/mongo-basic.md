```bash

# One To One
# one paitents has one disease summary,a disease summary belongs to one patient

use hospital

db.patients.insertOne({
    name:'Bob Smith',
    age:21,
    diseaseSummary:'summary-bob-1'
})

db.patients.drop()

db.patients.findOne().diseaseSummary

db.diseaseSummaries.insertOne({
    _id:'summary-bob-1',
    diseases:['cold','broken leg']
})

var dis=db.patients.findOne().diseaseSummary
dis

db.diseaseSummaries.findOne({_id: dis})

db.patients.deleteMany({})

db.patients.insertOne({
    name:'Bob Smith',
    age:23,
    diseaseSummary:{
        diseases:['head','broken leg']
    }
})

---------------------------------------
_______________________________________
# One To One
# one person has one car,a car belongs to one person 
use carData

db.persons.insertOne({
    name:'Bob Smith',
    car:{
        model:'BMW',
        price:33333
    }
})

db.persons.insertOne({name:'Bob Smith',salary:3333333,age:23})

db.persons.insertOne({model:'BMW',price:444444,owner:ObjectId("5f46377385fcb1e50cd06b6e")})

---------------------------------------
_______________________________________
# One To Many
# one thread has many answers,one answer belongs to one question thread

use support

db.questionThread.insertOne({
    creator:'Bob Smith',
    question:'which frameworks use for server-side languate?',
    answers:['laravel','vue','bootstrap']
})

db.questionThread.insertOne({
    creator:'Smith Row',
    question:'which frameworks use for frontend?',
    answers:[
        {text:'angular'},
        {text:'django'},
        {text:'express'}
    ]
})

db.answers.insertMany([
    {_id:'answers1',text:'php'},
    {_id:'answers2',text:'javascript'},
    {_id:'answers3',text:'python'}
])

---------------------------------------
_______________________________________
# One To Many

# one city has many citizens,one citizen belongs to one city

use cityData

db.cities.insertOne({name:'Boston',coordinates:{lan:21,lng:44}})

db.citizens.insertMany([
    {
        name:'Bob Smith',
        ctiyId:'boston1'
    },
    {
        name:'Smith Row',
        cityId:'boston2'
    }
])

---------------------------------------
_______________________________________

# Many To Many
# one customer has many products(via orders),a product belongs to many customers

use shop

db.products.insert({car:'BWM',price:444444})

db.customers.insertOne({name:'Bob Smith',age:23})

db.orders.insertOne({
productId:ObjectId('5f463f5f85fcb1e50cd06b75'),
customerId:ObjectId('5f463f6085fcb1e50cd06b76')})

db.customers.updateOne({},
{$set: {orders:[{title:'lords of the ring',price:333.33,quantity:33}]}})

---------------------------------------
_______________________________________
# Many To Many
# one book has many authors,an author belongs to many books

use bookRegistry

db.books.insertOne({
    name_title:'lord of the ring',
    name_title:'the king of hobbit',
    authors:[
        {
            name:'Bob Smith',
            age:23
        },
        {
            name:'Smith Row',
            age:24
        }
    ]
})

db.authors.insertMany([
    {
        name:'Bob Smith',
        age:23,
        addrees:{
            street:'MA 23'
        }
    },
    {
        name:'Smith Row',
        age:24,
        address:{
            street:'BD 12'
        }
    }
])

db.books.aggregate([{$lookup: {from:'author',localField:'author',foreignField:'_id',as:'creators'}}]).pretty()

---------------------------------------
_______________________________________

use blog

db.users.insertMany([
    {
        name:'Bob Smith',
        age:23,
        email:'bob@testing.com'
    },
    {
        name:'Smith Row',
        age:24,
        email:'row@faker.com'
    }
])

db.posts.insertOne({
 title:'hello world',
 text:'hello lorme is not a really paragraph',
 category:'books collection',
 tags:['lords of the rings,the hobbits'],
 creator:ObjectId("600f647ea465e3f98c2cf047"),
 comments:[
    {
      text:'nice books',
      author:ObjectId("600f647ea465e3f98c2cf047")
    }
 ]})
 
```