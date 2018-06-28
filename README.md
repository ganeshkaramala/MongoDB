# MongoDB

http://info-mongodb-com.s3.amazonaws.com/ReferenceCards15-PDF.pdf

# Features

# Test

cd ..

cd ..

cd mongodb

cd homework

cd hw3-2

mvn compile exec:java -Dexec.mainClass=course.BlogController

 mongoimport -d school -c students < students.json

db.students.find({ "scores" : { "$elemMatch" : { "type" : "homework"} }});

db.posts.aggregate([{$unwind:"$comments.author"},{$group:{_id:"$comments.author",total:{$sum:_id}}},{$sort:{total:1}},{$limit:{1}}])

h.w ---5-1 
**************************************************************************************************************************************
db.posts.aggregate([{$unwind:"$comments"},{$group:{_id:{author:"$comments.author"},total:{$sum:1}}},{$sort:{total:-1}}])
**************************************************************************************************************************************


h.w 5-2 
**************************************************************************************************************************************
mongoimport -d test -c grades --drop homework/hw5-2/small_zips.json

Q. Please calculate the average population of cities in California (abbreviation CA) and New York (NY) (taken together) with populations over 25,000. 

 ANS
    use test
	
	db.grades.aggregate([{$match:{ state:"CA",state:"NY",pop:{$gte:250000}}},{$group:{ _id:null,ppo:{$avg:"$pop"}}}])
**************************************************************************************************************************************



hw 5- 3
**************************************************************************************************************************************
mongoimport -d test -c grades --drop homework/hw5-3/grades.json

 Q. Your task is to calculate the class with the best average student performance. This involves calculating an average for each student in each class of all non-quiz assessments and then averaging those numbers to get a class average. To be clear, each student's average includes only exams and homework grades. Don't include their quiz scores in the calculation.
 
 ans 
 
    avg of each stu---- db.grades.aggregate([{$unwind:"$scores"},{$match:{ "scores.type":"homework","scores.type":"exam"}},{$group:{_id:{studentid:"$student_id",classid:"$class_id"},avg_stu:{$avg:"$scores.score"}}}])
	
	avg of class---

	db.grades.aggregate([{$unwind:"$scores"},{$match:{ "scores.type":"homework","scores.type":"exam"}},{$group:{_id:{studentid:"$student_id",classid:"$class_id"},avg_stu:{$avg:"$scores.score"}}},{$group:{_id:"$_id.classid",avg_class:{$avg:"$avg_stu"}}},{$sort:{avg_class:1}}])
	
	
	db.grades.aggregate([{$unwind:"$scores"},{$match:{ "scores.type":"homework","scores.type":"exam"}},{$group:{_id:{studentid:"$student_id",classid:"$class_id"},avg_stu:{$avg:"$scores.score"}}},{$match:{class_id:"2"}}])
	
	
	
*************************************************FINAL EXAM**********************************************

Q1 :   
      
Q2 :   
	  db.messages.aggregate
	  ([
	   {$unwind:"$headers.To"},
	   {$group:{_id:{id:"$_id",from:"$headers.From"},"TO":{$addToSet:"$headers.To"}}},
	   {$unwind:"$TO"},
	   {$group:{"_id":{ sender:"$_id.from","receiver":"$TO"},total_count:{$sum:1}}},
	   {$sort:{total_count:-1}},
	   {$limit:2}
	  ])

Q3 :  db.messages.update({"headers.Message-ID":"<8147308.1075851042335.JavaMail.evans@thyme>"},{$addToSet:{"headers.To":"mrpotatohead@10gen.com"}})
	
Q4 :  postsCollection.update( new BasicDBObject("permalink", permalink),
	                            new BasicDBObject("$inc",new BasicDBObject("comments."+ordinal+".num_likes",1)));

Q5 :

     
	
	
Q7 : 	MongoClient c =  new MongoClient(new MongoClientURI("mongodb://localhost"));
            DB db = c.getDB("final7");
            int i =0;
            DBCollection album = db.getCollection("albums");
            DBCollection image = db.getCollection("images");
            
            DBCursor cur = image.find();
            cur.next();
            
            while (cur.hasNext()){
                Object id = cur.curr().get("_id");
               DBCursor curalbum = album.find(new BasicDBObject("images", id));
               if(!curalbum.hasNext()){
                   image.remove(new BasicDBObject("_id", id));
               }
               cur.next();
            }
        }
	
	db.albums.aggregate({$unwind:"$images"},{$group:{_id:null,sum:{$sum:"$images"},count:{$sum:1}}}
	
	db.images.find({"tags":"sunrises"}).count()
	
	
     



