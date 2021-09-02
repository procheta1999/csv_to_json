# csv-to-json-converter
A shell script that converts a csv file to a json file

__Tested in Windows__   
-----

# INSTRUCTIONS: 
1. Firstly, git bash into your folder where you have kept the .sh files.  
2. copy the csv file (input.csv) into the folder (csv-to-json-converter) with csvtojson.sh file
3. execute first "chmod a+x csvtojson.sh" to make csvtojson.sh executable 
4. execute the csvtojson.sh file in the Git Bash terminal with "bash ./csvtojson.sh input.csv > output.json"  

****

# Basic documentation of the work:
1. First I downloaded the dataset from [International Greenhouse Gas Emissions](https://www.kaggle.com/unitednations/international-greenhouse-gas-emissions) .
2. Next, for converting to JSON file:
- csvtojson.sh : It reads the csv files line by line and takes the table headers as the keys of the objects in the json array 'data' and the data of the table as the value of each set of keys.
<br>
Example: Suppose in line 2 of the csv file (since line 1 of the csv file contains the table headers) there are: 
<br>
Australia,
<br>2014,
<br>393126.946994288,<br>carbon_dioxide_co2_emissions_without_land_use_land_use_change_and_forestry_lulucf_in_kilotonne_co2_equivalent
<br>
<br>
So while converting to json, it will appear almost like this : 
<br>
{
    <br>
"data":
<br>
[
    <br>
{
    <br>
    "country_or_area":"Australia",
<br>"year":"2014",
<br>"value":"393126.946994288",<br>"category":"carbon_dioxide_co2_emissions_without_land_use_land_use_change_and_forestry_lulucf_in_kilotonne_co2_equivalent"
<br>},
<br>
...............
<br>
}
<br>]

## Explanantion of the code:
<code>input=$1</code>
<br>Takes input parameter<br>
<code>[ -z $1 ]</code><br>
Checks if input[1] is empty or not<br>
<code>[ ! -e $input ]</code><br>
Checks for existence of filename(input)<br>
<code>read first_line < $input</code><br>
Reads first line of input file and stores it in first_line<br>
<code>attributes=`echo $first_line | awk -F, {'print NF'}`</code><br>
echo $first_line | awk -F, {'print NF'} with tail tags acts as a Bash command where:

1. awk for pattern scanning and processing
2. awk -F fs: where fs is the input seperator
3. NF is the count of input fields.
<br>

So basically, this command returns the number of fields in the input file.
