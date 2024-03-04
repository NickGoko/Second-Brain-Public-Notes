---
tags:
  - cloud/aws
review-frequency: normal
reviewed: 2023-12-21
---
# Amazon Braket Getting Started
🌟<mark style="background: #BBFABBA6;">Amazon Braket is the fully managed quantum computing service on AWS. </mark>  
With **Braket APIs**, you can <mark style="background: #BBFABBA6;">interact with quantum processing units (QPUs) or on-demand simulators. </mark>
- You can also run advanced hybrid algorithms that combine quantum and classical resources. 
- Braket provides a software library, or **Amazon Braket SDK**, to <mark style="background: #ABF7F7A6;">streamline working with Braket APIs in Python.</mark>

- ✨Quantum computing has the potential to solve computational problems that are beyond the reach of classical computers. 
- It does this by harnessing the _laws of quantum mechanics_ to process information in new ways.
- Braket <mark style="background: #FFF3A3A6;">supports your quantum computing research and helps you assess the maturity and potential of the technology.</mark>

![](https://i.imgur.com/9XLeXbi.png)


#### What Problems Does **Amazon Braket** Solve?
- Many quantum devices are available only in labs or through individual web portals from hardware manufacturers. This often requires you to negotiate long-term subscriptions and familiarize yourself with bespoke tooling and interfaces. This slows innovation and makes it difficult to fairly evaluate and compare technologies.  
- <mark style="background: #BBFABBA6;"> Braket is a one-stop shop for quantum computing. Braket is a cross-technology quantum computing service that enables you to research and explore different types of quantum computers through a consistent programming experience and tooling, from uperconducting circuit-based quantum computers, trapped ion quantum computers, and neutral-atom based Analog Hamiltonian Simulation (AHS).</mark>

- <mark style="background: #FFB86CA6;">Braket is fully integrated with AWS.</mark>  
  - <mark style="background: #ADCCFFA6;">Combine quantum computing with scalable classical compute options on AWS to explore hybrid quantum-classical algorithms.</mark> Then, you can benchmark them against state-of-the-art classical approaches. 
  - You can use familiar AWS tools for monitoring, user access management, and encryption. 
  - In addition, you can create secure environments for your teams to research applications. Braket is always adding new quantum processors to give customers access to the newest technology and highest quality QPUs to accelerate research.

![](https://i.imgur.com/NncjGVr.png)

#### **How Does Amazon Braket work?**
As new quantum technologies emerge and are added to Braket, your development experience will remain consistent. _Braket helps you through the three main stages of quantum program development._  
<mark style="background: #BBFABBA6;">Build</mark> - <mark style="background: #ADCCFFA6;">Braket provides fully managed Jupyter notebook environments to help you get started.</mark>  
- <mark style="background: #FFB86CA6;">Braket notebooks are preinstalled with sample algorithms, resources, and developer tools</mark>, including the Braket SDK.  
- The **Braket SDK** is a unified interface for building quantum programs that run on all the different QPUs on Braket by only changing a few lines of code.

<mark style="background: #BBFABBA6;">Test</mark>- <mark style="background: #ADCCFFA6;">Braket provides access to fully managed, high-performance quantum circuit simulators. You can test and validate your circuits. </mark>Braket handles all the underlying software components and Amazon Elastic Compute Cloud (Amazon EC2) clusters. This takes away the burden of simulating quantum circuits on classical HPC infrastructure.

<mark style="background: #BBFABBA6;">Run</mark> - <mark style="background: #ADCCFFA6;">Braket provides secure, on-demand access to different types of quantum computers. </mark>  
You have access to <mark style="background: #D2B3FFA6;">quantum devices</mark> from multiple quantum hardware providers, including <mark style="background: #D2B3FFA6;">superconducting, trapped ion, neutral-atom quantum computers.</mark>You also have no upfront commitment and no need to procure access through individual providers.

<mark style="background: #FF5582A6;">Amazon Braket provides everything you need to build, test, and run quantum algorithms on AWS</mark>

#### **How Much Does Amazon Braket cost?**
Beyond the AWS Free Tier, you pay only for the AWS resources that you use.  
<mark style="background: #ADCCFFA6;">Braket provides access to quantum computers, quantum circuit simulators, and Jupyter notebook development environments.</mark>  
<mark style="background: #FFB86CA6;">It also gives you the ability to run fully managed hybrid quantum-classical algorithms.</mark>

You will be billed separately for use of each of these capabilities. You will also be billed for other AWS services you use with Braket, such as Amazon Simple Storage Service (Amazon S3) for storing the results of quantum computations.

## Architecture and Use Cases
#### **How Is Amazon Braket Used to Architect a Cloud solution?**
<mark style="background: #FFB86CA6;">Braket provides on-demand access to quantum computing devices, including on-demand circuit simulators and different types of QPUs. </mark>  
In Braket the atomic request to a device is a quantum task.  
For gate-based QC devices, this request includes the quantum circuit (plus the measurement instructions and number of shots) and other request metadata.  
For Analog Hamiltonian Simulation (AHS), the task contains the physical layout of the quantum register and the time and space dependence of the manipulating fields.

![](https://i.imgur.com/8PMvrwk.png)

1. **Create task**  
	With Jupyter notebooks, you can conveniently define, submit, and monitor your tasks using the Amazon Braket SDK.  
	Submitting the program to a device creates an AWS resource called a **task**.  
	A **task** is a sequence of repeated shots based on the same circuit design or Hamiltonian specification. You define how many shots you want included in a task when you submit it to Braket. 
2. **Submit task to API**  
	<mark style="background: #CACFD9A6;">After your task is defined, you can choose a device to run it on and submit it to the Amazon Braket API.</mark> <mark style="background: #ABF7F7A6;">You can create quantum tasks through the Amazon Braket SDK or by using the CreateQuantumTask API operation directly. </mark>
3. **Send task to QPU or simulator** - <mark style="background: #CACFD9A6;">Depending on the device you choose, the task is queued until the device becomes available, and the task is sent to run on the QPU or simulator. </mark>  
   <mark style="background: #ABF7F7A6;">You can view your quantum task on the Tasks page of the Amazon Braket console or by using the GetQuantumTask or SearchQuantumTasks API operations. </mark>
4. **Return results to S3 bucket**  
	Braket returns the results to an S3 bucket where the data is stored in your AWS account.  
	You can monitor your task status in the Amazon Braket console by using the SDK or by using the GetQuantumTask API directly. 
5. **Integrate with other AWS services**  
	Braket is integrated with Amazon CloudWatch and AmazonEventBridge, among other AWS services. This helps to provide monitoring and event base processes for task status changes. 

---
#### **What Are the Basic Technical Concepts of Amazon Braket?**

🔹 [Quantum Circuit](#)  
	<mark style="background: #CACFD9A6;">Is the instruction set that defines a computation on a gate-based quantum computer.</mark> A quantum circuit is a sequence of quantum gates together with measurement instructions. 
	
🔹 [Quantum processing unit](#)  
	<mark style="background: #ABF7F7A6;">A QPU is a physical quantum computing device where you can a quantum task.</mark> Braket provides AWS customers with access to quantum computing technologies from multiple quantum hardware providers. This includes superconducting, trapped ion, and neutral-atom quantum computers. 
	
🔹[Device](#)  
	In Braket, <mark style="background: #ABF7F7A6;">a device is a QPU or simulator that you can call to run quantum tasks.</mark> Braket provides access to QPU devices from quantum hardware providers, on-demand simulators, local simulators, and embedded simulators.  
	For all devices, you can find device properties, such as device topology, calibration data, and native gate sets, on the Devices page of the Amazon Braket console. You can also find device properties through the Braket API.
	
🔹 [Task](#)  
	In Braket, <mark style="background: #ABF7F7A6;">a task or quantum task is the atomic request to a device. </mark>  
	For gate-based quantum computing devices, this includes the quantum circuit, including the measurement instructions and number of shots and other requested metadata. For AHS, **the task contains the physical layout of the quantum register and the time dependence and space dependence of the manipulating fields.**  
	<mark style="background: #ABF7F7A6;">You can create quantum tasks through the Braket SDK or by using the CreateQuantumTask API operation directly</mark>. After you create a task, it is queued until the requested device becomes available. You can view your quantum tasks on the Tasks page of the Amazon Braket console or by using the GetQuantumTask or SearchQuantumTasks API operations.
	
🔹 [Shots](#)  
	Because quantum computing is inherently probabilistic, any circuit needs to be evaluated multiple times to get an accurate result.  
	A single circuit evaluation and measurement is called a shot. The number of shots, or repeated evaluations, for a circuit is based on how accurate you want the result to be. The number of shots can range from 10–100,000 shots per task.
	
🔹 [Braket Notebook Instances](#)  
	<mark style="background: #ABF7F7A6;">A Braket Notebook Instance is a Jupyter notebook instance fully managed by Amazon Braket.</mark> The Amazon Braket notebook instances are based on Amazon SageMaker notebook instances and come pre-installed with the Amazon Braket SDK, example tutorials, and plugins. You can launch Braket Notebook Instances from the AWS Management Console.

🔹 [Braket local simulator](#)  
	The local simulators are included in the Amazon Braket SDK at no cost. They can run on your laptop or within an Amazon Braket managed notebook. You can use them for quick validation of circuit designs. They are well suited for small and medium-scale simulations – up to 25 qubits without noise, or up to 12 qubits with noise, depending on your hardware.

🔹 [Braket on-demand simulator](#)  
	<mark style="background: #ABF7F7A6;">Braket includes access to fully managed on-demand simulators</mark>. All on-demand simulators automatically scale AWS computing resources to deliver high-performance execution of your quantum algorithms.  
	<mark style="background: #ABF7F7A6;">The cost of using the Amazon Braket on-demand simulators is based on the duration of each simulation task</mark>.  
	When you use on-demand simulators, you are billed at a per-minute rate, in increments of one millisecond, for the time your simulation takes to run, with a minimum billing duration of 3 seconds per simulation.

🔹 [Amazon Braket Hybrid Jobs](#)  
	<mark style="background: #BBFABBA6;">Amazon Braket Hybrid Jobs provides additional support for hybrid quantum-classical algorithms. </mark>You can run <mark style="background: #D2B3FFA6;">fully managed hybrid algorithms that combine AWS classical compute resources based on Amazon EC2, or the job instance, with Braket QPUs or quantum circuit simulators.</mark>  
	While your job is running, it has priority access to the selected target QPU, AND tasks from your job run ahead of other tasks queued on the device. This results in shorter, more predictable runtimes for hybrid algorithms.  
	<mark style="background: #ABF7F7A6;">For hybrid variational algorithms, the QPUs act as coprocessors to classical computers. This is similar to how a graphics processing unit (GPU) is used in training machine learning models. </mark>  
	Such hybrid algorithms rely on iterative computations between classical computers and QPUs or simulators.  
	With the Braket Hybrid Jobs feature, Braket coordinates the necessary quantum and classical compute resources. It then runs your algorithm and releases the resources after the job is complete, so you pay only for what you use.

🔹S3 bucket  
🔹 IAM roles  
🔹IAM policies

![](https://i.imgur.com/LxOFpPs.png)


#### **What Are Typical Use Cases for Amazon Braket?**
##### Research Quantum Computing Algorithms.
Since launch, Amazon Braket has been committed to providing customers with a single access point to different quantum hardware choices, allowing them to experiment and innovate with multiple quantum processing units (QPUs) through the same interface.

As a research scientist or quantum algorithm developer, you can quickly get started with developing your own code on Amazon Braket by referencing our ready-to-use examples, and running these algorithms on a variety of on-demand, managed simulators, and quantum processors available on Braket.

Modern quantum algorithms involve close coupling between the classical and quantum resources. With Hybrid Jobs, you can run algorithms that use both classical and quantum compute resources. These hybrid quantum-classical methods include the [Quantum Approximate Optimization Algorithm(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/hybrid_quantum_algorithms/QAOA/QAOA_braket.ipynb) (QAOA), [Variational Quantum Eigensolver(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/hybrid_quantum_algorithms/VQE_Chemistry/VQE_chemistry_braket.ipynb) (VQE), and [typical quantum machine learning workflows(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/hybrid_jobs/1_Quantum_machine_learning_in_Amazon_Braket_Hybrid_Jobs/Quantum_machine_learning_in_Amazon_Braket_Hybrid_Jobs.ipynb).

##### Test Different Quantum Hardware
Push the boundaries of quantum hardware research with convenient access to superconducting, trapped-ion, and neutral-atom devices. Braket is typically used when you want to access quantum computing technologies for research and development or educational purposes. By running algorithms on different types of quantum hardware with Braket, you can directly compare technologies and assess which quantum hardware best fits your different applications.

##### Develop Open-source Software
Contribute new quantum applications and influence software features, tools, or plugins that can make development more efficient.

For example, Braket provides support for [PennyLane(opens in a new tab)](https://amazon-braket-pennylane-plugin-python.readthedocs.io/en/latest/), an open-source software framework built around the concept of quantum differentiable programming. You can use this framework to train quantum circuits. It is similar to training a neural network to find solutions for computational problems in quantum chemistry, quantum machine learning, and optimization. <mark style="background: #BBFABBA6;">The PennyLane library provides interfaces for familiar machine learning tools, including PyTorch and TensorFlow, to make training quantum circuits quick and intuitive.</mark>

#### **What Else Should You Keep in Mind about Amazon Braket?**
##### Test before Running
Running on quantum hardware can be resource intensive, so it's important to test applications before running on QPUs. The simulators can be used to debug, fine-tune, and experiment with quantum programs before sending the task or job to the QPU.

##### Localize by Region
QPUs are available in their corresponding Region by their Amazon Resource Name (ARN) on the developer’s guide page listing the Braket devices. When checking the AWS Management Console for results of a task or job, ensure that you're in the same Region as the QPU.

The SageMaker notebook instances are also localized to Regions. If you don’t see your notebook instances, make sure that you’re in the same Region where the resource was created.

### How Do You Set Up Braket in the AWS Management Console?
Open the AWS Management Console, and search for Braket in the Services search bar. Then, choose Amazon Braket.  
  
On the Service dashboard, choose Get started.  
  
Go through each step and agree to the terms and conditions. This first step creates a service linked role, which gives you access to Braket.

### How Do You Run Amazon Braket on an On-Demand Simulator?
<mark style="background: #D2B3FFA6;">Use the state vector simulator (SV1) to emulate the results of using Braket without engaging actual quantum computing hardware.</mark>  
With the AWS Free Tier, you can use the simulator managed by Braket for up to 1 hour of free simulation time per month. This is sufficient time to run Demo 2 successfully.  
<mark style="background: #D2B3FFA6;">run the same Bell state task on the state vector simulator (SV1) to emulate the results of using actual quantum computing hardware.</mark>  
To access the on-demand quantum circuit simulators, we need the device Amazon Resource Name (ARN). _You can find a list of all simulators and QPUs available through Amazon Braket on the AWS Management Console._ In the navigation pane, choose **Devices**.  
Information about available devices and simulators is displayed, including names and availability windows.  
You can also find the list of available Braket devices in the Amazon Braket Developer Guide. Pricing for each of the devices is found on the pricing page or by choosing the name of the device.

Use the <mark style="background: #ADCCFFA6;">state vector simulator, or SV1</mark>.  
<mark style="background: #CACFD9A6;">It is an on-demand, high-performance, universal state vector simulator.</mark>  
Circuits that require connectivity between arbitrary qubits, also known as all-to-all connectivity, are well suited for SV1. It returns results in forms such as a full state vector or an array of amplitudes.

Select **SV1**.  
To access specific quantum resources, you will need to get the ARN for the device. Copy the Device ARN, which you will use to update the Getting started with Amazon Braket notebook.

In the navigation pane, choose **Notebooks**. Then, select the Amazon SageMaker instance created previously.  
  
The Getting started with Amazon Braket notebook should open by default.  
  
Now, you need to find the call to the LocalSimulator(). In the next steps, you will edit the notebook to run on the SV1 simulator instead of on the local simulator.  
  
First, delete the string "device = LocalSimulator()".  
  
Next, enter "from braket.aws import AwsDevice".  
  
On the subsequent line, enter "device = AwsDevice()".

You will now need the ARN number.  
  
Paste the ARN you copied from the Amazon Braket Devices page for the SV1 device between the quotation marks. Do not include additional trailing or leading spaces. To paste the clipboard contents, on Windows devices, press Ctrl V, and on Mac devices, press Command V.  
  
Now, you can run your quantum circuit on the SV1 on-demand simulator by running all cells. Choose **Run**, and then choose **Run All Cells**.  
  
If you want to run individual cells, select the desired cell and press Shift+Enter.  
  
The results from the SV1 will be displayed in the last cell of the Jupyter notebook. You have now run your first quantum circuit on an on-demand simulator.

### How Do You Run Amazon Braket on a QPU?
Use the full Braket service and quantum computing capabilities of AWS. This demo incurs charges from the use of the IonQ Aria device in this example. The cost can be reduced by changing shots=1000 to shots=100 or less, as illustrated in the demo. You can avoid the QPU charges entirely by not running this demo.  
In this demonstration, we will <mark style="background: #D2B3FFA6;">run the same Bell state task on a QPU instead of the local simulator. </mark>  
<mark style="background: #ADCCFFA6;">The runtime will depend on the availability of the QPU, and running on a QPU will incur additional costs per the pricing page. </mark>  
There is an additional charge for using the IonQ device in this example. The cost can be reduced by changing shots equals 1000 to shots equals 100 or less.  
<mark style="background: #ADCCFFA6;">To access quantum devices, you will need the device Amazon Resource Name, or ARN.</mark> You can find a list of all simulators and QPUs available through Amazon Braket on the AWS Management Console. In the navigation pane, choose **Devices**

>[!missing] Next steps missing

### How Do You Use Amazon Braket with a Programming Language?
#### **What Programming Languages Can You Use with Amazon Braket?**


To learn more about using programming languages with Braket, expand each of the following five sections.
1. <mark style="background: #D2B3FFA6;">Python SDK</mark>  
   The <mark style="background: #CACFD9A6;">Amazon Braket Python SDK is an open-source library used to design and build quantum circuits, submit them to Braket devices as quantum tasks, and monitor their progress.</mark> The project homepage is on GitHub.  
You can perform local installation using pip by running the following command:  
	``pip install amazon-braket-sdk``  
The SDK includes a local simulator, so you can perform prototyping and testing without an AWS account.
2. <mark style="background: #D2B3FFA6;">PennyLane</mark>  
   With the Amazon Braket SDK, you can use other popular software libraries. <mark style="background: #CACFD9A6;">PennyLane is a machine learning library for optimization and automatic differentiation of hybrid quantum-classical computations. It is preinstalled on notebook instances and integrated into Amazon Braket Hybrid Jobs. </mark>
3. <mark style="background: #D2B3FFA6;">Qiskit</mark>  
   Using the Qiskit provider for Braket, with a few lines of code, you can modify existing algorithms written in Qiskit. This is a widely used open-source quantum programming SDK.
4. <mark style="background: #D2B3FFA6;">Julia</mark>  
   If you prefer to work in Julia instead of Python, you can use Braket.jl. This package is a Julia implementation of the Amazon Braket SDK.
   
5. <mark style="background: #D2B3FFA6;">Open Quantum Assembly Language</mark>  
   You might prefer to work in languages such as C++, Go, Java, JavaScript, Ruby, or Hypertext Preprocessor (PHP). You can send quantum circuits and algorithms written in the Open Quantum Assembly Language (OpenQASM) directly to the service using the AWS SDK in the corresponding language.

### How Do You Delete Resources Used by Amazon Braket?

The Amazon Braket managed notebooks uses the Amazon SageMaker notebook instances. SageMaker charges for uptime regardless of whether the SageMaker notebook instance is idle. Consequently, you should remember to shut down the notebook instance when you are finished.

To change Regions, choose the Region dropdown menu in the upper-right corner. Select the Region where you created the SageMaker notebook instances.  
  
In the Amazon Braket navigation pane, choose Notebooks.  
  
Select the circle next to the instance you want to shut down.  
  
For Actions, choose Stop.  
  
If you have more than one notebook instance, select the circle next to the name of the instance you want to shut down.  
  
The Status should read Stopping.  
  
Thank you for your participation.

## **What Else is AWS Doing in Quantum technology?**
- <mark style="background: #FFB86CA6;">The Amazon Quantum Solutions Lab (QSL) </mark>is a collaborative research and professional services program. Through QSL, you can work with leading experts in quantum computing, machine learning, optimization, and high-performance computing (HPC). The program helps you research and identify the most promising applications of quantum computing and develop a quantum strategy while delivering value today. 
- At the <mark style="background: #FFB86CA6;">AWS Center for Quantum Computing (CQC)</mark>, we are embarking on a journey to build a fault-tolerant quantum computer. The CQC conducts research into hardware development and quantum error correction. The CQC is not customer-facing. 
- The <mark style="background: #FFB86CA6;">AWS Center for Quantum Networking (CQN)</mark> is pursuing research to put quantum communication technology in the hands of our customers. The CQN is making advances toward a fully developed quantum network that can distribute entanglement between end nodes. Research at the CQN is focused on developing quantum memories and repeaters. The CQN is not customer-facing.


# Amazon Braket Quantum Application Development
With Amazon Braket, customers can test and evaluate a range of quantum computers and research quantum algorithms. This course builds on the _Amazon Braket Getting Started_ course.

In this course, you will <mark style="background: #FFB86CA6;">learn how to use Braket to run programs on quantum processing units (QPUs).</mark>  
You will <mark style="background: #FFB86CA6;">explore advanced service features, such as cost tracking and Amazon Braket Hybrid Jobs.</mark>  
Through demonstrations and exercises, you will also learn about the features, functionality, and applications of Braket.

In this course, you will:

- Describe Braket, including key concepts, use cases, and features.
- Create and run quantum tasks and hybrid jobs on QPUs and simulators.
- Use Braket from both the AWS Management Console and the Amazon Braket Python SDK.
- Understand how and when to use key features of Braket, such as Amazon Hybrid Jobs and Braket Pulse.
- Explore the Braket pricing scheme and tools for estimating and tracking costs.

## **What Is Quantum computing?**
Essentially, <mark style="background: #ABF7F7A6;">quantum computing is a new way of processing information that uses quantum coherence and entanglement.</mark>  
<mark style="background: #CACFD9A6;">It has the potential to solve computational problems beyond the reach of classical computers by using the laws of quantum mechanics.</mark>

Quantum devices process information differently than conventional information processing. The way that quantum computers solve problems is fundamentally new and different.  
<mark style="background: #CACFD9A6;">Instead of using traditional CPU and memory models, _qubits_—the building blocks of a quantum computer—are used to store and process quantum information.</mark>  
While quantum computers have the potential to be disruptive, we are still in the early stages of this technology. Significant scientific and engineering challenges need to be overcome before customers can use quantum computing to address business problems.  
![](https://i.imgur.com/qbJbDdy.png)  
You might wonder why a quantum computer can provide speedups for some problems but not for others.  
<mark style="background: #CACFD9A6;">A quantum computer has a different model of computation than conventional computers. </mark>  
In this model, there are algorithms that, for certain problems, are exponentially faster than the fastest possible—or fastest known—classical algorithms.  
<mark style="background: #CACFD9A6;">Integer factoring is known to be efficiently solvable using quantum resources.</mark> <mark style="background: #FFF3A3A6;">Some algorithms, such as the Grover Search algorithm, have demonstrated polynomial speedups.</mark> In these cases, there is no known classical algorithm for doing the same task in a reasonable amount of time.  
<mark style="background: #083CA4A6;">Discovering new algorithms where quantum computers are more efficient than their classical counterparts is an active area of research.</mark>  
![](https://i.imgur.com/A5FNRpN.png)  
[Resources](#)
- [60minutes Quantum Computing Youtube Video](https://www.youtube.com/watch?v=K4ssT6Dzmnw&list=TLPQMDgxMjIwMjNJF_u4Fnwsnw&index=3)
- [Quantum computers explained](https://www.youtube.com/watch?v=e3fz3dqhN44&list=TLPQMDgxMjIwMjNJF_u4Fnwsnw&index=2&pp=gAQBiAQB)
- [The Map of Quantum Computing](https://www.youtube.com/watch?v=-UlxHPIEVqA&list=TLPQMDgxMjIwMjNJF_u4Fnwsnw&index=4)
## Overview of Braket
**Lesson objectives**  
By the end of the lesson, you will be able to do the following:
- Recall the key stages of quantum program development.
- Plan your journey through the key features of Braket.

### **Braket For Quantum Program development**
As new quantum technologies emerge and are added to the Braket service, your development experience will remain consistent. Braket helps you through the four main stages of quantum program development.  
![[#**How Does Amazon Braket work?**]]  
<mark style="background: #BBFABBA6;">Analyze</mark> - Braket is integrated with AWS services, such as Amazon CloudWatch, AWS CloudTrail, Amazon EventBridge, and AWS Identity and Access Management (IAM). This means you can monitor workloads, generate notifications when your tasks are complete, and manage access controls and permissions.  
<mark style="background: #CACFD9A6;">Your simulation and quantum task results are delivered to your preferred Amazon Simple Storage Service (Amazon S3) bucket for storage and analysis. This gives you full control over your data.</mark>


### Security in Bracket
As a managed service, Braket is protected by AWS global network security procedures. Security is a shared responsibility between AWS and you. The shared responsibility model describes AWS and you.  
The shared responsibility model describes this as security of the cloud<mark style="background: #FFB86CA6;">AWS</mark> and security in the cloud<mark style="background: #FFB86CA6;">You/Customer</mark>: 

QPUs on Braket are hosted by third-party hardware providers. If you use Braket for access to quantum computing hardware operated by a third-party hardware provider, your circuit and its associated data are processed by hardware providers outside of facilities operated by AWS.

<mark style="background: #CACFD9A6;">Your content is anonymized. Only the content necessary to process the circuit is sent to third parties.</mark>  
AWS account information is not transmitted to third parties.  
All data is encrypted at rest and in transit.  
Data is decrypted for processing only.  
<mark style="background: #CACFD9A6;">Braket third-party providers are not permitted to store or use your content for purposes other than processing your circuit. </mark>  
After the circuit completes, the results are returned to Braket and stored in your S3 bucket.

<mark style="background: #CACFD9A6;">The security of Braket third-party quantum hardware providers is audited periodically to ensure that standards of network security, access control, data protection, and physical security are met.</mark>

### What Are the Basic Technical Concepts of Braket?

Users of Braket should have a basic understanding of the following concepts. To learn more, expand each of the following four categories.  
<mark style="background: #FF5582A6;">QPU</mark>  
	A **QPU** is a physical quantum computing device where you can run a quantum task.  
	Braket provides AWS customers with access to quantum computing technologies from multiple quantum hardware providers.  
	This includes **superconducting, trapped ion, and neutral-atom quantum computers**  
<mark style="background: #FF5582A6;">Device</mark>  
	In Braket, a device is a QPU or simulator that you can call or run quantum tasks. Braket provides access to QPU devices from quantum hardware providers, on-demand simulators, local simulators, and embedded simulators.  
	<mark style="background: #ABF7F7A6;">For all devices you can find further device properties, such as device topology, calibration data and built in device gate sets, on the Devices tab of the Braket console or by using the Braket API. </mark>  
<mark style="background: #FF5582A6;">Quantum task</mark>  
	In Braket, a quantum task is the atomic request to a device.  
	For gate-based quantum computing devices this include the quantum circuit, including the measurement instructions, number of shots, and other requested metadata.  
	For Analog Hamiltonian Simulation(AHS) the task contains the physical layout of the quantum register and the time dependence and space dependence of the pulse schedule.  
	<mark style="background: #ABF7F7A6;">You can create quantum tasks through the Braket SDK or by using the CreateQuantumTask API operation directly. After you create a task, it is queued until the requested device becomes available. </mark>  
	You can view your quantum tasks on the Tasks page of the Braket console or by using the GetQuantumTask or SearchQuantumTask API operations.  
<mark style="background: #FF5582A6;">Shots</mark>  
	Because quantum computing is inherently probabilistic, any circuit needs to be evaluated multiple times to get an accurate result.  
	<mark style="background: #D2B3FFA6;">A single circuit evaluation and measurement is called shot</mark>.  
	The number of shots, or repeated evaluations, for a circuit is based on how accurate you want the result to be.  
	The number of shots can range from 10-100,00 shots per task. 

### How to Use Braket
<mark style="background: #FFB86CA6;">Braket structures the experience for scientists and developers to explore quantum computing.</mark> <mark style="background: #083CA4A6;">From the ideation stage to running algorithms on quantum devices, Braket provides tools and features to support your journey to developing quantum applications.</mark>

<mark style="background: #D2B3FFA6;">Tasks are standalone requests of a device.</mark> Such requests include a quantum circuit or an Analog Hamiltonian Simulation program along with the number of shots to be performed.  
Braket provides tools and a plugin to help you build tasks, test them on simulators, and run them on QPUs.

<mark style="background: #FFB86CA6;">Many quantum algorithms require interacting over numerous tasks to learn the outcome of the algorithm.</mark>  
<mark style="background: #ABF7F7A6;">Amazon Braket Hybrid Jobs helps make running hybrid quantum-classical workloads faster, more efficient, and more predictable.</mark>

## **How Is Braket Used to Architect a Cloud solution?**
Braket provides on-demand access to quantum computing devices, including on-demand circuit simulators and different types of QPUs.  
In Braket, **the atomic request to a device is a quantum task (often referred to as a _job_ outside of AWS)**.

For gate-based quantum computing devices, this request includes the quantum circuit plus the measurement instructions, number of shots, and other request metadata. For Analog Hamiltonian Simulation, the task contains the physical layout of the quantum register and the time and space dependence of the manipulating fields.

A Python example of how to run a two-qubit circuit is as follows. In the code snippet following this diagram, the SDK polls for the results in the background and loads them into the Jupyter notebook, Amazon Braket Hybrid Jobs, or the local environment at task completion.  
[View code example](#)
```
# choose the on-demand simulator to run the circuit  
 from braket.aws import AwsDevice

device = AwsDevice("arn:aws:braket:::device/quantum-simulator/amazon/sv1")

# create a circuit with a result type  
circ = Circuit().rx(0, 1).ry(1, 0.2).cnot(0,2).variance(observable=Observable.Z(), target=0)  
  
# add another result type  
 circ.probability(target=[0, 2])
 
# submit the task to run  
 my_task = device.run(circ, shots=1000)

# get results of the task  
 result = my_task.result()
```

**Creating tasks using Qiskit and the Qiskit-Braket provider**  
You can run algorithms written with a few lines of code in Qiskit, a widely used open source quantum programming SDK. You can run Qiskit code directly on Braket with the Qiskit-Braket provider.

#### [Curated Resources](#)
**Building circuits, tasks, and hybrid jobs**  
For more information about building circuits, tasks, and hybrid jobs on Braket, see the following resources:
- [Anatomy of Quantum Circuits and Quantum Tasks in Amazon Braket(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/getting_started/3_Deep_dive_into_the_anatomy_of_quantum_circuits/3_Deep_dive_into_the_anatomy_of_quantum_circuits.ipynb)
- [Amazon Braket Examples: Deep Dive into the Anatomy of Quantum Circuits(opens in a new tab)](https://github.com/aws/amazon-braket-examples/tree/main/examples/getting_started/3_Deep_dive_into_the_anatomy_of_quantum_circuits)
- [Getting Started with OpenQASM on Braket(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/braket_features/Getting_Started_with_OpenQASM_on_Braket.ipynb)
- [Amazon Braket Examples: Braket Features(opens in a new tab)](https://github.com/aws/amazon-braket-examples/tree/main/examples/braket_features)
- [AWS Open-Sources OQpy to Make It Easier to Write Quantum Programs in OpenQASM 3](https://aws.amazon.com/blogs/quantum-computing/aws-open-sources-oqpy-to-make-it-easier-to-write-quantum-programs-in-openqasm-3/)


**Building with PennyLane**  
For more information about using PennyLane with Braket, see the following resources:
- [Combining PennyLane with Amazon Braket(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/pennylane/0_Getting_started/0_Getting_started.ipynb)
- [Amazon Braket Examples: PennyLane/Getting Started(opens in a new tab)](https://github.com/aws/amazon-braket-examples/tree/main/examples/pennylane/0_Getting_started)
- [Creating a Bridge between Machine Learning and Quantum Computing with PennyLane](https://aws.amazon.com/blogs/opensource/creating-a-bridge-between-machine-learning-and-quantum-computing-with-pennylane/)

**Building with Qiskit**  
For more information about using Qiskit with Braket, see the following resources:
- [How to Run Qiskit on Amazon Braket(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/qiskit/0_Getting_Started.ipynb)[(opens in a new tab)](https://github.com/aws/amazon-braket-examples/tree/main/examples/qiskit)
- [Introducing the Qiskit Provider for Amazon Braket](https://aws.amazon.com/blogs/quantum-computing/introducing-the-qiskit-provider-for-amazon-braket/)

![](https://i.imgur.com/wymBxul.png)


## Running Tasks on Simulators
By the end of the lesson, you will be able to do the following:

- <mark style="background: #FFB86CA6;">Differentiate between local and on-demand simulators based on appropriate use cases and project needs.</mark>

### **Benefits Of Quantum simulators**
Running on quantum hardware can be resource intensive, so it's important to test applications before running on QPUs.  
<mark style="background: #D2B3FFA6;">You can use quantum simulators running on classical computers to debug, fine-tune, and experiment with quantum programs before sending the task or job to the QPU.</mark>

<mark style="background: #ABF7F7A6;">With simulators, you can test your quantum algorithms at a lower cost because you do not need quantum hardware or access to specific quantum machines. </mark>  
<mark style="background: #ADCCFFA6;">Simulation is a convenient way to troubleshoot and optimize algorithms before progressing to run them on quantum hardware.</mark>  
<mark style="background: #ABF7F7A6;">Classical simulation is also essential to verify the results of near-term quantum computing hardware and study the effects of noise.</mark>

><mark style="background: #BBFABBA6;">Braket gives you access to two types of simulators: local and on-demand simulators.</mark>

#### Local Simulators
Local simulators run in your local python environment.

When using simulators, consider the following details:
- <mark style="background: #ADCCFFA6;">The running time and maximum number of qubits the local simulators can process depends on the Braket notebook instance type or on your local hardware specifications.</mark>
    
- <mark style="background: #FFB8EBA6;">The local simulator supports all gates in the Braket SDK, and QPU devices support a smaller subset. </mark>  
  You can find the supported gates of a device through Braket on the AWS Management Console. In the navigation pane on the Braket console page, choose Devices. Here, you can find detailed information about available quantum hardware.
    
- <mark style="background: #FFB8EBA6;">The local simulator supports advanced Open Quantum Assembly Language (OpenQASM) features, which might not be supported on QPU devices or other simulators.</mark> For more information about supported features, see [Simulating Advanced OpenQASM Programs with the Local Simulator(opens in a new tab)](https://github.com/aws/amazon-braket-examples/blob/main/examples/braket_features/Simulating_Advanced_OpenQASM_Programs_with_the_Local_Simulator.ipynb).

There are three local simulators available. To learn more, expand each of the following three categories.  
<mark style="background: #FFB86CA6;">Local state vector simulator</mark>  
	**The local state vector simulator(braket_sv)** is part of the Braket SDK that runs locally in your environment. It is well suited for rapid prototyping on small circuits(up to _25 qubits_), depending on the hardware specification of your Braket notebook instance or your local environment.  
<mark style="background: #FFB86CA6;">Local density matrix simulator</mark>  
	The local density matrix simulator(braket_dm) is part of the Braket SDK that runs locally in your environment. It is well suited for rapid prototyping on small circuits with noise(up to _12 qubits_) depending on the hardware specifications of the your Braket notebook instance or your local environment.  
<mark style="background: #FFB86CA6;">Local Analog Hamiltonian Simulation(AHS) Simulator</mark>  
	The local simulator(braket_ahs) is part of the Braket SDK that runs locally in your environment. It can be used to simulate results from an AHS program. It is well suited for prototyping on small registers( up to 10-12 atoms), depending on the hardware specifications of your Braket notebook instance or your local environment. 

#### On-demand Simulators
<mark style="background: #BBFABBA6;">In addition to the local simulators, Braket includes access to fully managed on-demand simulators. All on-demand simulators automatically scale AWS computing resources to deliver high performance processing of your quantum algorithms. </mark>  
<mark style="background: #D2B3FFA6;">The cost of using the Braket on-demand simulators is based on the duration of each simulation task.</mark>  
<mark style="background: #ABF7F7A6;">When you use on-demand simulators, you are billed at a per-minute rate in increments of 1 millisecond for the time your simulation takes to run.</mark> There is a minimum billing duration of 3 seconds for each simulation.  
<mark style="background: #FFB86CA6;">You can test and validate your circuits. Braket handles all the underlying software components and Amazon EC2 clusters. </mark>This takes away the burden of simulating quantum circuits on classical HPC infrastructure.

There are three on-demand simulators available.
- **State vector simulator(SV1)**  
	SV1 is an on-demand, high performance, universal state vector simulator. It can simulate circuits of up to _34 qubits_. You can expect a 34-qubit dense circuit with depth 34 to take approximately 1–2 hours to complete, depending on the type of gates used and other factors
- **Density matrix simulator(DM1)**  
	DM1 is an on-demand, high performance, density matrix simulator. It can simulate circuits of up to 17 qubits. You can build common noisy circuits from the ground up using gate noise operations, such as bit flip and depolarizing error.
- **Tensor network simulator(TN1)**  
	TN1 is an on-demand, high performance, tensor network simulator. TN1 can simulate certain circuit types with up to _50 qubits_ and a circuit depth of 1,000 or smaller. TN1 is particularly powerful for sparse circuits, circuits with local gates, and other circuits with special structure, such as quantum Fourier transform (QFT) circuits.

![](https://i.imgur.com/uQwo5yo.png)

### **Quantum Noise simulation**
<mark style="background: #D2B3FFA6;">Noise refers to the multiple factors that can affect the accuracy of the calculations that a quantum computer performs.</mark>  
<mark style="background: #ABF7F7A6;">Quantum computers are susceptible to noise from various sources, such as disturbances in Earth’s magnetic field, local radiation from Wi-Fi or mobile phones, and cosmic rays.</mark>  
<mark style="background: #CACFD9A6;">Even the influence that neighboring qubits exert on each other by physical proximity can be a source of noise.</mark>  
The noise generated by any of these sources can cause loss of information in the state of the qubit.

When performing a quantum logic operation, qubits can also suffer from errors that cause them to rotate by the wrong amount. In the case that noise has occurred, the final state of the quantum computer is not precisely the state you might expect. Unless you can reverse the action of the noise, the information in the quantum system can become randomized or totally erased. This phenomenon is known as decoherence.

### **Pure And Mixed Quantum states**
Mixed quantum states are required when you want to describe general physical systems in non-ideal settings. For instance, if the quantum system is subject to noise and decoherence, or if there is entanglement with the outside environment, then mixed states are appropriate. <mark style="background: #D2B3FFA6;">This more general description of quantum states makes use of probability density matrices, often called density matrices,</mark> to describe both pure and mixed quantum states.

### **Building A Noisy Quantum circuit**
In the same way that you can build a noiseless circuit with quantum gates, you can build a noisy quantum circuit from the bottom up. In the following example, you start with the Bell pair preparation circuit that you reviewed previously. You add a noise channel after each gate: a bit flip and a phase flip with probability values of 0.1.

[View code example](#)
```
from braket.circuits import Circuit
circuit =Circuit().h(0).bit_flip(0,0.1).cnot(0,1).phase_flip(0,0.1)
```

You can also use the **apply_gate_noise** method to add noise channels to a circuit. For example, to add noise to every gate in a circuit, you can define it separately and then apply it to the whole circuit.
```
from braket.circuits import Circuit, Noise

circuit = Circuit().h(0).cnot(0,1)

noise =Noise.BitFlip(probability=0.1)

circuit.apply_gate_noise(noise)
```

Finally, it is possible to add noise to a particular gate or a particular qubit individually. The following example uses the keyword arguments **target_qubits** and **target_gates** to apply gate noise to specific targets in the circuit.  
[View code example](#)
```
from braket.circuits import Circuit, Noise, Gate

circuit = Circuit().h(0).cnot(0,1)

noise1 = Noise.BitFlip(probability=0.1)

noise2 = Noise.PhaseFlip(probability=0.2)

circuit.apply_gate_noise(noise1, target_qubits=[1])

circuit.apply_gate_noise(noise2, target_gates=[Gate.H])
```

### **Density Matrix simulators**
Braket provides two density matrix simulators: a <mark style="background: #ABF7F7A6;">local simulator (braket_dm</mark>) that comes with the Braket SDK and an <mark style="background: #ABF7F7A6;">on-demand DM1.</mark>

The local simulator is convenient for fast prototyping, and there is no requirement for you to have access to an AWS account. The local density matrix simulator comes preinstalled with the Braket SDK. You can instantiate it by using the parameter **braket_dm** that is passed when declaring the local simulator.  
[View code example](#)
```
from braket.devices import LocalSimulator

device = LocalSimulator('braket_dm')
```

<mark style="background: #D2B3FFA6;">Using the local simulator has limitations on the circuit depth and size that you can define because they are determined by the available resources on the local machine.</mark> The local simulator can run circuits with noise up to 12 qubits without any concurrency.

<mark style="background: #BBFABBA6;">For larger experiments, a better option is to use the on-demand DM1 simulator.</mark> This is defined using its corresponding Amazon Resource Name (ARN).  
[View code example](#)
```
from braket.aws import AwsDevice

device = AwsDevice("arn:aws:braket:::device/quantum-simulator/amazon/dm1")
```

### **Best Practices for Using Braket**
- <mark style="background: #FFB86CA6;">Verify with simulators</mark>
- <mark style="background: #FFB86CA6;">Restrict user access to certain devices</mark>
- <mark style="background: #FFB86CA6;">Set billing alarms</mark>
- <mark style="background: #FFB86CA6;">Test TN1 tasks with low shot counts</mark>
- <mark style="background: #FFB86CA6;">Check all Regions for tasks</mark>
- <mark style="background: #FFB86CA6;">Use the cost tracking tools</mark>

### **Notebook pricing**
Braket provides fully managed Jupyter notebooks so you can build your quantum algorithms, share code, test your algorithms, and visualize your results. When you create a notebook in Braket, it is hosted and billed by Amazon SageMaker, the AWS ML service.

With Braket managed notebooks, you can choose your preferred instance type to run each notebook. You are billed hourly for usage, according to pricing for the selected instance type. For usage under 1 hour, cost is prorated based on the hourly price. The cost of using each notebook is listed in the SageMaker portion of your bill.

## Running Quantum Tasks on QPUs
By the end of the lesson, you will be able to do the following:

- Examine QPU properties using both the Braket console and the Braket SDK.
- Identify the QPU access paradigms available on Braket.
- Understand the pricing scheme for QPUs, and estimate costs before running tasks on the QPU.
### Quantum Processing Units
<mark style="background: #D2B3FFA6;">Braket provides you with a single access point to different quantum hardware choices, so you can experiment and innovate with multiple QPUs through the same interface. </mark>  
In the past, the lack of access to quantum hardware has been one of the limiting factors as researchers in academia and industry have tried to innovate with quantum computing. This experimentation is crucial to develop quantum algorithms that can address challenging problems in finance, energy, pharmaceuticals, and logistics

<mark style="background: #D2B3FFA6;">In Braket, a QPU is a hardware device that you can call using the API to run quantum tasks. </mark>  
For all QPUs, you can find device properties, such as device topology, calibration data, and gate sets, on the **Devices** tab of the Braket console. You can also find device properties through the **AwsDevice** and **GetDevice** APIs.  
Search for devices with one or more of the following filtering criteria:
- ARNs
- Names
- Types
- Statuses
- Provider names

### Quantum Circuits
There are **three ways** you can specify tasks for quantum devices: <mark style="background: #FFB86CA6;">quantum circuits</mark>, <mark style="background: #ADCCFFA6;">Analog Hamiltonian Simulation (AHS)</mark>, and <mark style="background: #ABF7F7A6;">Braket Pulse.</mark>  
You can seamlessly swap between different devices without any modifications to the circuit definition by redefining the device object. You can run the quantum circuits constructed for use with the local simulator on QPUs by changing the device.

### QPU Pricing
With Braket, you can access quantum computing resources on demand without upfront commitment. You pay only for what you use.  
<mark style="background: #ADCCFFA6;">A task is a sequence of repeated shot based on the same quantum instructions. </mark>  
You define how many shots you want included in a task when you submit the task to Braket.  
There are <mark style="background: #CACFD9A6;">two pricing components when using a quantum computer or QPU on Braket</mark>: <mark style="background: #D2B3FFA6;">a per-shot fee</mark> and <mark style="background: #D2B3FFA6;">a per-task fee.</mark>

![](https://i.imgur.com/QWUjT3w.png)

## Amazon Braket Hybrid Jobs
By the end of the lesson, you will be able to do the following:

- Differentiate between quantum tasks and hybrid jobs.
- Identify algorithms that benefit from Amazon Braket Hybrid Jobs with priority access to QPUs.
- Create a hybrid job using both the Braket console and your local development environment.
- Understand pricing and estimate costs for hybrid jobs.

### What is Amazon Braket Hybrid Jobs?
A hybrid quantum algorithm is one that uses quantum computer as coprocessors alongside classical computers.  
<mark style="background: #D2B3FFA6;">In a sense, all quantum algorithm are hybrid since classical computers are simply more efficient for tasks like preprocessing and postprocessing, loading in data, and other sequential tasks. </mark>

However, when people refer to **hybrid quantum algorithm**, they most commonly mean a specific sub-type. This is one that <mark style="background: #ABF7F7A6;">uses classical computers to improve the performance in iterative algorithms on Noisy Intermediate Scale Quantum(NISQ) hardware. </mark>  
This type of algorithm typically has many rounds of communication back and forth between the quantum and classical hardware.  
Examples of such algorithms include the **Quantum Approximate Optimization Algorithm (QAOA), Variational Quantum Eigensolver (VQE), and quantum machine learning algorithms more broadly.**

This is where Amazon Braket Hybrid Jobs comes in to provide fully managed, containerized, and scalable classical compute resources with pay-as-you-go pricing. Using this orchestration service, it is more efficient to set up, monitor, and scale the classical compute needed in advanced hybrid algorithms on QPUs or quantum simulators.

Additionally, <mark style="background: #ABF7F7A6;">quantum tasks created from a hybrid job get higher priority in the queue on your chosen QPU.</mark> This ensures that quantum tasks are processed and run ahead of others in the queue. With Amazon Braket Hybrid Jobs, you also have a checkpoints feature, so you can pick up where you left off in case your job gets interrupted.

### Using Amazon Braket Hybrid Jobs
Braket provides individual, standalone quantum tasks for asynchronous processing of quantum programs on QPUs or simulators. For algorithms that require many sequential calls to a QPU, such as variational quantum algorithms and quantum optimization tasks, Braket recommends Amazon Braket Hybrid Jobs.  
<mark style="background: #D2B3FFA6;">As a fully managed, containerized environment, you can run experiments combining classical and quantum computations with priority queueing for quantum tasks.</mark>

You can run entire hybrid quantum-classical algorithms asynchronously with near real-time monitoring.  
<mark style="background: #FFB86CA6;">Amazon Braket Hybrid Jobs is designed to spin up the requested classical resources when your target quantum device is available. It then runs your algorithm and releases the instances after completion, so you pay only for what you use.</mark> <mark style="background: #ABF7F7A6;">Only a single hybrid job will run on a QPU at any given time.  
</mark>
### Braket Algorithm Library
 <mark style="background: #ADCCFFA6;">The Amazon Braket Algorithm Library provides researchers with ready-to-use Python implementations for a set of quantum algorithms on Braket</mark>.  
  You can run these algorithms to get started with developing your own code on Braket by referencing the ready-to-use examples. You can use them as they are or as a starting point to build more complex algorithms. The Braket Algorithm Library is open source, and community contributions are accepted to help it grow.

The Braket console provides a description of each available algorithm in the Braket Algorithm Library.

### Building Hybrid Jobs with PennyLane
<mark style="background: #D2B3FFA6;">Braket provides support for PennyLane, so you can train quantum circuits in the same way that you would train a neural network.</mark>  
PennyLane is a library for optimization and automatic differentiation of hybrid quantum-classical computation. The library includes solutions for computational problems in quantum chemistry, quantum machine learning, and optimization. The PennyLane library provides interfaces to familiar ML tools, including PyTorch and TensorFlow.

PennyLane is preinstalled on Braket notebooks. For access to Braket devices from PennyLane, open a notebook and import the PennyLane library by using the following command.

```
import pennylane as qml
```

### Hybrid Jobs Pricing
There are two components to pricing for the Amazon Braket Hybrid Jobs feature: <mark style="background: #D2B3FFA6;">the use of classical resources and the use of quantum computers or on-demand simulators.</mark>  
You can choose the classical compute instance type when creating a job.  
Additionally, you can use multi-instance computing for distributed workloads or specialized compute, such as graphics processing unit (GPU) instances.


## Overview of Braket Pulse
**Unlike <mark style="background: #FFB86CA6;">quantum gates</mark> that abstract away several concepts of quantum physics, <mark style="background: #FFB86CA6;">pulse-level control</mark> requires a deeper knowledge of interacting with quantum systems in general and hardware design specifically.**  
<mark style="background: #BBFABBA6;">To program at this lower level, you need a new programming interface to help manipulate the physical parameters of qubits and driving fields such as frequencies and amplitudes. </mark>  
<mark style="background: #D2B3FFA6;">Braket Pulse implements this new interface and is based on OpenPulse, the grammar extension of the OpenQASM 3 specification.</mark>

You first need to be familiar with some of the new concepts at the core of Braket Pulse.  
When programming at the pulse level, you generate signals that are transiting using different channels, also called ports, of the devices. Braket Pulse introduces the class Port as a software abstraction for physical QPU ports.

Frames are bound to ports. They are software abstractions representing physical frames of reference of the carrier signals. They serve as support for scheduling waveforms. A waveform is a time-dependent envelope that can be used to emit signals on an output port or receive signals from an input port. With Braket, you can instantiate predefined frames to prototype pulse.

You can construct low-level programs using a PulseSequence, which holds a chronologically ordered sequence of pulse instructions. PulseSequence is fully integrated with the rest of the Braket SDK. For instance, you can submit them as standalone programs or as part of your circuits using the pulse_gate circuit instructions to test timings for a precise quantum evolution. You can also use them as the base object to create new gates or replace existing ones without modifying your circuits.

<mark style="background: #ADCCFFA6;">Braket Pulse is a part of the Braket SDK you can use to construct pulse sequences using the PulseSequence class.</mark>  
<mark style="background: #FFB86CA6;">PulseSequence</mark> shares many similarities with Circuit.  
<mark style="background: #083CA4A6;"> Both define a recording of the list of chronologically ordered quantum instructions and can be run with the device.run() function. </mark>

<mark style="background: #ADCCFFA6;">PulseSequence exposes a user interface to schedule waveforms on arbitrary frames. It includes functions for scheduling these time-dependent signals such as play, delay, or barrier and also as frame-modifier functions to adapt the phase and the frequency of the carrier signal.</mark>

<mark style="background: #ABF7F7A6;">A PulseSequence can be submitted as standalone program or be incorporated in your circuit</mark> using two mechanisms.  
The first one is the<mark style="background: #FFB86CA6;"> pulse_gate</mark>, which inserts pulse instructions directly into your circuit.  
The second one is the <mark style="background: #FFB86CA6;">ability to replace the default implementation of an arbitrary gate</mark> by your own pulse sequence. The following snippet demonstrates how to use both these methods.


## How to Create Analog Hamiltonian Simulation Programs
### What is AHS?
<mark style="background: #D2B3FFA6;">Analog Hamiltonian Simulation (AHS) is a paradigm of quantum computing, which refers to the ability to encode a problem of interest into a mathematical object known as the Hamiltonian.</mark>  
<mark style="background: #ADCCFFA6;">The Hamiltonian represents the energy levels of a quantum system, such as interacting atoms on a lattice. </mark>  
<mark style="background: #FFB86CA6;">The computer is then tuned so it directly simulates the continuous time evolution of the quantum system under that Hamiltonian.</mark>

<mark style="background: #D2B3FFA6;">QuEra Aquila</mark> is the first device available on Braket that follows the principles of this paradigm.  
<mark style="background: #D2B3FFA6;">It is a special purpose device, trading off the ability to perform universal or gate-based computation for the ability to efficiently solve specific tasks.</mark>

<mark style="background: #ABF7F7A6;">This device operates by trapping atoms with lasers, arranging them in programmable one-dimensional or two-dimensional layouts, called quantum registers</mark> in this paradigm, and inducing interatomic interactions through van der Waals forces.  
Furthermore, you can dynamically tune driving field parameters, thus controlling qubit states and their interactions.  
In the next section, you will learn how to create and run an AHS program with Braket.

### Creating an AHS Program
You can create a program for AHS in two steps, as follows:
1. **Specify the quantum register**- Define atom positions, fixing the processor qubit layout and connectivity. 
2. **Specify the quantum evolution**- Determine the time series of the atomic drive parameters. This is similar to deciding the quantum gates of digital machines, prescribing a particular algorithm.


## Additional Advanced Topics
### Error Mitigation on IonQ
With IonQ Aria QPU, customers can take advantage of 25 qubits, higher fidelities, and error mitigation (EM), making it possible to run more complex quantum algorithms with improved accuracy.

Aria is the first QPU on Braket to feature EM techniques that are designed to improve the accuracy of current-generation noisy quantum hardware. EM, an active area of research, is crucial to make the most out of near-term quantum hardware. EM uses classical post-processing to extract the best signal from noisy measurements from a quantum computer. With Aria, customers can experiment with EM techniques and, by toggling them on or off, study the impact they have on algorithm performance.

IonQ Aria offers two forms of error mitigation: _debiasing_ and _sharpening_. Debiasing is suitable for all circuits. However, sharpening assumes the form of the output distribution to be sparse, with few high-probability states and many zero-probability states. It might distort the probability distribution if this assumption is not valid. In Braket, debiasing and sharpening both require a minimum of 2,500 shots. Any result types specified in the circuit, such as expectation values, are computed using debiasing.

For more information about error mitigation, see each of the following resources:

- [Exploring Quantum Error Mitigation with Mitiq and Amazon Braket(opens in a new tab)](https://aws.amazon.com/blogs/quantum-computing/exploring-quantum-error-mitigation-with-mitiq-and-amazon-braket/)
- [Amazon Braket Launches IonQ Aria with Built-in Error Mitigation(opens in a new tab)](https://aws.amazon.com/blogs/quantum-computing/amazon-braket-launches-ionq-aria-with-built-in-error-mitigation/)
- [Error Mitigation on Amazon Braket](https://github.com/aws/amazon-braket-examples/blob/main/examples/braket_features/Error_Mitigation_on_Amazon_Braket.ipynb)

## **Perform Quantum simulations**

<mark style="background: #D2B3FFA6;">One of the earliest driving ideas behind quantum computing was the idea of simulating physical systems, and you can use Braket for this purpose. Many AWS customers and AWS Partners have designed resources to help you get started with quantum simulation in various contexts.</mark>


# Badge Assessment

The pricing components for your Hybrid Job using the SV1 on-demand state-vector simulator are:

1. **The simulation time of your SV1 tasks, provided you have exceeded the AWS Free Tier:**
   - The duration for which your SV1 tasks run contributes to the overall cost. This is based on the simulation time.

2. **The hybrid job instance (i.e., the classical host) that runs your code:**
   - The classical host, which runs your hybrid quantum-classical code, incurs costs. The type and specifications of the classical host influence the pricing.

3. **The number of shots for each task:**
   - The number of shots, or the number of times the quantum circuit is executed, affects the cost. Higher shot counts generally result in longer simulation times and, consequently, higher costs.

Explanation:

- **The choice of container image:**
   - While the container image choice may impact the functionality and performance of your hybrid job, it doesn't directly contribute to the cost in the context of the provided options.

- **The AWS region in which your Hybrid Job is run:**
   - While the region can influence the cost structure, it is not directly a component of the cost; it primarily affects data transfer costs and other regional considerations.

- **The duration of your Hybrid Job:**
   - The overall duration of your hybrid job is indeed a factor, but it is more specifically captured by the simulation time of your SV1 tasks and the classical host's runtime.

---
The best option to compare the Analog Hamiltonian Simulation (AHS) program results from the noisy QPU to noiseless simulation is:

Run AHS program on local braket_ahs simulator.

The braket_ahs simulator provides an implementation of noiseless AHS to classically benchmark quantum AHS program performance. By taking the 12-atom AHS program run on the QPU and executing it locally using the braket_ahs simulator, you can generate ideal noiseless results for comparison.

Running on the DM1 or SV1 simulators would introduce additional noise rather than provide a noiseless reference. Scaling down the atom count would fail to simulate the full target system. And managed AHS resources are not offered.

So running locally with braket_ahs gives you the most direct noiseless simulation to benchmark against the noisy QPU outputs for the 12-atom AHS workflow. This allows evaluating the effects of noise on your quantum program.

---
The best way to identify which AWS Region to create your Amazon Braket Hybrid Job against a specific QPU is to:

Navigate to the Devices page in the Braket Management Console, click your desired QPU, and observe the Region in the Details tab.

The Devices page in the Braket console provides a centralized view of all available QPUs. Selecting a specific QPU shows details like the provider, location, and importantly the AWS Region the device is associated with.

---
The most appropriate Braket feature for gaining a deeper level of control over the QPU and its qubits is Braket Pulse.

Braket Pulse provides low-level control of a quantum processor by letting you specify control pulses that target individual qubits and control electronics on the device. This gives direct programming access to the quantum hardware.

In comparison:

- Hybrid Jobs: Allow running algorithms across simulated and quantum resources but do not provide pulse-level control.

- PennyLane: Focused more on quantum machine learning rather than pulse-level control of a QPU.

- Quantum circuits: Enable defining algorithms with quantum gates but operate at a higher, gate-based level without pulse control.

Because the developer wants to build up physical control signals targeting elementary QPU components, Braket Pulse is the right fit. It delivers the capability to program the qubit control electronics directly with fine-grained pulse specifications. This supports creating custom control flows tailored to the QPU hardware at the most fundamental level.

So for the goal of programming QPUs directly for maximum control and visibility, Braket Pulse is the most appropriate feature.

---
The SV1 (State Vector) simulator specifically simulates the noise properties and error rates of different quantum hardware to provide realistic noisy simulations. This allows testing and evaluating quantum algorithms under real-world noisy conditions to analyze the impacts and develop error mitigation techniques.

In comparison:

- Local state vector simulator: Provides ideal, noiseless state vector simulations without hardware error modeling.
- TN1 simulator: A tensor network simulator focused on high performance rather than noise modeling.
- DM1 simulator: Density matrix simulator not optimized for simulating noisy environments.

---
The best way to track progression on your quantum algorithm using Amazon Braket Hybrid Jobs in near-real time is through Custom Metrics.

Amazon Braket Hybrid Jobs allow you to run quantum algorithms across a combination of simulated and quantum hardware resources. Custom Metrics give you the ability to define events and properties to track within your algorithm implementation. As your algorithm runs, you can visualize these custom metrics in near-real time to understand the current status and progression.

For example, you could add custom metrics to track key milestones in your algorithm like the completion of different subroutines or loops. Or track metrics like fidelity values at various points to monitor quality and performance. The Amazon Braket console provides a visualization and tracking tool for custom metrics in near-real time.

While Jupyter Notebooks allow you to interact with Braket and visualize results, they do not provide tracking capacbilities for currently running jobs. Simulators can help test algorithms, but also do not give visibility into live jobs. And the Braket Python SDK enables defining and executing quantum algorithms, but does not offer custom metric tracking of running hybrid jobs.

---
The simulators best fitted for profiling the number of shots to set when running a small quantum circuit on Rigetti Aspen M-3 are:

1. **Local density matrix simulator (TN1)**
   - Local density matrix simulators are well-suited for analyzing quantum circuits and profiling shot counts, as they provide information about the full density matrix, allowing for a comprehensive understanding of the quantum state.

2. **Local state vector simulator (SV1)**
   - Local state vector simulators are also suitable for profiling shot counts, especially for small quantum circuits. They simulate the quantum state vector, offering insights into the state evolution and enabling accurate assessment of shot requirements.

Explanation:
- **Rigetti Aspen M-3:**
   - The Rigetti Aspen M-3 is a real quantum processor, not a simulator. Therefore, it's not directly involved in the profiling of shot counts. Profiling is typically done using simulators to understand the impact of finite sampling on the accuracy of results.

- **Local density matrix simulator (TN1):**
   - Density matrix simulators provide a more complete characterization of the quantum state compared to state vector simulators. This is crucial for accurately profiling shot counts, especially when finite sampling effects need to be considered.

- **Local state vector simulator (SV1):**
   - State vector simulators can also be suitable for profiling shot counts, particularly for small circuits. They simulate the quantum state directly as a vector, offering insights into the evolution of the state during the simulation.

---
For efficiently creating and testing a quantum algorithm before considering physical quantum hardware, the most advantageous component of Amazon Braket for your team would be:

**Local quantum simulators**

Explanation:

- **Integration with advanced AI algorithms:**
  - While Amazon Braket provides various capabilities, including integration with AI algorithms, this is not the primary focus for creating and testing quantum algorithms.

- **Quantum hardware access:**
  - Access to quantum hardware is essential for running algorithms on actual quantum processors. However, for algorithm development and testing, it's often more practical and faster to use simulators before transitioning to physical hardware.

- **Integration with AWS services:**
  - While integration with AWS services is beneficial for broader computational and data management needs, it doesn't specifically address the initial stages of quantum algorithm development and testing.

- **Local quantum simulators:**
  - Local quantum simulators are crucial for efficient algorithm development and testing. They allow you to simulate quantum circuits on classical machines, providing a faster feedback loop and avoiding the constraints of physical hardware access. This is particularly valuable in the early stages of algorithm refinement.

---
- **The local AHS simulator:**
    - The local AHS simulator is a simulator that runs on your local machine, allowing you to simulate the quantum circuit without using remote quantum devices.
- **QPUs relying on the gate-based models like the IonQ devices:**
    - IonQ devices use a gate-based model, and Amazon Braket supports running quantum tasks on these devices.
- **QPUs relying on the gate-based model like the QuEra device:**
    - The QuEra device, which also relies on a gate-based model, is compatible with Amazon Braket for running quantum tasks.

---
