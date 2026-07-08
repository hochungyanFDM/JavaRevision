## 1. How do you check current directory?
pwd

## 2. How do you list files?
```
ls
```
// shows details
```
ls -l 
```
// shows hidden files
```
ls -a
```
// shows details + human-readable file size 
```
ls -lh 
```
## 3. How do you move/rename file?
```
mv hi.txt /tmp/
mv old.txt new.txt
```
## 4. How do delete a file?
```
rm hi.txt
rm -r folder
```
## 5. How do you check the last 100 lines of a log?
```
tail -n 100 live.log
```
## 6. How do you monitor a live log?
```
tail -f live.log
```
## 7. How do you copy a file?
```
cp source.txt backup.txt
cp -r folder1 folder2
```
## 8. How do you view a file?
```
cat file.txt
less file.txt
head file.txt
tail file.txt
```
// For large log, use:
```
less app.log
```

## 9. How do you search for an error in a log?
```
grep "ERROR" app.log
grep -i "error" app.log  
```

## 10. How do you search recursively inside folders?
```
grep -r "Connection refused" /app/logs/
```

## 11. How do you show lines before and after an error?
```
grep -A 5 -B 5 "ERROR" app.log
```
// -A means 5 Lines after
// -B means 5 Lines before

## 12. How do you find only today's logs?
```
grep "2026-07-08" app.log
ls -rlt
```

## 13. How do you search multiple keywords?
```
grep -E "ERROR|FAILED|Exception" app.log 
```

## 14. How do you search logs by process/order/trade ID?
```

```