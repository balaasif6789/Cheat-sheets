# bash-one-liners
Tried and tested

cat output.txt | grep "^\." | cut -d '.' -f 2- | cut -f 1 > bugcrowd_domains_final

cat output.txt |  grep "^\[a-z]" | cut -d '.' -f 2- | cut -f 1

while read LINE; do echo "$LINE" ;done | cut -d "*" -f 2 < bugcrowd_domain > output.txt

cat bugcrowd_domain | cut -d "*" -f 2 | cut -f 2


sed 's/ //g' bugcrowd_domain | sed 's/^\*//' | sed 's/^\.//' | cut -f 1

The firsr sed removes blank spaces
2nd sed removes the * when they occur at the beginning
3 sed removes . which occur in the beginning 
last cut command removes any unwanted things after the domain name 

sed -e 's/^\*//' <bugcrowd_domain | sed -e 's/^\.//' | cut -f 1


find -type d -exec test -e "{}/hosts.txt" ';' ! -exec test -e "{}/urls.txt" ';' -print | cut -d "/" -f 2
Searching for all sub folders in the aquatone folder which contain the hosts.txt file but do not contain the urls.txt file
