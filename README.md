# Blue/Green Deployment
### What is a Blue/Green Deployment?

A **blue/green deployment** is a safe way to release updates to your app or service without downtime. It works by running **two identical environments**:

* **Blue**: The current live version.
* **Green**: The new version you want to release.

With this method, you test the green version first. If everything looks good, you switch traffic from blue to green. If something goes wrong, you can quickly switch back.

---

### Benefits of Blue/Green Deployment

* **Safer updates**: You test the new version before sending real user traffic.
* **No downtime**: Users won’t notice the switch — your app stays online.
* **Easy rollback**: If there’s a problem, you can go back to the old version (blue) right away.
* **Real-world testing**: Test new changes with real traffic without affecting users.
* **Consistent process**: Each deployment follows clear steps, making it more reliable.
* **Automated checks**: You can run automated tests during each step to make sure things work.

---

### Key Terms

* **Bake time**: The period when both versions (blue and green) are running after traffic is switched.
* **Blue deployment**: The current version running in production.
* **Green deployment**: The new version you’re releasing.
* **Lifecycle stage**: Steps in the deployment process, like testing before traffic is switched.
* **Lifecycle hook**: A special step (like a Lambda function) that checks if the deployment is working.
* **Listener**: Listens for incoming traffic (requests) and sends it to the right version.
* **Rule**: Tells the listener where to send traffic based on conditions.
* **Target group**: A group of servers or containers that handle traffic.
* **Traffic shift**: The process of moving all traffic from blue to green.

---

### Things to Keep in Mind

* **More resources needed**: You’re running two versions at the same time, which uses more CPU/memory during deployment.
* **Auto scaling**: If your service auto-scales, it might still scale up/down during deployment — be careful as this could cause failures.
* **Better monitoring**: You get detailed updates on each step of the deployment.
* **Quick rollback**: Since the blue version is still running, you can go back fast if something breaks.

---

Let me know if you'd like a diagram or a one-page summary too!
