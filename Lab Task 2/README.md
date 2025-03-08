let
    Source = Csv.Document(File.Contents("C:\Users\COMLAB\Downloads\Uncleaned_DS_jobs.csv"),[Delimiter=",", Columns=15, Encoding=1252, QuoteStyle=QuoteStyle.Csv]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"index", Int64.Type}, {"Job Title", type text}, {"Salary Estimate", type text}, {"Job Description", type text}, {"Rating", type number}, {"Company Name", type text}, {"Location", type text}, {"Headquarters", type text}, {"Size", type text}, {"Founded", Int64.Type}, {"Type of ownership", type text}, {"Industry", type text}, {"Sector", type text}, {"Revenue", type text}, {"Competitors", type text}}),
    #"Split Column by Delimiter" = Table.SplitColumn(#"Changed Type", "Salary Estimate", Splitter.SplitTextByDelimiter("(", QuoteStyle.Csv), {"Salary Estimate.1", "Salary Estimate.2"}),
    #"Changed Type1" = Table.TransformColumnTypes(#"Split Column by Delimiter",{{"Salary Estimate.1", type text}, {"Salary Estimate.2", type text}}),
    #"Inserted Literal" = Table.AddColumn(#"Changed Type1", "Literal", each "101", type text),
    #"Renamed Columns" = Table.RenameColumns(#"Inserted Literal",{{"Literal", "Min Sal"}}),
    #"Duplicated Column" = Table.AddColumn(#"Renamed Columns", "Min Sal - Copy", each [Min Sal], type text),
    #"Renamed Columns1" = Table.RenameColumns(#"Duplicated Column",{{"Min Sal - Copy", "Max Salary"}}),
    #"Added Custom" = Table.AddColumn(#"Renamed Columns1", "Role Type", each if Text.Contains([Job Title], "Data Scientist") then
"Data Scientist"
else if Text.Contains([Job Title], "Data Analyst") then
"Data Analyst"
else if Text.Contains([Job Title], "Data Engineer") then
"Data Engineer"

else if Text.Contains([Job Title], "Machine Learning") then
"Machine Learning Engineer"
else
"other"),
    #"Changed Type2" = Table.TransformColumnTypes(#"Added Custom",{{"Role Type", type text}}),
    #"Added Custom1" = Table.AddColumn(#"Changed Type2", "Custom", each if [Location]= "New Jersey" then ", NJ"
else if [Location] = "Remote" then ", other"
else if [Location]= "United States" then ", other"
else if [Location]= "Texas" then ", TX"
else if [Location]= "Patuxent" then ", MA"
else if [Location]= "California" then ", CA"
else if [Location]= "Utah" then ", UT"
else [Location]),
    #"Removed Columns" = Table.RemoveColumns(#"Added Custom1",{"Custom"}),
    #"Added Custom2" = Table.AddColumn(#"Removed Columns", "Location Correction", each if [Location]= "New Jersey" then ", NJ"
else if [Location] = "Remote" then ", other"
else if [Location]= "United States" then ", other"
else if [Location]= "Texas" then ", TX"
else if [Location]= "Patuxent" then ", MA"
else if [Location]= "California" then ", CA"
else if [Location]= "Utah" then ", UT"
else [Location]),
    #"Removed Columns1" = Table.RemoveColumns(#"Added Custom2",{"Location Correction"}),
    #"Added Custom3" = Table.AddColumn(#"Removed Columns1", "Custom", each if [Location]= "New Jersey" then ", NJ"
