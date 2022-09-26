# How-to-delete-all-user-installed-package-in-R
When I update my R from 3.4 to 4.x, I find some packages are incompatible, I have to find them out and reinstall, but it is hard to find them. 

### Create a list of all installed packages
```
ip <- as.data.frame(installed.packages())
head(ip)
```

### If you use MRO, make sure that no packages in this library will be removed
```
ip <- subset(ip, !grepl("MRO", ip$LibPath))
```

### We don't want to remove base or recommended packages either
```
ip <- ip[!(ip[,"Priority"] %in% c("base", "recommended")),]
```
 
### Determine the library where the packages are installed
```
path.lib <- unique(ip$LibPath)
```

### Create a vector with all the names of the packages you want to remove
```
pkgs.to.remove <- ip[,1]
head(pkgs.to.remove)
```

### Remove the packages
```
sapply(pkgs.to.remove, remove.packages, lib = path.lib)
```

reference 
https://www.r-bloggers.com/2016/10/how-to-remove-all-user-installed-packages-in-r/
