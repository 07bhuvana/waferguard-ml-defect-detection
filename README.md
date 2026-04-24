# 🔬 Real-Time Wafer Defect Detection — ML + Hadoop Analytics System

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python" />
  <img src="https://img.shields.io/badge/Scikit--Learn-RandomForest-orange?style=for-the-badge&logo=scikit-learn" />
  <img src="https://img.shields.io/badge/Streamlit-Dashboard-red?style=for-the-badge&logo=streamlit" />
  <img src="https://img.shields.io/badge/Apache-Hadoop-yellow?style=for-the-badge&logo=apachehadoop" />
  <img src="https://img.shields.io/badge/Domain-Semiconductor%20Manufacturing-blueviolet?style=for-the-badge" />
</p>

> A **real-time wafer defect detection and classification system** for semiconductor manufacturing — powered by a Random Forest classifier, live data simulation, and an interactive Streamlit dashboard.
> This README also includes a **complete Hadoop installation guide** for future Big Data integration.

---

## 🖼️ Screenshots


| Streamlit Dashboard | Wafer Heatmap |
<img width="1600" height="764" alt="WhatsApp Image 2026-04-24 at 12 22 20 PM" src="https://github.com/user-attachments/assets/1d9933d3-18e2-4226-abe2-6db3b37b395f" />
<img width="1600" height="651" alt="WhatsApp Image 2026-04-24 at 12 22 55 PM" src="https://github.com/user-attachments/assets/21c5a736-d24b-4f13-a91e-88493bd32cd2" />


| Defect Trend Chart | Live Alert Panel |
<img width="715" height="640" alt="WhatsApp Image 2026-04-24 at 12 22 57 PM" src="https://github.com/user-attachments/assets/06c9f211-5ac2-4a69-b823-dbf6affb23b9" />


---

## 🧩 Defect Classes Detected

| Class | Description |
|---|---|
| 🔴 Center | Defects concentrated at the wafer center |
| 🟠 Edge-Ring | Ring-shaped defects along the wafer edge |
| 🟡 Scratch | Linear scratches across the wafer surface |
| 🟣 Random | Scattered, non-patterned defects |
| 🟢 None | No defect detected |

---

## 📁 Current Project Structure

> ⚠️ **Note:** Currently this project contains only the core Python ML file.
> Hadoop, Spark, and pipeline files are planned for future integration (see Roadmap).

```bash
wafer-defect-detection/
│
├── app.py               # ✅ Main Python file — ML + Streamlit Dashboard
├── requirements.txt     # ✅ Python dependencies
└── README.md            # ✅ This file
```

### Planned Structure (After Full Integration)
```bash
wafer-defect-detection/
│
├── app.py                        # Streamlit dashboard
├── train_model.py                # Model training script
├── realtime_prediction.py        # Real-time simulation
├── preprocessing.py              # Data preprocessing
├── wafer_dataset.csv             # Dataset
├── rf_model.pkl                  # Saved model
├── hadoop/
│   ├── mapper.py                 # Hadoop MapReduce mapper
│   ├── reducer.py                # Hadoop MapReduce reducer
│   └── hdfs_upload.sh            # HDFS data upload script
├── spark/
│   └── spark_streaming.py        # Spark Streaming integration
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started — Python Setup

### Step 1 — Clone the Repository

```bash
git clone https://github.com/yourusername/real-time-wafer-defect-detection-ml.git
cd real-time-wafer-defect-detection-ml
```

### Step 2 — Create Virtual Environment _(Recommended)_

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux / Mac
python3 -m venv venv
source venv/bin/activate
```

### Step 3 — Install Dependencies

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install streamlit pandas numpy scikit-learn matplotlib seaborn opencv-python joblib
```

### Step 4 — Run the Application

```bash
streamlit run app.py
```

Open in browser → `http://localhost:8501`

---

## 📊 Sample Prediction Output

```text
Incoming Wafer  : #1042
Predicted Defect: Edge-Ring
Confidence      : 96.4%
Alert           : ⚠️  Defect Detected
```

---

## 🤖 ML Model Details