else if [Location] = "Remote" then ", other"
else if [Location]= "United States" then ", other"
else if [Location]= "Texas" then ", TX"
else if [Location]= "Patuxent" then ", MA"
else if [Location]= "California" then ", CA"
else if [Location]= "Utah" then ", UT"
else [Location]),
    #"Renamed Columns2" = Table.RenameColumns(#"Added Custom3",{{"Custom", "Location Correction"}}),
    #"Split Column by Delimiter1" = Table.SplitColumn(#"Renamed Columns2", "Location Correction", Splitter.SplitTextByDelimiter(",", QuoteStyle.Csv), {"Location Correction.1", "Location Correction.2"}),
    #"Changed Type3" = Table.TransformColumnTypes(#"Split Column by Delimiter1",{{"Location Correction.1", type text}, {"Location Correction.2", type text}}),
    #"Replaced Value" = Table.ReplaceValue(#"Changed Type3","Anne Rundell","MA",Replacer.ReplaceText,{"Location Correction.2"}),
    #"Renamed Columns3" = Table.RenameColumns(#"Replaced Value",{{"Location Correction.2", "State Abbreviation"}}),
    #"Duplicated Column1" = Table.DuplicateColumn(#"Renamed Columns3", "Size", "Size - Copy"),
    #"Split Column by Delimiter2" = Table.SplitColumn(#"Duplicated Column1", "Size - Copy", Splitter.SplitTextByDelimiter("to", QuoteStyle.Csv), {"Size - Copy.1", "Size - Copy.2"}),
    #"Changed Type4" = Table.TransformColumnTypes(#"Split Column by Delimiter2",{{"Size - Copy.1", type text}, {"Size - Copy.2", type text}}),
    #"Renamed Columns4" = Table.RenameColumns(#"Changed Type4",{{"Size - Copy.1", "MinCompanySize"}, {"Size - Copy.2", "MaxCompanysize"}}),
    #"Removed Columns2" = Table.RemoveColumns(#"Renamed Columns4",{"Min Sal", "Max Salary"}),
    #"Duplicated Column2" = Table.DuplicateColumn(#"Removed Columns2", "Salary Estimate.1", "Salary Estimate.1 - Copy"),
    #"Split Column by Delimiter3" = Table.SplitColumn(#"Duplicated Column2", "Salary Estimate.1 - Copy", Splitter.SplitTextByDelimiter("-", QuoteStyle.Csv), {"Salary Estimate.1 - Copy.1", "Salary Estimate.1 - Copy.2"}),
    #"Changed Type5" = Table.TransformColumnTypes(#"Split Column by Delimiter3",{{"Salary Estimate.1 - Copy.1", type text}, {"Salary Estimate.1 - Copy.2", type text}}),
    #"Renamed Columns5" = Table.RenameColumns(#"Changed Type5",{{"Salary Estimate.1 - Copy.1", "MinSalary"}, {"Salary Estimate.1 - Copy.2", "MaxSalary"}}),
    #"Reordered Columns" = Table.ReorderColumns(#"Renamed Columns5",{"index", "Job Title", "Salary Estimate.1", "Salary Estimate.2", "Job Description", "Rating", "Company Name", "Location", "Headquarters", "Size", "Founded", "Type of ownership", "Industry", "Sector", "Revenue", "Competitors", "MinSalary", "MaxSalary", "Role Type", "Location Correction.1", "State Abbreviation", "MinCompanySize", "MaxCompanysize"}),
    #"Filtered Rows" = Table.SelectRows(#"Reordered Columns", each ([Industry] <> "-1") and ([Competitors] <> "-1")),
    #"Split Column by Delimiter4" = Table.SplitColumn(#"Filtered Rows", "Company Name", Splitter.SplitTextByDelimiter("#(lf)", QuoteStyle.Csv), {"Company Name.1", "Company Name.2"}),
    #"Changed Type6" = Table.TransformColumnTypes(#"Split Column by Delimiter4",{{"Company Name.1", type text}, {"Company Name.2", type number}}),
    #"Removed Columns3" = Table.RemoveColumns(#"Changed Type6",{"Company Name.2", "Salary Estimate.1"}),
    #"Reordered Columns1" = Table.ReorderColumns(#"Removed Columns3",{"index", "Job Title", "MinSalary", "MaxSalary", "Salary Estimate.2", "Job Description", "Rating", "Company Name.1", "Location", "Headquarters", "Size", "Founded", "Type of ownership", "Industry", "Sector", "Revenue", "Competitors", "Role Type", "Location Correction.1", "State Abbreviation", "MinCompanySize", "MaxCompanysize"}),
    #"Removed Columns4" = Table.RemoveColumns(#"Reordered Columns1",{"Salary Estimate.2"}),
    #"Reordered Columns2" = Table.ReorderColumns(#"Removed Columns4",{"index", "Job Title", "MinSalary", "MaxSalary", "Job Description", "Company Name.1", "Rating", "Location Correction.1", "Location", "Headquarters", "Size", "Founded", "Type of ownership", "Industry", "Sector", "Revenue", "Competitors", "Role Type", "State Abbreviation", "MinCompanySize", "MaxCompanysize"}),
    #"Removed Columns5" = Table.RemoveColumns(#"Reordered Columns2",{"Location"}),
    #"Renamed Columns6" = Table.RenameColumns(#"Removed Columns5",{{"Location Correction.1", "Location"}}),
    #"Reordered Columns3" = Table.ReorderColumns(#"Renamed Columns6",{"index", "Job Title", "MinSalary", "MaxSalary", "Job Description", "Company Name.1", "Rating", "Location", "State Abbreviation", "Headquarters", "Size", "MinCompanySize", "MaxCompanysize", "Founded", "Type of ownership", "Industry", "Sector", "Revenue", "Competitors", "Role Type"})
in
    #"Reordered Columns3"
