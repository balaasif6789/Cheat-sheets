
<b>kali@kali:~/Pentester Academy/Python for Pentesters$ for f in $(ls *.m4v); do nf=$(echo $f | awk -F: '{st=index($0,"_");print substr($0,st+1)}'| cut -d "." -f 1); ef=$(echo $f | awk -F: '{st=index($0,"_");print substr($0,0,2)}'); nf=$nf"_"$ef.m4v;echo $nf; mv $f $nf ;  done  </b>


IP files order: 
01_Module1_sometext.m4v
01_Module2.sometext.m4v
...
02_Module1.sometext.m4v

OP files order:
Module1.sometext_01.m4v
Module1.sometext_02.m4v
...
Module2.sometext_01.m4v


The 1st awk extracts the text Module1_sometext.m4v using the first occurrence of "_" as the delimiter. The output is then cut to remove the m4v using the "." delimiter. this is stored in variable $nf  

The 2nd awk extracts the preceding number from each of the files names.i.e. 01,02 and so on. This is stored in $ef/
The two variable are combined to create a new filename.


************************************************************************************************
only those lines which start with a . 
cat output.txt | grep "^\." | cut -d '.' -f 2- | cut -f 1 > bugcrowd_domains_final


only those lines which start with an alphbet 
cat output.txt |  grep "^\[a-z]" | cut -d '.' -f 2- | cut -f 1

while read LINE; do echo "$LINE" ;done | cut -d "*" -f 2 < bugcrowd_domain > output.txt

cat bugcrowd_domain | cut -d "*" -f 2 | cut -f 2

***********************************************************************************************

sed 's/ //g' bugcrowd_domain | sed 's/^\*//' | sed 's/^\.//' | cut -f 1
The firsr sed removes blank spaces
2nd sed removes the * when they occur at the beginning
3 sed removes . which occur in the beginning 
last cut command removes any unwanted things after the domain name 

sed -e 's/^\*//' <bugcrowd_domain | sed -e 's/^\.//' | cut -f 1
****************************************************************************************
Search all folders which contain the hosts.txt file but do not contain the urls.txt file. 
Useful to know for which domains we have run aquatone-discover but not run aquatone-scan

find -type d -exec test -e "{}/hosts.txt" ';' ! -exec test -e "{}/urls.txt" ';' -print | cut -d "/" -f 2
Searching for all sub folders in the aquatone folder which contain the hosts.txt file but do not contain the urls.txt file

****************************************************************************************************
Using a string as delimiter


awk -F 'delim' '{print $1; print $3}'

From the manual:

    -F fs
    –field-separator fs Use fs for the input field separator (the value of the FS predefined variable).
    
    
    
*********************************************************************************************************************
diff <(ls *.txt) <(ls *.*.txt)

will check difference of output returned between the 2 commands
1st ls will return all *.txt files  such as subdomains.txt
2nd ls will return all *.*.txt files such as facebook.com.txt


***********************************************************************************************************************

The following command enables me to start scanning from in between. 
Eg. Lets say I have already scanned the 1st 4 IP addresses and for some reason I had to stop the scan. 
I can then start scanning from the 5th IP without having to remove any IP Addresses that I have already scanned from the original 
file. 


for ips in  $(cat ips_list | tail -n+4); do bash testssl.sh $ips; done


**********************************************************************************************************************

ls *.txt |sed 's/\.txt//'


for domains in $(ls Sublist3r/*.*.txt |sed 's/\.txt//'| cut -d "/" -f2 ); python takeover.py -d $domains -w $domains.txt ; done



 for domains in $(ls ../Sublist3r/*.*.txt |sed 's/\.txt//'| cut -d "/" -f 3 ); do python takeover.py -d $domains -w ../Sublist3r/$domains.txt ; done  >>takeover


