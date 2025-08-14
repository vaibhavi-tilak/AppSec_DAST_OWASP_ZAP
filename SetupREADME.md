
- 1.	Install node.js
- 2.		Run git clone [https://github.com/juice-shop/juice-shop.git](https://github.com/juice-shop/juice-shop.git) --depth 1 (or clone your own fork of the repository)
-3.	Go into the cloned folder with cd juice-shop
-4.	Run npm install (only has to be done before first start or when you change the source code)
-5.	Run npm start
-6.	Browse to http://localhost:3000

Docker Container-

-1.	Install Docker
-2.	docker pull bkimminich/juice-shop
-3.	docker run --rm -p 127.0.0.1:3000:3000 bkimminich/juice-shop
-4.	Browse to http://localhost:3000 (on macOS and Windows browse to [http://192.168.99.100:3000](http://192.168.99.100:3000) if you are using docker-machine instead of the native docker installation)'


1. **OWASP Juice Shop**
   - A modern, JavaScript-heavy insecure web application built with Node.js, Express, and Angular.  
     It intentionally includes vulnerabilities from the **OWASP Top 10**.

### Installation

#### **From Source**
1. Install [Node.js](https://nodejs.org/)
2. Clone the repository (or your own fork):
```

git clone https://github.com/juice-shop/juice-shop.git --depth 1

```
3. Navigate into the cloned folder:
```

cd juice-shop

```
4. Install dependencies (only required before first start or after source code changes):
```

npm install

```
5. Start the application:
```

npm start

```
6. Open your browser and go to:
```

http://localhost:3000

```

#### **Using Docker**
1. Install [Docker](https://www.docker.com/)
2. Pull the Juice Shop Docker image:
```

docker pull bkimminich/juice-shop

```
3. Run the container:
```

docker run --rm -p 127.0.0.1:3000:3000 bkimminich/juice-shop

```
4. Open your browser and go to: http://localhost:3000  





