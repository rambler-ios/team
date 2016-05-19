### Настройка CI на Jenkins с build.sh

1. Добавьте пустой файл *build.sh* в корневую папку проекта.
2. Настройте переменные `workspace`, `scheme`, `sourceDir=`.
3. Выполните команду в консоли в папке проекта: `chmod +x build.sh`.
4. Зайдите в настройки проекта на Jenkins.
5. Добавьте build step *Execute shell* с командой `./build.sh`.
6. Добавьте *Post-build Actions*: *Publish JUnit test result report*.
  1. Test report XMLs 

```sh
#!/bin/bash -l
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
export LC_CTYPE=en_US.UTF-8
 
#Configuration
workspace=LiveJournal
scheme=LiveJournal
sourceDir=LiveJournal
reportsDir=build/reports
 
#Fail immediately if a task fails
set -e
set -o pipefail
 
#Clean
rm -fr ~/Library/Developer/Xcode/DerivedData
rm -fr ./build
#Compile, run tests
iosVersion='9.1'
xcodebuild test -workspace ${workspace}.xcworkspace -scheme ${scheme} -configuration Debug \
-destination "platform=iOS Simulator,name=iPhone 5s,OS=${iosVersion}" ONLY_ACTIVE_ARCH=YES | xcpretty -c --report junit
```