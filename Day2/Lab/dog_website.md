
# Create a docker container with a sample website about dogs. 

### To create a Docker container that hosts a simple website about dogs, you can follow these steps:

### Step 1: Create the Website Files

First, let's create a simple HTML website about dogs. You can create a directory for your project and add the necessary files.

```bash
mkdir dog-website
cd dog-website
```

Now, create an `index.html` file with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dogs Website</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
            padding: 50px;
        }
        h1 {
            color: #333;
        }
        p {
            color: #666;
        }
        img {
            max-width: 100%;
            height: auto;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Welcome to the Dogs Website!</h1>
    <p>Here you can find information about different breeds of dogs.</p>
    <img src="https://www.dogbreedslist.info/uploads/allimg/dog-pictures/German-Shepherd-Dog-1.jpg" alt="German Shepherd Dog">
</body>
</html>
```

### Step 2: Create a Dockerfile

Next, create a `Dockerfile` in the same directory (`dog-website`). This file will define how the Docker image should be built.

```Dockerfile
# Use the official Nginx image as the base image
FROM nginx:alpine

# Remove the default Nginx website
RUN rm -rf /usr/share/nginx/html/*

# Copy the website files to the Nginx HTML directory
COPY index.html /usr/share/nginx/html/

# Expose port 80 (HTTP)
EXPOSE 80

# Start Nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]
```

### Step 3: Build the Docker Image

Now that you have the `index.html` file and the `Dockerfile`, you can build the Docker image.

```bash
docker build -t dog-website .
```

This command will create a Docker image named `dog-website`.

### Step 4: Run the Docker Container

Once the image is built, you can run the container using the following command:

```bash
docker run -d -p 8080:80 dog-website
```

- `-d`: Runs the container in detached mode (in the background).
- `-p 8080:80`: Maps port 8080 on your local machine to port 80 in the container (which is the default HTTP port).

### Step 5: Access the Website

Now, open your web browser and go to `http://localhost:8080`. You should see the simple website about dogs.

### Optional: Push the Docker Image to Docker Hub

If you want to share your Docker image, you can push it to Docker Hub.

1. First, log in to Docker Hub:

   ```bash
   docker login
   ```

2. Tag your image with your Docker Hub username:

   ```bash
   docker tag dog-website your-dockerhub-username/dog-website
   ```

3. Push the image to Docker Hub:

   ```bash
   docker push your-dockerhub-username/dog-website
   ```

Now, anyone can pull and run your Docker image using:

```bash
docker run -d -p 8080:80 your-dockerhub-username/dog-website
```


### Directory structure for the `dog-website` project that we created in the previous steps:

```
dog-website/
├── Dockerfile
└── index.html
```

### Explanation of the Directory Structure:

1. **`dog-website/`**: This is the root directory of your project. It contains all the files necessary to build and run the Docker container.

2. **`Dockerfile`**: This file contains the instructions for building the Docker image. It specifies the base image (Nginx), copies the website files into the appropriate location, exposes port 80, and starts the Nginx server.

3. **`index.html`**: This is the main HTML file for your website. It contains the content that will be displayed when you visit the website. In this case, it's a simple webpage about dogs with some text and an image.

### Detailed Breakdown:

- **`Dockerfile`**:
  - **FROM nginx:alpine**: Specifies that the base image is `nginx:alpine`, which is a lightweight version of the Nginx web server.
  - **RUN rm -rf /usr/share/nginx/html/***: Removes the default Nginx welcome page.
  - **COPY index.html /usr/share/nginx/html/**: Copies the `index.html` file from your local machine to the Nginx HTML directory inside the container.
  - **EXPOSE 80**: Exposes port 80, which is the standard HTTP port.
  - **CMD ["nginx", "-g", "daemon off;"]**: Starts the Nginx server in the foreground when the container starts.

- **`index.html`**:
  - This is a simple HTML file that displays a webpage about dogs. It includes a title, a paragraph, and an image of a German Shepherd dog.

### To push your Docker image to Docker Hub, you need to follow these steps:

### Step 1: Create a Docker Hub Account

If you don't already have a Docker Hub account, you can create one by visiting [Docker Hub](https://hub.docker.com/) and signing up.

### Step 2: Log in to Docker Hub from the Command Line

Before pushing your image, you need to log in to Docker Hub using the `docker login` command.

```bash
docker login
```

You will be prompted to enter your Docker Hub username and password. Once you've entered the correct credentials, you should see a message like:

```
Login Succeeded
```

### Step 3: Tag Your Docker Image

Before pushing the image to Docker Hub, you need to tag it with your Docker Hub username. The format for tagging is:

```
docker tag <local-image-name> <dockerhub-username>/<repository-name>:<tag>
```

In our case, the local image name is `dog-website`. Let's tag it with your Docker Hub username and a repository name (e.g., `dog-website`). You can also add a version tag (e.g., `v1.0`), but if you omit the tag, it will default to `latest`.

```bash
docker tag dog-website your-dockerhub-username/dog-website:v1.0
```

Replace `your-dockerhub-username` with your actual Docker Hub username.

For example, if your Docker Hub username is `johndoe`, the command would look like this:

```bash
docker tag dog-website johndoe/dog-website:v1.0
```

You can verify that the image has been tagged correctly by running:

```bash
docker images
```

You should see something like this:

```
REPOSITORY               TAG       IMAGE ID       CREATED          SIZE
dog-website              latest    abc12345def6   10 minutes ago   22MB
johndoe/dog-website      v1.0      abc12345def6   10 minutes ago   22MB
```

### Step 4: Push the Docker Image to Docker Hub

Now that the image is tagged with your Docker Hub username, you can push it to Docker Hub using the `docker push` command.

```bash
docker push your-dockerhub-username/dog-website:v1.0
```

Again, replace `your-dockerhub-username` with your actual Docker Hub username.

For example:

```bash
docker push johndoe/dog-website:v1.0
```

The push process may take a few moments depending on the size of the image and your internet connection. Once the push is complete, you should see output similar to this:

```
The push refers to repository [docker.io/johndoe/dog-website]
v1.0: digest: sha256:abcdef1234567890abcdef1234567890abcdef1234567890abcdef1234567890 size: 1234
```

### Step 5: Verify the Image on Docker Hub

You can now verify that the image has been successfully pushed to Docker Hub by visiting your Docker Hub profile in a web browser.

1. Go to [Docker Hub](https://hub.docker.com/).
2. Log in with your credentials.
3. Navigate to your profile or repositories.
4. You should see the `dog-website` repository listed, along with the `v1.0` tag.

### Step 6: Pull and Run the Image from Docker Hub

Now that the image is on Docker Hub, anyone can pull and run it using the following commands:

```bash
docker pull your-dockerhub-username/dog-website:v1.0
docker run -d -p 8080:80 your-dockerhub-username/dog-website:v1.0
```

For example:

```bash
docker pull johndoe/dog-website:v1.0
docker run -d -p 8080:80 johndoe/dog-website:v1.0
```

After running the container, you can access the website by navigating to `http://localhost:8080` in your web browser.

### Optional: Update the Image

If you make changes to your website or Dockerfile, you can rebuild the image, retag it with a new version (e.g., `v2.0`), and push it again:

```bash
docker build -t dog-website .
docker tag dog-website your-dockerhub-username/dog-website:v2.0
docker push your-dockerhub-username/dog-website:v2.0
```

This way, you can maintain different versions of your image on Docker Hub.

### Conclusion

You've successfully pushed your Docker image to Docker Hub! Now, anyone can pull and run your `dog-website` container by using the `docker pull` and `docker run` commands.

Here's a quick recap of the commands:

1. **Log in to Docker Hub**:
   ```bash
   docker login
   ```

2. **Tag the image**:
   ```bash
   docker tag dog-website your-dockerhub-username/dog-website:v1.0
   ```

3. **Push the image**:
   ```bash
   docker push your-dockerhub-username/dog-website:v1.0
   ```

4. **Pull and run the image**:
   ```bash
   docker pull your-dockerhub-username/dog-website:v1.0
   docker run -d -p 8080:80 your-dockerhub-username/dog-website:v1.0
   ```

That's it! Your Docker image is now available on Docker Hub for others to use.
