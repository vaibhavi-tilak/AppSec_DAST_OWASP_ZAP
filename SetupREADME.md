
### Installation Juice Shop

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


### Installation OWASP ZAP 

# Pull the Juice Shop Docker image
```
docker pull bkimminich/juice-shop
```
# Run Juice Shop in a container
```
docker run --rm -p 127.0.0.1:3000:3000 bkimminich/juice-shop
```

### Download FoxyProxy Chrome extension: https://chromewebstore.google.com/detail/foxyproxy/gcknhkkoolaabfmlnjonogaaifnjlfnp?hl=en




