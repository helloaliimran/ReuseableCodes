# Export to excel

> CSV file mean comma seperated values. but you can also use other seprater as well. [, "" ; :]

```
public FileResult ExportCSV(long Id)
        {
            var model = new SomeModel();
            model.Init(Id); 
            //initialize model
            StringWriter sw = new StringWriter();
            //column headers.
            sw.WriteLine("Id,Name,Value,Date");
            //optional.
            var result = model.OrderBy(x => x.Name).ToList(); 
            // read line by line and seperated with semi-colon ; or comma ,
            foreach (var item in result)
            {
                sw.WriteLine(string.Format("{0},{1},{2},{3}", item.Id, item.Name, item.Value,item.Date)) ;
            }
            //download file in the broswser.
            return File(new UTF8Encoding().GetBytes(sw.ToString()), "text/csv", "export.csv");
        }
```
#### limitation
  - how to merge two cell in csv file.
  
  This is not possible
  - A comma-separated values (CSV) file stores tabular data (numbers and text) in plain text.
  - It is just data, with no attached formatting or knowledge of how the cells should be merged when the data is imported.
