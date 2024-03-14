Library:openpyxl


## to load a workbook
wb= openpyxl.load_workbook(r"your/workbook/path")

## select sheet
sheet = wb['sheetname']

## max row
sheet.max_row 

## row value (same for column)
sheet['A' + str(row)].value
 or
sheet['B' + str(row)].value

//the 'A' and 'B' here, are the column numbering. 

