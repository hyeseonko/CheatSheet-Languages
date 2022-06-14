## Command: awk

### inputfile1 - inputfile2: How to get the lines in one file (=inputfile1) that are not in another file (=inputfile2)?

```bash
    awk 'NR==FNR{a[$1];next}!($1 in a){print }' inputfile2 inputfile1 > outfile
```
- Example
   - assume that inputfile1 = {lineA, lineB} and inputfile2 = {lineB, lineC}
   - Then outfile would be like {lineA}.
- Reference: https://unix.stackexchange.com/questions/28158/is-there-a-tool-to-get-the-lines-in-one-file-that-are-not-in-another

### If I want to do SOMETHING about k-th column which is separted by tab
```
awk 'BEGIN {FS="\t"); {SOMETHING with $k}' inputfile
awk -F"\t" '{SOMETHING with $k}' inputfile
```
### IF, OR within awk-statement
```
awk -F"\t" '{if($4==1 || $4==2 || $4==3 || $4==4 || $4==5) {print $4, $7}}' inputfile > outputfile
```

#### Example. If I want to extract values where 2nd column > 0.9 separated by tab in an inputfile
```
awk 'BEGIN {FS="\t"}; {if($2>0.9) {print $0}}' inputfile > outfile
awk -F"\t" '{if($2>0.9) {print $0}}' inputfile > outfile
```

### Column swap
```
awk -F $'\t' ' { t = $1; $1 = $2; $2 = t; print; } ' OFS=$'\t' inputfile > outputfile
```

### Count the number of words in each line
```
awk '{print NF}' ${inputfile} 
```

### Sum the numbers in each line
```
awk '{n += $1}; END{print n}' ${inputfile}
```
- Example.
   ```
   # Inputfile
   1
   2
   3
   4
   
   # Output: 10
   ```

### Find intersection between two files
```bash
 awk 'NR==FNR { lines[$0]=1; next } $0 in lines' file1 file2 
```

### Calculate the average of lines of a file 
```
awk '{ total += $1; count++ } END { print total/count }' test.txt
```
