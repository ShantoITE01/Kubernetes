

**Kubernetes Architecture (K8s)** 



### 🧠 **Overview**

Kubernetes is a **container orchestration system** — it automatically manages, deploys, scales, and maintains containers (like Docker containers) across multiple servers.

It’s made up of two main parts:

1. **Control Plane (Master Node)**

2. **Worker Nodes**

---

## ⚙️ 1. Control Plane (Master Node)

The **Control Plane** manages and controls the entire Kubernetes cluster.

It decides **what runs where** and monitors the cluster’s health.

### 🧩 Components:

#### 🟩 API Server

* The **entry point** for all commands (from `kubectl`, dashboard, etc.).

* It communicates with all other components.

* Example: When you type `kubectl get pods`, the API Server handles it.

#### 🟩 etcd

* A **key-value database** that stores all cluster data (like configuration, secrets, and node states).

* Think of it as Kubernetes’ **memory**.

#### 🟩 Controller Manager

* Watches the cluster and ensures the **desired state** is maintained.

* For example, if a pod crashes, it tells the system to create a new one.

#### 🟩 Scheduler

* Decides **which node** a pod will run on.

* It looks at CPU, memory, and resource availability.

---

## 🖥️ 2. Worker Nodes

Each **worker node** runs actual applications (containers).

The control plane sends instructions to these nodes.

### 🧩 Components:

#### 🟨 Kubelet

* An **agent** running on each node.

* It receives tasks (like “run this container”) from the Control Plane and ensures containers are running properly.

#### 🟨 Kube Proxy

* Manages **network communication** inside and outside the cluster.

* Ensures services can talk to each other securely.

#### 🟨 Container Runtime

* The actual software that runs containers (like **Docker**, **containerd**, etc.).

---

## 🧱 3. Pod

* The **smallest deployable unit** in Kubernetes.

* Each pod contains one or more containers that share storage and network.

---

## 📡 How It All Works (In Short)

1. You send a command → `kubectl apply -f app.yaml`.

2. The **API Server** receives it.

3. The **Scheduler** picks a node.

4. The **Kubelet** on that node runs the pod.

5. **Controller Manager** ensures it keeps running.

6. **etcd** stores the state.

7. **Kube Proxy** manages network between pods.

---



---

## ☸️ **Kubernetes কীভাবে কাজ করে (বাংলায় সহজভাবে)**

Kubernetes সিস্টেমটা দুই ভাগে ভাগ করা যায়:

1. 🧠 **নিয়ন্ত্রণ সমষ্টি (Control Plane / Master Node)**

2. ⚙️ **কাজের প্রকল্প (Worker Nodes)**

---

## 🧠 **১️⃣ নিয়ন্ত্রণ সমষ্টি (Control Plane / Master)**

এটা পুরো ক্লাস্টারের **মস্তিষ্ক**।

এখান থেকে Kubernetes ঠিক করে কোন অ্যাপ কোথায় চলবে, কেমনভাবে চলবে।

### 🔹 প্রধান উপাদান:

#### **a. API Server**

* ইউজার যখন `kubectl` কমান্ড দেয়, প্রথমে সেটা এখানে আসে।

* এটা হলো Kubernetes-এর **গেটওয়ে (Entry Point)**।

* সব কনফিগারেশন আর নির্দেশ এখানেই জমা হয়।

🧩 উদাহরণ:
তুমি যদি লেখো

```bash
kubectl get pods
```

তাহলে API Server **etcd** থেকে তথ্য এনে তোমাকে দেখায়।

---

#### **b. etcd**

* এটা হলো Kubernetes-এর **ডেটাবেস**।

* সব তথ্য (পড কোথায় চলছে, কয়টা নোড আছে, ইত্যাদি) এখানে সংরক্ষিত থাকে।

---

#### **c. Scheduler**

* নতুন Pod কোথায় (কোন Node-এ) চলবে, সেটার সিদ্ধান্ত নেয়।

* দেখে কোন Node-এর CPU/RAM ফাঁকা আছে।

🧩 উদাহরণ:

Node1 ব্যস্ত, Node2 ফাঁকা → Scheduler Pod-টা Node2 তে চালাবে।

---

#### **d. Controller Manager**

* এটা Kubernetes-এর **ম্যানেজার**।

* কাজ হলো সবকিছু ঠিকভাবে চলছে কিনা দেখা।
  যেমন:

  * কোনো Pod মারা গেলে নতুনটা চালায়।

  * Replica সেট ঠিক আছে কিনা চেক করে।

---

## ⚙️ **২️⃣ কাজের প্রকল্প (Worker Node)**

এগুলো হলো **সার্ভার বা কম্পিউটার** যেখানে আসল অ্যাপ্লিকেশন চলে।

### 🔹 প্রধান উপাদান:

#### **a. Kubelet**

* প্রতিটি Node-এ থাকে।

* Master থেকে নির্দেশ পায় এবং Pod চালায়।

* দেখে যে Pod গুলো চলছে কিনা, না চললে জানায়।

---

#### **b. Service Proxy (kube-proxy)**

* Networking দেখে।

* Pod গুলোর মধ্যে যোগাযোগ ঠিক রাখে।

* Load balancing করে।

---

#### **c. Pod**

* এটা হলো **সবচেয়ে ছোট ইউনিট**।

* প্রতিটা Pod-এর ভিতরে এক বা একাধিক **Container (App)** থাকে।

* যেমনঃ একটাতে তোমার Web App, আরেকটাতে Database।

---

## 🧩 **কাজের ধারা (Workflow):**

1. ইউজার `kubectl` দিয়ে একটা YAML ফাইল apply করে।

2. API Server সেটা পড়ে `etcd` তে সেভ করে।

3. Scheduler দেখে কোন Node ফাঁকা আছে।

4. Controller Manager নিশ্চিত করে Pod তৈরি হয়েছে।

5. সেই Node-এর Kubelet Pod চালায়।

6. kube-proxy Pod-এর যোগাযোগ ঠিক রাখে।

---

## 🔁 **CNI Network (Weave Net / Calico ইত্যাদি)**

এইটা Node গুলোর মধ্যে **Networking Layer**।

এটার মাধ্যমে সব Pod একে অপরের সাথে কথা বলে।

---


