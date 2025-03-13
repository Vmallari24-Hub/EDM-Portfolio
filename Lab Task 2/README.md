# Midterm Lab Task 2: Data Cleaning and Transformation Using Power Query Editor
## Step 1- Cleaning the data using PowerQuery Editor
- Download and open the raw data given by your instructor.

- Add the required columns (Min Sal, Max Sal, Role Type).

- Split the columns (Salary Estimate, Location, Size).

- Change the columns to appropriate data types (Currency, Text).

- Filter columns (Competitors, Revenue, Industry to remove negative values).

- Remove unnecessary columns to avoid redundancy (Company Name ratings, extra descriptions).

- Save the M Language to a notepad.

 ## Before Cleaning
 ![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/90f96d50eaf163fbda23f64931ab14ccc5c7b28a/Lab%20Task%202/Image/Capture.PNG)
 ![image](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/20103bccd0395daa5ead03ecb9b57f7210d3d236/Lab%20Task%202/Image/Capture1.PNG)
 ![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/a831389c6fd96e49a81666694031d6d38453867a/Lab%20Task%202/Image/Capture2.PNG)
 ## After Cleaning
 ![image alt ](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/378a76220ee3cba44e5034d3cacad77fd3c1419a/Lab%20Task%202/Image/Uncleaned%20Ds%20jobs.PNG)
 ![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/1773f8cf095af0da41c064c794c9ba3eae069e35/Lab%20Task%202/Image/Uncleaned%20Ds%20jobs2.PNG)

 ![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/475fcc933dc79fc29bf9c8c17324a019b2125b0d/Lab%20Task%202/Image/Uncleaned%20Ds%20jobs3.PNG)
 ## Step 2- Reshaping and Grouping the Tables
 - Duplicate and reference Unclean DS Jobs to create new queries (Sal By Role Type dup, Sal By Role Size ref, Sal By State ref).

- Select appropriate columns (Role Type, Size, Min Sal, Max Sal).

- Change the columns to required data types (Currency).

- Multiply Min Sal and Max Sal by 1000.

- Group data by Role Type, Size, State Full Name to get averages.

- Merge State Mapping with Unclean DS Jobs using State Abbreviation.

- Rename merged column to State Full Name and remove nulls.

- Check and review Query Dependencies.
 # Group Tables 
  ## Sal_By_Role_Type
 ![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/c5a46773e40949a913bb76847de59de546ded78b/Lab%20Task%202/Image/Role%20type%20Dup.PNG)
 ## Sal_By_Role_Size
![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/15e7a19e98ac350d573e89792dc2ea302f05fa1a/Lab%20Task%202/Image/Role%20size%20Dup.PNG)
 ## Sal_By_Size_Role_Type
 ![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/7f96ca1ee92d33c3eed4ffa84964eb3b90d2c0e1/Lab%20Task%202/Image/Size%20Role%20Type%20Dup.PNG)
 ## States
![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/78fdee3151363d98cbe38e6360ac31ec1b2c9a15/Lab%20Task%202/Image/State.PNG)
## Sal_By_State_ref
![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/f346437fe5d1bcdd03bfd2d1ddc8aa2a2656f3ef/Lab%20Task%202/Image/state%20ref.PNG)

## Step 3- Query Dependencies 
- Go to View Menu → Click Dependencies
Check if all queries are correctly linked
![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/a085003ee3fffdd566fafc35e2934c30daf98cde/Lab%20Task%202/Image/Capture.PNG)
