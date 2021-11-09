## Handy Commands For Developers

## Chrome

#### Copy data to Clipboard
If you want to copy an object or variable to the clipboard from the console, then use the below copy command. The below line will copy AABB text to the system clipboard.

        copy("AABB");
#### Copy query param of page to Clipboard

        const urlSearchParams = new URLSearchParams(window.location.search);
        const params = Object.fromEntries(urlSearchParams.entries()); 
        copy(params['pageId']);
Run this command in chrome console, after opening the specific page, this will copy the value of pageId param to the system clipboard

## Couchbase

#### Scenario 1: Copy all documents from One Bucket to another

		INSERT INTO \`bucket-name\` (KEY _k, VALUE _v) SELECT META().id _k, _v from \`bucket-name\` _v

#### Scenario 2: Deleting everything from bucket

		DELETE FROM \`bucket-name\`

## Git


#### Scenario 1: Need to remove a Modified File from Git pull request

Switch to the branch from which you created the pull request:

     git checkout pull-request-branch

Overwrite the modified file(s) with the file in another branch, let's consider it's **master**:

    git checkout origin/master -- src/main/java/HelloWorld.java

Commit and push it to the remote:

    git commit -m "Removed a modified file from pull request"
    git push origin pull-request-branch

#### Scenario 2: Update the commit user name and email in the respective Git repo.

    git config user.name user-name
    git config user.email username-git@gmail.com

#### Scenario 3: Git updating the buffer size in Git repo, helps in case a large file is present in Git and you are trying to clone it in the local system.

    git config --global http.postBuffer 1048576000

#### Scenario 4: Stop tracking changes to a file in Sourcetree.

I guess This is the issue which troubled me most in git. Let's say, I have a file in my code base that I don't want to commit as this is specific to my local. But still, Sourcetree shows this file to me, every time I try to commit. This is really very annoying. to fix this run the below command in the repo folder and the Sourcetree will understand our feelings.

    git update-index --assume-unchanged file.filename

For folder use this

    git rm -r --cached path_to_your_folder/

To get undo/show dir's/files that are set to assume-unchanged run this:

    git update-index --no-assume-unchanged file.filename

To get a list of dir's/files that are assume-unchanged run this:

    git ls-files -v|grep '^h'
    
 To delete all local checked out branches
 	
	git branch -D `git branch`

## Maven

#### Scenario 1: Start the AEM in debug mode

    java -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=127.0.0.1:8765 -XX:+HeapDumpOnOutOfMemoryError -XX:MaxPermSize=256M -Xmx1024m -Dorg.apache.sling.commons.log.level=INFO -jar cq-quickstart-6.5.0.jar

#### Scenario 2: Build and deploy AEM

	mvn -PautoInstallPackage -Padobe-public clean install

#### Scenario 3: Start the Spring boot application

	mvn clean spring-boot:run

#### Scenario 4: Start Spring boot in specific mode

	mvn clean spring-boot:run -Dspring-boot.run.profiles=local

#### Scenario 5: Skip J-Unit test

	-Dmaven.test.skip=true

#### Scenario 6: Start Spring boot in debug mode and also run a specific profile and skip j unit test compilation

	mvn spring-boot:run -Dspring-boot.run.jvmArguments="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005" -Dspring-boot.run.profiles=local -Dmaven.test.skip=true


## Redis

#### Scenario 1: Start Redis Server

	redis-server

#### Scenario 2: Clear redis cache

	redis-cli flushall



#### To Be Continued....