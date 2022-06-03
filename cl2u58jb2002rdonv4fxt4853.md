## Google Serverless Infrastructure: A Primer on GCP & Serverless Computing

#### DevOps

#### Learn about GCP & it’s serverless computing infrastructure. Learn when to use App Engine, Cloud Functions or Cloud Run on Google Cloud Platform.

Who needs Digital Ocean when you got Google Serverless services?

Have you ever built a Machine Learning application? And did you wonder to yourself how to showcase it on the Internet, then you’re not alone. Fortunately, there’s a pretty good solution to this dilemma. And the solution is “ *Serverless Computing* “! And guess what? Google Cloud Platform (GCP) & Serverless Computing are a match made in heaven.

With GCP, you don’t just get one serverless service but three great services. And each catering to a very niche need based on the type of your projects. But choosing the right service can be confusing which is why I wrote this article. It should guide you through while deciding what suits your project’s needs.

### What is Serverless Computing

There’s a lot of buzz about “ *Serverless architecture*”, “ *Serverless this-and-that* “. Filtering out the buzz & understanding the core concepts of Serverless Computing is important. It’ll help you maintain & manage your project(s) better.

So, let’s understand what Serverless Computing is all about. Here’s a brief description of the concept from Wikipedia;

> *Serverless computing is a cloud computing execution model in which the cloud provider allocates machine resources on demand, taking care of the servers on behalf of their customers. \[&mldr;\] When an app is not in use, there are no computing resources allocated to the app. Pricing is based on the actual amount of resources consumed by an application. \[&mldr;\] “Serverless” is a misnomer in the sense that servers are still used by cloud service providers to execute code for developers. However developers of serverless applications are not concerned with capacity planning, configuration, management, maintenance, operating or scaling of containers, VMs, or physical servers.*

Reiterating on the quote from Wikipedia, let me sum up the information for you:

1.  The cloud service providers offer a range of serverless services wherein they manage all required resources for a project dynamically. The major players on this field are Google Cloud Platform (GCP), Amazon Web Services (AWS) & Microsoft Azure.
2.  Pricing is based on the specific amount of resources used by the project. Hence, quite often it’s cheaper to use Serverless Computing over renting out an actual server.
3.  Developers needn’t worry about the state of the servers. They can focus on improving their products & leave the responsibility of maintaining the servers to the Cloud Service Providers.

So, now you should’ve a better understanding of what serverless computing is. With this knowledge let’s dive deeper into what Google has to offer. More specifically we’ll look into their Serverless Computing services.

### Google’s Serverless Computing Solutions

Google Cloud Platform (GCP) provides three serverless computing services; namely:

While each of these services might look pretty much the same on face value, they’re not. Their specific use cases differs. The programming language to use with them varies as well & much more.

So, let’s check out how, when & why you might want to use any of these services.

Google defines Cloud Run as “a fully managed service for deploying containerized applications”. To be more specific, Cloud Run provides an API through [Knative](https://knative.dev/). The developer then can use the API to interact with the containerized instances.

Under the hood, Knative is just an open-source wrapper around Kubernetes. It enables developers to host serverless infrastructure for themselves.

Do note, Cloud Run utilizes containers-based technology. Hence, you can use any programming language of your choice or even a binary! The only thing stopping you would be if the image to build the container isn’t available for download.

You can find more information on Cloud Run at: [cloud.google.com/run](https://cloud.google.com/run).

App Engine is pretty much like renting out a server for yourself. The caveat being, Google manages the server for you. And it comes with every set of tools you would ever need.

So, you have the freedom of choosing either one of the most popular programming languages. Or you could use something else of your choice.

For example, you could build the backend of your application in Python. And let App Engine take care of scaling it and/or integrating it with other services as well. And if you could choose some other language too as per your preferences!

You should deliver your code using Docker containers & App Engine will take care of the rest. Besides that, App Engine will also version your application. But if you desire you could split incoming traffic, perform health checks & so on.

So, as you can see App Engine is perfect for production applications which need a lot of resources. And if you prefer not to mange the backend maintenance at all, App Engine is perfect for your use case.

That said, you can find comprehensive details on App Engine at: [cloud.google.com/appengine](https://cloud.google.com/appengine)

### Cloud Functions

GCP provides Cloud Functions on a “Functions-as-a-Service”. They are modular pieces of code which executes in response to certain events. So,for microservice-based applications, Cloud Functions are the best option money could buy.

As is with most serverless infrastucture, Cloud Fundtions offer similar benefits as well. For example, increased development velocty & built-in scalability among other stuff. Hence, the developer needn’t worry about server maintenance.

Pricing on Cloud Functions are also very light on the pocket. They are priced based on how long the functions run, the number of times they’re invoked & the extra resources provisioned for the functions.

The only drawback of using Cloud Functions though, is testing them. Since, you’re required to “upload” your functions to GCP, it’s hard to ensure quality of your functions. And, without a robust CI/CD pipeline keeping a watch on the quality standards, things can break. And when they do break, the mess goes south faster than a Bugatti Veron.

That said, peruse through the official documentations for info on Cloud Functions at: [cloud.google.com/functions](https://cloud.google.com/functions).

### Which Service Should You Use

And now, for the question you’ve been waiting for, “ *Which Google serverless service should you use?* “.

The short answer to this question is simple, *it depends!* 😅 But, let’s dive deeper into what contexts does it depend on.

*   Choose Cloud Run if your application is containerized & Kubernetes is a necessity. The major benefit of choosing this context is reproducibility. Since, the application is containerised, the runtime environment can easily be reproduced elsewhere.
*   Choose App Engine if the application isn’t containerised. But, you need a fully-managed platform to deploy the application. With App Engine you let Google take care of managing the backend systems. Scaling it up or down? Let Google do it. Managing dependencies? Let Google handle it as well.
*   And finally, Cloud Functions. Choose it if you want a zero-management way to glue together other modular pieces of code. Especially true if the application is built on top of microservice architecutre. Cloud Functions can act as glue-code for the application. You can design your app to invoke a certain Function only on specific set of events. And Google will take care of scaling it up/down as & when required.

### Final Words

Hopefully you’ve a better understanding of Google’s serverless computing offering right now. I, for sure learned a lot while using & researching each of these services. But I might’ve missed out on something. Or perhaps you would like to add a thing or two to the article. If so, then feel free to reach out to me. 🤗

That said, since you understand serverless computing now, go ahead & deploy something of your own. And if did, you might want to read these articles for further inspiration:

*Originally published at* [*https://jarmos.netlify.app*](https://jarmos.netlify.app/posts/details-of-google-serverless-computing/) *on April 19, 2021.*