# holbertonschool-softy-pinko-docker

- **[0. Create Your First Docker Image](./task0/Dockerfile)**

- Is based on the latest ubuntu
- Update APT using apt-get update
- Upgrade currently installed software through APT using apt-get upgrade -y
- Once built, you can run the Docker image in a container and it will echo “Hello, World!” on the terminal.

- **[1. Back-end](./task1)**

- Copy your task0 directory and name it task1
- Change the Dockerfile to install Python3, pip3, and Flask
- Install python3, python3-pip, and flask with the -y flag
- flask must be installed with pip3, not through apt-get
- Locally, create a Python file named `api.py` that uses Flask to create an endpoint `/api/hello` returning "Hello, World!"
- Host this Flask app on `0.0.0.0` and port `5252`
- In your Dockerfile, use `/app` as the working directory and copy the Python file to your Docker image
- Forward the Docker container’s port 5252 to the host machine’s port 5252 when running your image

- **[2. Front-end](./task2)**

- Copy your task1 directory and name it task2
- Create a new directory named `back-end` inside task2 and move `api.py` and `Dockerfile` inside
- Create a new `task2/front-end` directory
- Inside `task2/front-end`, clone the `softy-pinko-front-end` repository
- In the new `task2/front-end/Dockerfile`, use the latest version of `nginx`
- Copy `softy-pinko-front-end` files to `/var/www/html/softy-pinko-front-end` on the Docker image
- Create an Nginx config file named `softy-pinko-front-end.conf` configuring the port, server name, location, and index, and copy it to `/etc/nginx/conf.d/default.conf`

- **[3. Connecting the Front-end and Back-end](./task3)**

- Copy your task2 directory and name it task3
- In `index.html`, add `<h1 id="dynamic-content"></h1>` to insert dynamic data
- Add JavaScript at the bottom of the HTML to make an AJAX GET request to `http://localhost:5252/api/hello`
- In the back-end's Dockerfile, install `flask-cors` using pip3
- Update `api.py` to use `CORS(app)` to accept cross-origin requests from the front-end

- **[4. Making it Simpler with Docker Compose](./task4)**

- Copy your task3 directory and name it task4
- Inside the task4 directory, create a `docker-compose.yml` file
- Configure the front-end and back-end services using keywords: `services`, `build`, `context`, `dockerfile`, `image`, `ports`, `depends_on`
- Build the services using `docker-compose build` and run them with `docker-compose up`

- **[5. Proxy Server](./task5)**

- Copy your task4 directory and name it task5
- Create a new folder named `proxy`
- Create a Dockerfile that uses the latest version of `nginx`
- Create a file named `proxy.conf` listening on port 80 and routing `/` to the front-end service and `/api` to the back-end service
- Update the JavaScript in `index.html` to make the API call through the proxy server (`url: "/api/hello"`)
- Update the `docker-compose.yml` to add the `proxy` service, map port 80 to the host, and remove external port mappings for the front-end and back-end services

- **[6. Scale Horizontally](./task6)**

- Copy your task5 directory and name it task6
- Create a new file named `2-api-servers.txt` with the exact docker-compose command used to spin up two API servers
- The Nginx proxy will act as a load-balancer between the back-end API servers using the Round-Robin algorithm