**Algorithm:** Random Forest Classifier

| Property | Detail |
|---|---|
| Model Type | Ensemble — Random Forest |
| Input | Wafer map feature array |
| Output | Defect class + confidence score |
| Saved As | `rf_model.pkl` via Joblib |

**Why Random Forest?**
- High accuracy on imbalanced defect pattern data
- Robust against industrial sensor noise
- Fast real-time inference
- No feature scaling required

---

## 🛠️ Tech Stack

| Layer | Tools |
|---|---|
| Language | Python 3.x |
| ML Model | Scikit-learn (Random Forest), Joblib |
| Data Handling | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn, OpenCV |
| Dashboard | Streamlit |
| Big Data (Planned) | Apache Hadoop, Apache Spark |

---

---

# 🐘 Hadoop Installation Guide
### _(For Future Big Data Integration)_

> This section provides a complete step-by-step Hadoop installation on **Ubuntu/Linux**.
> Follow this when you are ready to scale the project with HDFS storage and MapReduce processing.

---

## Prerequisites

Before installing Hadoop, make sure you have:

| Requirement | Check Command |
|---|---|
| Ubuntu 20.04 / 22.04 | `lsb_release -a` |
| Java 8 or 11 | `java -version` |
| SSH installed | `ssh -V` |
| At least 4GB RAM | `free -h` |
| At least 20GB disk | `df -h` |

---

## Phase 1 — Install Java

Hadoop requires Java. Install OpenJDK 11:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```

Verify installation:

```bash
java -version
```

Expected output:
```text
openjdk version "11.x.x"
```

Set JAVA_HOME environment variable:

```bash
echo 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64' >> ~/.bashrc
echo 'export PATH=$PATH:$JAVA_HOME/bin' >> ~/.bashrc
source ~/.bashrc
```

Verify:

```bash
echo $JAVA_HOME
```

---

## Phase 2 — Configure SSH (Passwordless Login)

Hadoop nodes communicate via SSH. Set up passwordless SSH:

```bash
sudo apt install openssh-server openssh-client -y
```

Generate SSH key pair:

```bash
ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa
```

Add public key to authorized keys:

```bash
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

Test SSH localhost login (should NOT ask for password):

```bash
ssh localhost
```

If it connects without a password prompt — ✅ SSH is configured correctly.

Type `exit` to return to your normal terminal.

---

## Phase 3 — Download and Install Hadoop

Download Hadoop 3.3.6 (stable release):

```bash
cd /opt
sudo wget https://downloads.apache.org/hadoop/common/hadoop-3.3.6/hadoop-3.3.6.tar.gz
```

Extract the archive:

```bash
sudo tar -xvzf hadoop-3.3.6.tar.gz
sudo mv hadoop-3.3.6 hadoop
sudo chown -R $USER:$USER /opt/hadoop
```

---

## Phase 4 — Set Hadoop Environment Variables

Open your `.bashrc` file:

```bash
nano ~/.bashrc
```

Add the following lines at the bottom:

```bash
# Hadoop Environment Variables
export HADOOP_HOME=/opt/hadoop
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
```

Save and apply:

```bash
source ~/.bashrc
```

Verify Hadoop is accessible:

```bash
hadoop version
```

Expected output:
```text
Hadoop 3.3.6
```

---

## Phase 5 — Configure Hadoop Files

Navigate to Hadoop config directory:

```bash
cd /opt/hadoop/etc/hadoop
```

### 5a — Edit `hadoop-env.sh`

```bash
nano hadoop-env.sh
```

Find the line `# export JAVA_HOME=` and replace it with:

```bash
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

Save and exit.

---

### 5b — Edit `core-site.xml`

```bash
nano core-site.xml
```

Replace the contents between `<configuration>` tags with:

```xml
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/opt/hadoop/tmp</value>
  </property>
