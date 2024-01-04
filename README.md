SQL - NoSQL Material


MongoDB Quick installation 
```java
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.mongodbexample;

import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoClient;
import com.mongodb.client.MongoDatabase;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.model.Filters;
import com.mongodb.client.model.Updates;
import org.bson.Document;
public class MongoDBExample {
    public static void main(String[] args) {
        // Selecting the database
        try ( // Connecting to the MongoDB server
            MongoClient mongoClient = MongoClients.create("mongodb://localhost:27017")) {
            // Selecting the database
            MongoDatabase database = mongoClient.getDatabase("mydb");
            
            // Access the collections
            MongoCollection<Document> teamsCollection = database.getCollection("teams");
            MongoCollection<Document> playersCollection = database.getCollection("players");

            // Iterate over each team
            for (Document team : teamsCollection.find()) {
                // Adjust these lines to match the format stored in MongoDB
                String teamShort = team.getString("Short"); // Assuming extra quotes are part of the string
                String teamFull = team.getString("Team");  // Adjust field name and format if necessary
                System.out.println("Team Short"+teamShort +" and Full name:"+teamFull);
                // Update the players' team field where it matches the team's short code
                playersCollection.updateMany(
                        Filters.eq("Team",   teamShort),
                        Updates.set("Team",teamFull)
                );
            }
        }
    }
}

```
