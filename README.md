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
* **Rule**: Tells the listener where to send traffic based on conditions.(ALB)
* **Target group**: A group of servers or containers that handle traffic.
* **Traffic shift**: The process of moving all traffic from blue to green.

---

### Things to Keep in Mind

* **More resources needed**: You’re running two versions at the same time, which uses more CPU/memory during deployment.
* **Auto scaling**: If your service auto-scales, it might still scale up/down during deployment — be careful as this could cause failures.
* **Better monitoring**: You get detailed updates on each step of the deployment.
* **Quick rollback**: Since the blue version is still running, you can go back fast if something breaks.

---

### 6 Easy Steps in the Deployment Process

1. **Preparation**
   Set up the new version (**green**) alongside the current one (**blue**). ECS gets everything ready like new service versions and target groups.

2. **Deployment**
   ECS starts running the green version in the background. The blue version still handles all user traffic.

3. **Testing**
   ECS can send test traffic to the green version to make sure it works. Regular users still connect to the blue version.

4. **Traffic Switch**
   ECS slowly or instantly shifts real user traffic from blue to green — based on your settings.

5. **Monitoring**
   ECS watches the new green version closely. If there’s a problem, it can automatically roll back to blue.

6. **Completion**
   If everything looks good, ECS can remove the old blue version. Or you can keep it a bit longer just in case.

---

### Blue/Green Deployment Workflow (Simple Overview)

1. **Start**
   All users go to the blue version. The green version is set up but not getting traffic.

2. **Create Green**
   ECS launches the green tasks and adds them to a new target group (a group of servers).

3. **Health Checks**
   ECS checks if the green version is running properly and is healthy.

4. **Test Traffic (Optional)**
   ECS can send some test requests to green (like special test headers) to confirm it works.

5. **Switch Traffic**
   ECS moves real traffic to green — all at once or slowly (your choice).

6. **Watch Closely**
   ECS checks health, logs, and alarms. If there’s a problem, it switches back to blue automatically.

7. **Bake Time**
   Both blue and green versions run for a short while to make sure everything’s fine.

8. **Finish**
   Green version becomes the new live app. Blue version can be shut down or kept as a backup.

---


## Deployment Lifecycle Stages (Defined by AWS to Monitor our Deployments)

| Stage                                   | What's Happening                                                                                        | Use this stage for lifecycle hook? |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------- |
| **1. RECONCILE_SERVICE**               | ECS checks if you have multiple active versions. Only happens in special cases.                         | Yes               |
| **2. PRE_SCALE_UP**                   | Green version hasn't started yet. Blue is live and handling all user traffic.                           |  Yes               |
| **3. SCALE_UP**                        | Green version starts its containers (tasks), but it's not getting any traffic yet.                      |  No                |
| **4. POST_SCALE_UP**                  | Green is now running, but still no traffic. ECS checks if it's running fine.                            |  Yes               |
| **5. TEST_TRAFFIC_SHIFT**             | Green version receives **test traffic** (fake traffic just for testing). Blue still handles real users. |  Yes               |
| **6. POST_TEST_TRAFFIC_SHIFT**       | Test traffic has fully shifted to green. ECS checks if green passed the tests.                          | Yes               |
| **7. PRODUCTION_TRAFFIC_SHIFT**       | Real user traffic slowly moves from blue to green (like 10%, 50%, 100%).                                |  Yes               |
| **8. POST_PRODUCTION_TRAFFIC_SHIFT** | All real traffic is now going to green. Blue is still running for safety.                               |  Yes               |
| **9. BAKE_TIME**                       | Green version is live. ECS waits to monitor if it's working fine.                                       |  No                |
| **10. CLEAN_UP**                       | Blue version is removed. Green is now your new official version.                                        |  No                |


---

## Example Story: Simple Deployment

1. **Blue is live** (your current app).
2. You **deploy Green**.
3. ECS starts Green containers.
4. ECS sends **test traffic** to Green.
5. ✅ Green passed tests? Then go ahead.
6. ECS moves **real users** to Green **slowly**.
7. All good? Then Blue is deleted.

> * **Test Listener**: Special endpoint only for testing green.
> * **Bake Time**: Green runs for a while to ensure it's stable.
> * **Rollback**: If Green has problems, ECS switches back to Blue.

---

Here’s a **very simplified and crystal-clear version** of the **required resources and best practices** for **Amazon ECS Blue/Green Deployments**, written for beginners who want to grow to advanced levels:

---

## What You Need for ECS Blue/Green Deployment

To safely switch from your old app (blue) to your new version (green), **you must use at least one** of these:

### 1. **Load Balancer or Service Connect (Required for Traffic Shifting)**

You need one of the following so ECS can shift traffic smoothly:

* **Application Load Balancer (ALB)**
* **Network Load Balancer (NLB)**
* **Service Connect** (for ECS Services in a mesh-like setup)

> ❗ If you don’t use any of these, you can **still deploy**, but **you won’t get automatic traffic shifting** — it will be manual.

---

## 🛠️ High-Level Setup Checklist

| Step | What to Do                                                              |
| ---- | ----------------------------------------------------------------------- |
| 1  | Use **ALB**, **NLB**, or **Service Connect** in your ECS service        |
| 2  | In the service definition, set **Deployment Type = Blue/Green**         |
| 3  | Set **Deployment Controller = ECS**                                     |
| 4  | (Optional) Add extra features like:                                     |
| →    | **Bake Time** — time to monitor green before final switch               |
| →    | **CloudWatch Alarms** — auto rollback if problems                       |
| →    | **Lifecycle Hooks** — test green version during deployment using Lambda |

---

## Best Practices (Highly Recommended)

| Practice                                         | Why It's Important                                     |
| ------------------------------------------------ | ------------------------------------------------------ |
| Use **accurate health checks**                 | So ECS knows if green is healthy                       |
| Set a **bake time**                            | Wait a few minutes to catch hidden issues              |
| Use **CloudWatch alarms**                      | Auto rollback if CPU/memory/errors spike               |
| Add **lifecycle hooks**                        | Run test scripts or Lambda checks at each stage        |
| Make sure both blue and green can run together | So the switch doesn’t crash the app                    |
| Have **enough ECS capacity**                   | You need to run both versions side-by-side temporarily |
| Test your rollback process                     | Be ready in case something goes wrong                  |



