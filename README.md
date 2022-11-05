# Telephone-Directory
#CURD operation using the python

import pymongo
from pymongo import MongoClient

client=pymongo.MongoClient('mongodb://localhost:27017/')
db=client["Telephone_directory"]
col=db["Document"]

#create operation

data= [{"name":"sentha","address":"no 158 india","phone":8939035001},
       {"name":"milan","address":"no 159 india","phone":8939035001},
       {"name":"senthamilan","address":"no 160 india","phone":8929035001}
      ]

#create multiple document with separate obj_ids  
New_collecttion=col.insert_many(data)

#create one document and add it to collection
data_new={"name":"messi","address":"no 10 south africa","phone":9034327392}
New_collection1=col.insert_one(data_new)

#read operation

for i in col.find():
    print(i)
myquery={}
for i in col.find(myquery):
    print(i)

#update operation

#it upddates all the occurrences
col.update_many({"name":"messi"},{"$set":{"phone":8939035001}})
for i in col.find():
    print(i)

#it update the first occurrence
col.update_one({"name":"messi"},{"$set":{"phone":9750667893}})    
for i in col.find():
    print(i)

#delete operation

#delete the first occurance
col.delete_one({"name":"messi"})
for i in col.find():
    print(i)
    
#delete all the occurrances
col.delete_many({"name":"messi"})
for i in col.find():
    print(i)