</configuration>
```

Create the tmp directory:

```bash
mkdir -p /opt/hadoop/tmp
```

---

### 5c — Edit `hdfs-site.xml`

```bash
nano hdfs-site.xml
```

Replace the contents between `<configuration>` tags with:

```xml
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
  <property>
    <name>dfs.namenode.name.dir</name>
    <value>/opt/hadoop/hdfs/namenode</value>
  </property>
  <property>
    <name>dfs.datanode.data.dir</name>
    <value>/opt/hadoop/hdfs/datanode</value>
  </property>
</configuration>
```

Create the HDFS directories:

```bash
mkdir -p /opt/hadoop/hdfs/namenode
mkdir -p /opt/hadoop/hdfs/datanode
```

---

### 5d — Edit `mapred-site.xml`

```bash
nano mapred-site.xml
```

Replace the contents between `<configuration>` tags with:

```xml
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
  <property>
    <name>mapreduce.application.classpath</name>
    <value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
  </property>
</configuration>
```

---

### 5e — Edit `yarn-site.xml`

```bash
nano yarn-site.xml
```

Replace the contents between `<configuration>` tags with:

```xml
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.env-whitelist</name>
    <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
  </property>
</configuration>
```

---

## Phase 6 — Format the NameNode

> ⚠️ Do this only once during the first setup. Formatting again will erase all HDFS data.

```bash
hdfs namenode -format
```

Expected output at the end:
```text
Storage directory /opt/hadoop/hdfs/namenode has been successfully formatted.
```

---

## Phase 7 — Start Hadoop Services

Start HDFS (NameNode + DataNode):

```bash
start-dfs.sh
```

Start YARN (ResourceManager + NodeManager):

```bash
start-yarn.sh
```

Verify all services are running:

```bash
jps
```

Expected output:
```text
NameNode
DataNode
ResourceManager
NodeManager
SecondaryNameNode
Jps
```

If all 5 Hadoop processes appear — ✅ Hadoop is running successfully.

---

## Phase 8 — Access Hadoop Web UIs

| Service | URL |
|---|---|
| HDFS NameNode UI | http://localhost:9870 |
| YARN ResourceManager UI | http://localhost:8088 |

Open these in your browser to monitor your Hadoop cluster.

---

## Phase 9 — Test HDFS with Wafer Data

Create a directory in HDFS for wafer data:

```bash
hdfs dfs -mkdir -p /wafer/input
```

Upload your dataset to HDFS:

```bash
hdfs dfs -put /path/to/wafer_dataset.csv /wafer/input/
```

List files in HDFS:

```bash
hdfs dfs -ls /wafer/input/
```

Read a file from HDFS:

```bash
hdfs dfs -cat /wafer/input/wafer_dataset.csv
```

---

## Phase 10 — Stop Hadoop Services

When done, stop all services cleanly:

```bash
stop-yarn.sh
stop-dfs.sh
```

Verify all processes stopped:

```bash
jps
```

Only `Jps` should remain.

---

## ⚠️ Common Errors & Fixes

| Error | Cause | Fix |
|---|---|---|
| `Connection refused` on SSH | SSH not running | `sudo service ssh start` |
| `JAVA_HOME not set` | Env variable missing | Re-run `source ~/.bashrc` |
| NameNode not starting | Previous format corrupted | Delete `/opt/hadoop/hdfs/namenode/*` and reformat |
| DataNode not in `jps` | Port conflict | Check logs: `cat /opt/hadoop/logs/*.log` |
| Permission denied on HDFS | Wrong ownership | `sudo chown -R $USER /opt/hadoop` |

---

## 🗺️ Roadmap

- [x] Random Forest ML classifier
- [x] Real-time Streamlit dashboard
- [ ] Integrate wafer dataset with HDFS storage
- [ ] MapReduce job for batch defect analytics
- [ ] Apache Spark Streaming for real-time pipeline
- [ ] CNN deep learning classifier
- [ ] Predictive maintenance module
- [ ] Distributed defect analytics dashboard

---

## 👩‍💻 Author

Developed as a semiconductor defect analytics project combining **Big Data concepts** and **Machine Learning** for real-world manufacturing intelligence.

---

<p align="center">
  <sub>Built for faster, smarter, and scalable wafer inspection. 🏭</sub>
</p>
