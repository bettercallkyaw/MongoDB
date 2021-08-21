# Mongodb Basic CRUD

  ```bash

  mongod --version
  
  mongo

  show dbs

  use test_database

  db
  
  show collections

  db.dropDatabase()

  db.createCollection('posts')

  show collections

  db.posts.insert({
    title:'Post One',
    body:'Post of body',
    category:'Cooking',
    likes:4,
    tags:['news','events'],
    user:{
      name:'Htin Kyaw',
      email:'htinkyaw@gmail.com',
      age:21,
      status:'author'
    },
    date:Date()
  })

  db.posts.insertMany([
    {
      title:'Post One',
      body:'lorem is a fake paragraph',
      category:'News',
      date:Date()
    },
    {
      title:'Post Two',
      body:'can we love this a dog?',
      category:'Emainals',
      date:Date()
    },
    {
      title:'Post Three',
      body:'I love php,javascript and python',
      category:'Programming',
      date:Date()
    },

  ]);

  db.posts.count()
  
  db.posts.find()

  db.posts.find().pretty()

  db.posts.find({category:'News'})

  db.posts.find({category:'Cooking'}).pretty()

  db.posts.find().sort({title:1}).pretty()

  db.posts.find({category:'Programming'}).count()

  db.posts.find().sort({date:-1}).limit(2).pretty()

  db.posts.find().limit(2)

  db.posts.find().sort({title:-1}).limit(2)

  db.posts.find().forEach(function(doc){print('Blog Post: '+doc.title)})

  db.posts.findOne({category:'Programming'})

  db.posts.update({title:'Post Two'},
  {
    title:'Post Two Updated',
    body:'new posted updated in two',
    date:Date()
  },
  {
    upsert:true
  }
  )

  db.posts.update({title:'Post Two Updated'},
  {
    $set:{
      body:'Post Two Updated Again',
      category:'Polite'
    }
  }
  )

  db.posts.update({title:'Post Two Updated'},{$inc:{likes:2}})

  db.posts.update({title:'Post Two Updated'},{$rename:{likes:'views'}})

  db.posts.remove({title:'Post Three'})

  db.posts.createIndex({title:'text'})

  db.posts.find({$text:{$search:"\"Title O\""}}).pretty()
 
  db.posts.update({title:'Post Two Updated'},{$set:{views:1000}})

  db.posts.find({views:{$gt:6}}).pretty()

  db.posts.find({views:{$gte:6}}).pretty()

  db.products.insertOne({_id:1,name:"Pen",price:4.4})

  db.products.insertOne({_id:2,name:"Car",price:4444})

  db.products.find({_id:1},{name:1})

  db.users.insert({
       name:"Htin Kyaw",
       email:"HtinKyaw@hey.com",
       country:"Myanmar",
       state:"Yangon",
       city:"Yangon",
       age:21,
       reviews:[
           {
            authorName:"William Smith",
            rating:44,
            review:"Best seller Books"
           },
           {
             authorName:"John Doe",
             rating:42,
             review:"Best Seller On udemy"  
           }
       ],
       kyawSkill:{
           languate:"PHP"
       }
   })


 db.users.insert({
 firstName:'Htin',
 lastName:'Kyaw',
 fullName:'Htin Kyaw',
 email:'htinkyaw@gmail.com',
 location:'Myanmar,Shan State,Taunggyi,MA 333',
 isMarried:'will come',
 hobbies:['hiking','cooking','walking'],
 age:21,
 language:['php','javascript','python','sql','mongodb'],
 framework:['laravel','django','node js framework'],
 socialMedia:[
       {
       facebook_account:'https:://www.facebook.com/profile.php?id=333332fjae'
       },
       {
       twitter_account:'https:://www.twitter.com/htinkyaw'
       }
 ],
 date:Date()
 })


db.users.insert({
  fullName:'john smith',
  family:['robet smith','kate smith','bob smith'],
  job:'software developer',
  age:22,
  salary:45678,
  hobbies:['hiking','sports','movies'],
  city:'boston',
  country:'USA',
  profileLinks:{
    facebook:'www.facebook.com/profile.php?id=343',
    twitter:'www.twitter.com/@johnsmith23',
    github:'www.github.com/bettercalljohn'
  },
  language:['php','java','python'],
  framework:['laravel','Django','bootstrap'],
  address:{
    street:'BA'
  },
  date:Date()
})

```


