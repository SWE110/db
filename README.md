# Tables

These are the tables we used for our project. 

Recipe
```
CREATE TABLE recipe 
  ( 
     meal_id               UUID DEFAULT Uuid_generate_v4() PRIMARY KEY, 
     meal_name             CHARACTER varying(255) NOT NULL, 
     image                 TEXT[], 
     aggregate_rating      DOUBLE PRECISION, 
     author                CHARACTER varying(255), 
     date_published        TIMESTAMP WITH TIME zone DEFAULT current_timestamp, 
     description           TEXT, 
     keywords              TEXT[], 
     recipe_category       TEXT[], 
     recipe_cuisine        CHARACTER varying(255), 
     recipe_ingredient     TEXT[], 
     recipe_ingredient_str TEXT, 
     recipe_instructions   TEXT[], 
     recipe_yield          CHARACTER varying(255), 
     total_time            INTERVAL 
  ); 
```

User
```
CREATE TABLE USER 
  ( 
     user_id           CHARACTER VARYING(255) PRIMARY KEY, 
     user_email        CHARACTER VARYING(255) NOT NULL UNIQUE, 
     user_password     CHARACTER VARYING(255) NOT NULL, 
     user_first_name   CHARACTER VARYING(255) NOT NULL, 
     user_last_name    CHARACTER VARYING(255) NOT NULL, 
     security_question TEXT NOT NULL, 
     security_answer   TEXT NOT NULL 
  ); 
  
CREATE TABLE comment 
  ( 
     comment_id   UUID PRIMARY KEY, 
     user_id      CHARACTER VARYING(255) REFERENCES USER(user_id), 
     meal_id      UUID REFERENCES recipe(meal_id), 
     user_comment TEXT 
  ); 

CREATE TABLE inventory 
  ( 
     inventory_id     UUID PRIMARY KEY, 
     user_id          CHARACTER VARYING(255) REFERENCES USER(user_id), 
     user_ingredients TEXT 
  ); 

CREATE TABLE saved_recipe 
  ( 
     saved_recipe_id UUID PRIMARY KEY, 
     user_id         CHARACTER VARYING(255) REFERENCES USER(user_id), 
     meal_id         UUID REFERENCES recipe(meal_id) 
  ); 
```
