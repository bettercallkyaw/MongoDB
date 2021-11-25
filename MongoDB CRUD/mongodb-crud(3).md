```bash

net start mongoDB

db.shutdownServer()

net stop mongoDB

mongod --version

mongo

show dbs

use mongodb_crud

db

db.dropDatabase()

db.createCollection('posts')

show collections

---------------------------------------------------------
---------------------------------------------------------
INSERT FIELDS

db.posts.insert({
    title:'Title One',
    body:'body one',
    category:'Programming',
    likes:23,
    tags:['python','php','javascript'],
    user:{
      name:'Bob Smith',
      email:'bob@testing.com',
      age:23,
      status:'admin'
    },
    date:Date()
  })

 db.posts.insertMany([
    {
      title:'Title Two',
      body:'body two',
      category:'Frameworks',
      tags:['laravel','django','express']
      date:Date()
    },
    {
      title:'Title Three',
      body:'body three',
      category:'Phone',
      tags:['huawei','apple','oppo']
      date:Date()
    },
    {
      title:'Title Four',
      body:'body four',
      category:'Search Engine',
      tags:['google','yahoo','bing']
      date:Date()
    },

  ]);

use contactData

db.persons.insertOne({name:'Htin Kyaw',age:30,hoppies:['sports','cooking']})

db.persons.insertMany([{name:'John Doe',age:20,hoppies:['hiking','walking']}])

db.persons.insertMany([{name:'ashly kate',email:'ashly@gmail.com',age:20},{name:'william smith',email:'william@gmail.com',age:21}])

-------------------------------------------------
WRITE ERRORS

db.persons.insert([{name:'htin kyaw',age:21},{name:'min oo',age:20}])
-----------------------------------------------------

db.hobbies.insertMany([{_id:'sports',name:'Sports'},{_id:'hiking',name:'Hiking'},{_id:'cars',name:'Cars'}])

---------------------------------------------------------------------------------
"errmsg" : "E11000 duplicate key error collection: Max_Mongo_Two.hoppies index: _id_ dup key: { _id: \"hiking\" }"

db.hobbies.insertMany([{_id:'yoga',name:'Yoga'},{_id:'hiking',name:'Hiking'},{_id:'movies',name:'Movies'}])

db.hobbies.find().pretty()

db.hobbies.insertMany([{_id:'walking',name:'Walking'},{_id:'hiking',name:'Hiking',},{_id:'laptop',name:'laptop'}],{ordered:false})

db.users.insert({
       name:"Bob Smith",
       email:"bob@testing.com",
       country:"USA",
       state:"California",
       city:"Boston",
       age:23,
       reviews:[
           {
            authorName:'William Smith',
            rating:44,
            review:'Best seller Books'
           },
           {
             authorName:'John Doe',
             rating:42,
             review:'Best Seller On udemy'  
           }
       ],
       bobSkill:{
           languate:'PHP'
       }
   })

db.users.insert({
 firstName:'Bob',
 lastName:'Smith',
 fullName:'Bob Smith',
 email:'bob@faker.com',
 location:'USA,California State,Boston,MA 333',
 isMarried:'comming soon',
 hobbies:['hiking','cooking','walking'],
 age:23,
 language:['php','javascript','python','sql','mongodb'],
 framework:['laravel','django','node js framework'],
 socialMedia:[
       {
       facebook_account:'https:://www.facebook.com/profile.php?id=333332fjae'
       },
       {
       twitter_account:'https:://www.twitter.com/bobsmith'
       }
 ],
 date:Date()
})

db.users.insert({
  fullName:'smith row',
  family:['robet smith','kate smith','bob smith'],
  job:'software developer',
  age:22,
  salary:45678,
  hobbies:['hiking','sports','movies'],
  city:'boston',
  country:'USA',
  profileLinks:{
    facebook:'www.facebook.com/profile.php?id=343',
    twitter:'www.twitter.com/@smithrow23',
    github:'www.github.com/bettercallsmith'
  },
  language:['php','java','python'],
  framework:['laravel','Django','bootstrap'],
  address:{
    street:'BA'
  },
  date:Date()
})
-----------------------------------------------------------------------------------

db.persons.insertOne({name:'Htin kyaw',age:32},{writeConcern:{w: 0}})

db.persons.insertOne({name:'Alex',age:21},{writeConcern:{w: 1}})

db.persons.insertOne({name:'Michael',age:34},{writeConcern:{w: 1,j: false}})

db.persons.insertOne({name:'Bon',age:55},{writeConcern:{w: 1,j: true}})

db.persons.insertOne({name:'Aliya',age:22},{writeConcern:{w: 1,j: true,wtimeout: 200}})

db.persons.insertOne({name:'Aliya',age:22},{writeConcern:{w: 1,j: true,wtimeout: 1}})

db.persons.insertOne({name:'Mg Mg',hobbies:[{title:'Sports',frequency:3},{title:'Cooking',frequency:6}]})

db.sales.insertMany([{volume:100,target:120},{volume:89,target:80},{volume:200,target:177}])

----------------------------------------------------
----------------------------------------------------
FIND FIELDS

db.posts.count()
  
db.posts.find()

db.posts.find().pretty()

db.posts.find({category:'Programming'})

db.posts.find({category:'Programming'}).pretty()

db.posts.find({category:'Programming'}).count()

db.posts.find().sort({title:1}).pretty()

db.posts.find().sort({date:-1}).limit(2).pretty()

db.posts.find().limit(2)

db.posts.find().sort({title:-1}).limit(2)

db.posts.find().forEach(function(doc){print('Blog Post: '+doc.title)})

db.posts.findOne({category:'Programming'})

db.posts.find({views:{$gt:6}}).pretty()

db.posts.find({views:{$gte:6}}).pretty()

db.persons.find({age: {$exists: true}}).pretty()

db.persons.find({age: {$exists: false}}).pretty()

db.persons.find({age:{$exists:true}}).sort({name:1}).pretty().limit(1)

db.persons.find({age: {$exists: true,$ne: null}}).pretty()

db.persons.find({name:{$type: "string"}}).pretty()

db.persons.find({age:{$type: "number"}}).pretty()

db.persons.find({phone: {$type: "number"}}).pretty()

db.sales.find({$expr: {$gt: ["volume","target"]}}).pretty()

db.sales.find({$expr: {$gt: ["$volume","$target"]}}).pretty()

db.sales.find({
    $expr:{
        $gt:[
            {
                $cond:{
                    if:{$gte:["$volume",190]},
                    then:{$subtract:["$volume",10]},
                    else:
                    "$volume"
                }
            },
            "$target"
        ]
    }
}).pretty()

db.persons.find({"hobbies.title": "sports"}).pretty()

db.persons.find({hobbies: {$size:2}}).pretty()

db.persons.find({$and: [{"hobbies.title": "Sports"},{"hobbies.frequency":{$gte: 2}}]}).pretty()

db.persons.find({$and: [{"hobbies.title": "Sports"},{"hobbies.frequency":{$gte: 3}}]}).count()

db.persons.find({hobbies: {$elemMatch: {title:"Sports",frequency: {$gte: 3}}}}).pretty()

db.persons.find({$and:[{"hobbies.title": "Sports"},{"hobbies.frequency":{$gte:3}}]}).pretty()

db.persons.find({"hobbies.frequency":{$gt:2}}).count()
---------------------------------------------------------------------------
---------------------------------------------------------------------------

UPDATE FIELDS

db.posts.update({title:'Title Four'},
  {
    title:'Title Four Updated',
    body:'body four updated',
    date:Date()
  },
  {
    upsert:true
  }
  )

db.posts.update({title:'Title Four Updated'},
  {
    $set:{
      title:'Title Four',  
      body:'body four',
      category:'Social Media',
      tags:['facebook','twitter','pin'],
      date:Date()
    }
  }
  )

db.posts.update({title:'Title One'},{$inc:{likes:2}})

db.posts.update({title:'Title One'},{$rename:{likes:'total_views'}})

db.posts.update({title:'Title One'},{$set:{total_views:1000}})

db.persons.updateOne({_id:ObjectId("5fab3d9dfd6b9fb42cc781f3")},{$set:{hobbies:[{title:'Sports',frequency:5},{title:'Cooking',frequency:3},{title:'Hiking',frequency:1}]}})


db.persons.updateMany({"hobbies.title":"Sports"},{$set:{isSporty:true,age:40,
phone:393939393939}})

db.persons.updateOne({name:'Htin Kyaw'},{$inc:{age: -9}})

db.persons.updateOne({name:'Htin Kyaw',},{$min:{age:22}})

db.persons.updateOne({name:'Htin Kyaw'},{$max:{age:23}})

db.persons.updateOne({name:'Htin Kyaw',},{$max:{age:40}})

db.persons.updateMany({isSporty:true},{$set:{phone:null}})

db.persons.updateMany({isSporty:true},{$unset:{phone: ""}})

db.persons.updateMany({},{$rename:{age: "totalAge"}})

db.persons.updateOne({name:"Mg Mg"},{$set:{age:33,hobbies:[{title:'Food',frequency:3}],
isSporty:true}})

db.persons.updateOne({name:"Mg Mg"},{$set:{age:33,hobbies:[{title:'Food',frequency:3}],isSporty:true}},{upsert:true})

db.persons.updateMany({hobbies:{$elemMatch:{title:"Sports",frequency:{$gte:3}}}},{
    $set:{
        "hobbies.$.highFrequency":true
    }
})


db.persons.updateMany({"hobbies.frequency":{$gt:2}},{$set:{"hobbies.$.goodfrequency":true}})

db.persons.updateMany({totalAge:{$gt:30}},{$inc:{"hobbies.$[].frequency":-1}})

db.persons.updateMany(
    {
        "hobbies.frequency":{$gt:2}
    },
    {
        $set:{
            "hobbies.$[el].goodFrequency":true
        }
    },
    {
        arrayFilters:[
            {
                "el.frequency":{
                    $gt:2
                }
            }
        ]
    }
)

db.persons.updateOne({name:'Mg Mg'},{$push:{hobbies:{title:'Sports',frequency:2}}})

db.persons.updateOne(
    {
        name:'Mg Mg'
    },
    {
        $push:{
            hobbies:{
                $each:[
                    {
                        title:'Good Wine',
                        frequency:1
                    },
                    {
                        title:'Hiking',
                        frequency:2
                    }
                ],
                $sort:{
                    frequency:-1
                }
            }
        }
    }
)

db.persons.updateOne({name:'Mg Mg'},{$pull:{hobbies:{title:'Hiking'}}})

db.persons.updateOne({name:'Kyaw Kyaw'},{$pop:{hobbies:1}})

db.persons.updateOne({name:'Mg Mg'},{$addToSet:{hobbies:{title:'Hiking',frequency:4}}})

-------------------------------------------------------------------------------
-------------------------------------------------------------------------------

DELETE FIELDS

db.posts.remove({title:'Title Four'})

db.persons.deleteOne({name:'Kyaw Kyaw'})

db.persons.deleteMany({age:{$gt:30},isSporty:true})

db.persons.deleteMany({totalAge:{$gt:30},isSporty:true})

db.persons.deleteMany({totalAge:{$exists:false},isSporty:true})

db.persons.deleteMany({})

db.persons.drop()

-------------------------------------------------------------------------------
-------------------------------------------------------------------------------
working with index

db.posts.createIndex({title:'text'})

db.posts.find({$text:{$search:"\"Title O\""}}).pretty()

```
