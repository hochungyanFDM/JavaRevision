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