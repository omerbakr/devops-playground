FROM node:20-alpine

# A group is a collection of user accounts. 
# Instead of giving 100 people individual permission to access a folder, an admin puts them all into one "group" and assigns the permission to that group. 
# It’s all about efficiency and keeping things organized.

# Create a user with permissions to run the app.
# addgroup -> Create a new group.
# app -> The name of the group.
# adduser -> Create a new user.
# -S -> Sets the user as a system user. This prevents manual logins.
# -G -> Add this user to the following group.
# app (First instance) -> The target group name (referencing the "app" group created previously).
# app (Second instance) -> The actual username of the account being created.
RUN addgroup app && adduser -S -G app app

#? Why do we need to create a user?
# In Docker, everything runs as the root user by default. 
# If we don't create a specific user, the application will execute with root privileges.
# This poses a significant security risk. If the container is compromised, the attacker will gain root access to your system.

# Switch from the default root user to the app user you created in the previous step.
USER app

#! Pro Tip: Since you just switched to the "app" user in the previous step, Docker ensures that this directory is handled with the permissions of that user, keeping your environment tidy and secure.

WORKDIR /app

# If you haven't changed your package.json file, Docker will skip this step and the following npm install step during the next build.
# It will simply use the "cached" version from the last build.
# This saves you from waiting minutes for dependencies to download every time you change a single line of source code.
COPY package*.json ./

# This is a tactical switch. Even though we want the app to run as a limited user, sometimes the system needs "Admin privileges" to fix file permissions before the app starts.
USER root

#? Why switch here?
# You are switching to root specifically so you can run the next command (chown), which requires administrative power.
# You can't change who owns a folder unless you have the authority to do so!

# chown: Short for "change owner".
# -R: Stands for Recursive. It tells Docker: "Don't just change the folder; change every single file and subfolder inside it too."
# chown -R <user>:<group> <directory>
# Change the ownership of the /app directory to the app user.
RUN chown -R app:app .

#? Why we back and forth between root and app users:
# The Problem: When we use the COPY command to move files in, Docker automatically marks them as belonging to the "Superuser" (root). Even though we switched to the app user.
# The Obstacle: However, for security reasons, we want to operate as a "Standard User" (app). A standard user cannot touch the Superuser's files or install anything new (like node_modules) into those directories.
# The Solution (The previous step): Out of necessity, we temporarily became root again, commanded that "these files now belong to the app user" (chown), and finished the task.

# Now that the job is done, we are leaving the "Superuser" privileges behind and returning to our seat as the app user.
USER app

RUN npm install

# Copy the rest of the files to the working directory.
COPY . .

# Expose port 5173 to tell Docker that the container listens on the specified network ports at runtime.
EXPOSE 5173

CMD npm run dev