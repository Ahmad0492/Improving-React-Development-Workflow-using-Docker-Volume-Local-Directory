# Improving-React-Development-Workflow-using-Docker-Volume-Local-Directory
Setting up Docker Volume Local Directory significantly improves developers’ workflow. We can see how it can be done in one easy step.

In this article, we’ll look at creating a local Docker directory volume for a Docker container. We will take the example of a React application running in our Docker container to illustrate the same.

Enabling Docker volumes has the benefit of enabling data sharing between the host and the Docker container.

When we update our code in a React application, for instance, the changes are typically automatically mirrored in the Docker container that is currently running the application. In essence, this enables developers to test their incremental updates on an active container.

## 1. Understanding the working of Docker Volume
We can map the file system inside the container to the file system of the host machine using Docker volumes. In essence, we can communicate files between our host and the active container by book marking volumes. Below illustration explains Docker volumes with the example of a React application

![docker-volumes-illustration](https://user-images.githubusercontent.com/106924407/219957290-3656323a-cd90-43eb-a8d6-f848f43e7ed0.png)

As you can see from the example above, we can force our Docker containers to use the files and directories on our host computer by bookmarking volumes.

For our React development work, this entails that we may update the running container as soon as we make changes. In other words, we don’t need to rebuild our Docker image every time we make a code change.

## 2. Running the Container

docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app ad98ac0c301e

```
docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app ad98ac0c301e
```

Let’s clarify the above written command:

* The port in the container is mapped to the port on the host using the -p flag.
* The volumes are then bookmarked using the -v command.
* Here, the /app/node_modules are initially mapped. In essence, we are instructing the container to use its own node_modules folder rather than the one on the host computer.
* Next, we use -v ($pwd):/app to map the rest of the pwd or present working directory with the container. In other words, we are instructing the container to look in the host machine’s current working directory, which is where our source code actually exists, for the contents of the app folder.
* The image id for the created image is the last item on the list.
* However, a point to be noted here is that the above command will not work on Windows or Mac. It will work on a Linux host machine.

## 3. Lets Test the code changes in REACT

We can test our configuration in this phase to determine if it functions as intended. If you run the aforementioned command, you ought to see the React application launch. The URL will be http://localhost:3000.
![docker-multi-stage-running-react-app](https://user-images.githubusercontent.com/106924407/219957591-254c11d9-add7-4224-9865-b064656fc0da.png)

To check our setup, we make a slight change in the React application as below. We change Learn React to You Should Learn React.

```
<a
  className="App-link"
  href="https://reactjs.org"
  target="_blank"
  rel="noopener noreferrer">
  You Should Learn React
</a>
```
An automatic compile will start as soon as we save the modifications, just like it does when you run a React application locally. The website will update with the modifications.
![react-application-dev-server](https://user-images.githubusercontent.com/106924407/219957598-2fbda5e5-16fb-4d22-903a-59b3dd18d911.png)

The primary distinction is that the refresh is taking place inside the Docker container this time. The image didn’t require rebuilding.

## Conclusion

With this, we have successfully illustrated how to use local directory mapping for Docker volumes. To automatically update a running container with code changes made to a React application, we leveraged the functionality of bookmarking volumes.

Developers now have an easier time of things since they can test their modifications directly on a Docker container rather than on a local PC. Moreover, this configuration does not require several builds of the Docker image.

Please share your thoughts in the comments box below if you have any questions or remarks.
