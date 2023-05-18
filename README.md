# Deploying a React Application with Nginx

## Introduction

Deploying a React web application with Nginx as a reverse proxy server is a reliable and efficient approach. In this guide, we will explore how Nginx can enhance the deployment of your React application. We'll cover the installation of Nginx, configuring the server, and deploying your React app. Let's dive in!

## Understanding Nginx

Nginx is a powerful open-source web server software known for its high performance, scalability, and robust features. It serves as a reverse proxy server, handling client requests and forwarding them to the appropriate backend server. Nginx is particularly well-suited for serving static files and improving the performance of your React application.

## Setting up Nginx

Before deploying your React application, you need to install and configure Nginx on your server. Here are the steps:

**Provision an environment:** Set up an environment where you will deploy your React app. This can be an AWS EC2 instance, a virtual machine, or any other hosting provider that allows you to install software.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684404684915/412b5e30-0102-4b10-8b9e-64e356d9598e.png)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684404699762/ffc5f3a7-7149-46c8-934e-9743251aa532.png)

**Install Nginx:** Use the package manager of your server's operating system to install Nginx. For example, on Ubuntu, you can run:

```bash
sudo apt update
sudo apt install nginx
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684404898134/d3f7bee1-e2de-4608-8837-33152f824003.png)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684404913014/93fe4915-5989-4a34-ac3c-92d1dc58a215.png)

**Verify Nginx installation:** After installation, ensure that Nginx is running by accessing your server's IP address in a web browser. If Nginx is installed correctly, you should see the default Nginx welcome page.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684405023068/84c98b38-3bc8-4ec4-a007-d4a070e7c71d.png)

You can also check nginx by using the below command:

```bash
sudo systemctl status nginx
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684405164996/d6cb7449-b764-4ac2-8ae4-0802a7024083.png)

## Configuring Nginx for React Application

If you are cloning a React project from GitHub, you can follow these steps to deploy it with Nginx:

**Step 1:** Clone the React project

Clone the React project repository from GitHub onto your server using the `git clone` command. Open your terminal and navigate to the directory where you want to clone the project. Then run:

```bash
git clone <repository_url>
```

Replace `<repository_url>` with the URL of the GitHub repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684405612835/84d2d60b-d065-4062-92bf-0718e117d3b2.png)

**Step 2:** Install dependencies and build the project Navigate into the cloned project directory:

```bash
cd <project_directory>
```

Install the project dependencies using `npm` or `yarn`:

```bash
npm install
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684405931568/8bf470ab-5aab-47e1-8840-68ab768c139a.png)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684406219762/c2060ad3-d72c-4f2a-8223-281fd7730b51.png)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684406380437/f28aa42a-3ddb-459b-bce4-14890e0a9d24.png)

Once the dependencies are installed, build the project by running:

```bash
npm run build
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684406456021/954f2bf9-61a9-4dfe-98ba-39b9d276e7e5.png)

This will generate an optimized production build in the `build` folder.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684406489763/994335a9-280f-48f6-8585-daa3bb8ef7b8.png)

The below practice is the best approach according to nginx documentation:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684408074789/d798b413-9bba-44f4-b90b-caaf0928c041.png)

Open the nginx.conf and do comment like below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684408484822/61088ea7-3a78-4f0b-aee3-38d49033a840.png)

Create a new server configuration file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684408661176/6698bfb9-3624-4fa9-b75a-888d764fecf9.png)

Add the following configuration to the `react-portfolio.conf` file:

```bash
server {
    listen 80;
    server_name 65.2.29.39;

    root /home/ubuntu/react-portfolio/build;
    index index.html;

    location / {
        try_files $uri /index.html;
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684412142203/4c5db06d-87a6-416b-978c-1c1402f0efe8.png)

Replace `your_domain.com` with your actual domain name or server IP, and `/home/ubuntu/react-portfolio/build` with the absolute path to your React app's build folder.

Save the configuration file and exit the text editor.

Test the Nginx configuration to ensure there are no syntax errors:

```bash
sudo nginx -t
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684409063410/20226e44-801a-4831-9702-78d2e4e43c65.png)

Finally, restart Nginx to apply the changes:

```bash
sudo service nginx restart
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684409119853/7c261527-43ee-4e4e-87a2-986441b06124.png)

**Verify the deployment:**

Visit your domain name or server IP in a web browser, and you should see your React web application successfully deployed using Nginx.

Now you can access your React app by visiting your server's IP address in a web browser. For example, if your server's IP address is `65.2.29.39`, you can access your app by entering [http://65.2.29.39/](http://65.2.29.39/) in the browser's address bar.

If got permission denied error then you can refer this 👉 [https://stackoverflow.com/questions/25774999/nginx-stat-failed-13-permission-denied](https://stackoverflow.com/questions/25774999/nginx-stat-failed-13-permission-denied)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684411926645/c45e47a4-c1b1-4811-b28a-1fa0753211bc.png)

Note: Without a domain name, your app will only be accessible via the IP address, so you may consider obtaining a domain name if you want a more user-friendly URL.

That's it! You have successfully deployed your cloned React project with Nginx. Enjoy using Nginx to serve your React application efficiently.

## Conclusion

Deploying a React application with Nginx offers improved performance and scalability. Nginx's reverse proxy capabilities and efficient handling of static files make it an excellent choice for serving React applications. By following the steps outlined in this guide, you can successfully deploy your React app using Nginx. Enjoy the benefits of a fast and reliable web server for your React application!

If you have any questions or need further assistance, feel free to leave a comment below. Happy coding!

Nginx documentation: [https://nginx.org/en/docs/?\_ga=2.148869746.453070200.1684412743-1722295106.1683266947](https://nginx.org/en/docs/?_ga=2.148869746.453070200.1684412743-1722295106.1683266947)

And don't forget to connect with us on social media to stay updated with the latest tips, tutorials, and guides:

- Connect with us on LinkedIn: [**Shaik Ahmad Nawaz**](https://www.linkedin.com/in/shaik-ahmad-nawaz-894425239/)
- Follow us on Twitter: [**@shaikahmadnawaz**](https://twitter.com/shaikahmadnawaz)

We also encourage you to check out our GitHub repository for more code samples and projects:

- Explore our GitHub: [**shaikahmadnawaz**](https://github.com/shaikahmadnawaz)
