# Dockerfile is a text file that contains instructions for building a Docker image.
# Think of it like a recipe. "Use this base operating system, install these dependencies, and copy over these files."

# A Docker image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries, and settings.
# Like a raw dough of a cake. It has all the ingredients but it is not an edible cake yet.

# A Docker container is a running instance of a Docker image.
# Like a baked cake. It is ready to be eaten.

# Step 1: Selection of operating system and runtime environment
FROM node:20-alpine
# Comes with Node v20 pre-installed.
# Uses Alpine, the lightest and most secure Linux distribution, as OS.

# Step 2: Setting the working directory inside the container
WORKDIR /app
# All subsequent commands (COPY, CMD) will be executed from this directory. 
# If the directory does not exist, it will be created.

# Step 3: Copying the application code into the container
COPY . .
# Take all files from the current directory (in this case hello-docker folder)
# and copy them to the /app directory inside the container.

# Step 4: Defining the command to run when the container starts
CMD node hello.js
# This is the default command that will be executed when the container starts.
# Runs the hello.js file using Node.js.