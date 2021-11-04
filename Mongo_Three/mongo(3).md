```bash

net start mongoDB

db.shutdownServer()

net stop mongoDB

---------------------------------------------------------
---------------------------------------------------------
INSERT FIELDS

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

db.persons.deleteOne({name:'Kyaw Kyaw'})

db.persons.deleteMany({age:{$gt:30},isSporty:true})

db.persons.deleteMany({totalAge:{$gt:30},isSporty:true})

db.persons.deleteMany({totalAge:{$exists:false},isSporty:true})

db.persons.deleteMany({})

db.persons.drop()


```