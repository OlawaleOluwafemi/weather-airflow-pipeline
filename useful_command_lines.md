# Git
- git init     ---->  Initialize the local repository
- git add .    ------>   Stage all your pipeline code
- git status   ------>  Check the status to ensure no massive data/volume folders are being tracked
- git commit -m "message"  ---->  Create your baseline architecture commit
- git branch -M main ----> Rename the local branch to 'main'
- git remote add origin https://github.com/your-username/your-project-directory.git ----> this is used to link your github repo
- git push -u origin main ---->  Push your code live!
- git config --global user.email "example@gmail.com"
- git config --global user.name "example"
- git pull origin main --rebase   ---->  Pull the remote changes from GitHub and rebase your local commits on top of them
- git pull origin main --allow-unrelated-histories
- git rm filename.txt  ----> to remove a file or text from github

# Python
# setting up a venv environment 
    python3 -m venv venv
    source venv/bin/activate
    deactivate
    sudo apt update
    sudo apt install python3-pip python3-venv -y
    pip install requests psycopg2-binary apache-airflow
    add the below code in your python script if you want to force wsl to read from your .env
    from dotenv import load_dotenv
    load_dotenv()

# Docker
- docker-compose up --build -d    This is used to start your infrastructure.
- docker-compose up -d
- docker-compose down -v
- docker logs (put the container name here without the bracket)
- docker-compose logs -f  ---->  All services 
- #Clear out any dead volume locks: docker compose rm -f

# Install or Use a Proper WSL Distribution
Step 1: Open your Windows Terminal, PowerShell, or Command Prompt.
- wsl --install
- wsl -l -v

Step 2: Configure Docker Desktop to Integration with Your Distro
- To make Docker containers accessible from your actual development distro, you need to turn on integration.
- Open the Docker Desktop application on Windows.Click the Gear Icon (Settings) in the top right corner.
- Navigate to Resources, WSL integration.Toggle the switch to enable integration for your specific distribution (e.g., Ubuntu).
- Click Apply & restart.

Step 3: Connect VS Code to the Correct Distro
- Now that your development distro is ready and linked to Docker, connect VS Code to that instance instead of the Docker internal backend.
- Open VS Code.
- Press Ctrl + Shift + P to open the Command Palette.
- Type and select WSL: Connect to WSL using Distro...
- Select Ubuntu (or your specific Linux distro) from the list—do not choose docker-desktop.

# Install Airbyte
- Move into the airbyte folder allocation
- cd airbyte
- Pull down the official deployment launcher scripts
- curl -LsfS https://get.airbyte.com | bash -
- Once the installer finishes running, you can boot your local instance right away with this command:
- abctl local install --low-resource-mode
- abctl local credentials
- 1. To Shut It Down (When you are done working)
- abctl local shutdown
- 2. To Start It Back Up (When you want to resume)
- abctl local install --low-resource-mode

# PostgresDB
- Verify the database directly
- docker exec -it postgres-1 psql -U olawale -d source_data -c "SELECT * FROM weather LIMIT 5;"

# ClickHouse
- ClickHouse network connection string:
- clickhouse://analytics:clickhouse123@clickhouse:8123/gold_analytics

# DBT
- First, make sure you are in your active virtual environment ((venv)) in your WSL terminal. If it’s not active, turn it on using source venv/bin/activate.
- We are going to start with 
- Step 1: Installing and Initializing dbt for ClickHouse.
  - 1. Install the dbt ClickHouse Adapter. 
     - Inside your terminal, we need to install dbt-core along with the specific adapter that allows dbt to talk to ClickHouse. Run this command:
     - pip install dbt-clickhouse
  - 2. Initialize the dbt Project Structure
     - Now, we will use dbt's built-in initializer to scaffold your directory structure automatically. Run this command inside your main retail-analytics-pipeline directory:
     - dbt init transform_dbt (But because i have already created the folder manually i dont need to run this command.)
  - 3. Configure dbt_project.yml and profiles.yml
  - 4. Test the Connection 
      - Once you save both dbt_project.yml and profiles.yml, change into your dbt project directory in your terminal and run a connection test:
      - cd ~/Data-Engineering-Projects/retail-analytics-pipeline/transform_dbt/
      - dbt debug
      - Note: If it returns error. It means the current python version doesn't support dbt so you will need to remove the venv and reinstall a stable python version e.g python3.12
  - 5. Once that is done, reinstall your pipeline packages.
      - # 1. Install the database drivers and generator packages
      - pip install psycopg2-binary faker

      - # 2. Install the dbt ClickHouse adapter (which also installs dbt-core safely)
      - pip install dbt-clickhouse
  - 6. Run the Test Again!
      - cd transform_dbt
      - dbt debug

- # Crucial step if i don't want to hardcode my clickhouse credentials in my profiles.yml file: 
- Before running dbt, you must load your .env variables directly into your current terminal session memory so dbt can find them. Run this command in your terminal first:
- export $(xargs < ~/Data-Engineering-Projects/retail-analytics-pipeline/.env)
- Thn after that is done, cd transform_dbt
- dbt debug.

    - # Now, we are ready for Step 2: Building Your Transformation Models.
    - We are going to build a clean Staging Model (to parse and clean the messy raw data Airbyte landed) and a Gold Aggregation Model (to calculate business metrics for your dashboard).

    - # Phase A: Define Your Data Source
    - Before dbt can transform data, we need to tell it exactly where Airbyte dropped the raw tables.
    - Look inside your transform_dbt/models/staging/ folder.
    - Create a new file there named schema.yml.

# Superset
- # 1. Pull down the old broken state and start fresh
- docker compose down
- docker compose up -d superset

- # 2. Run the initialization commands directly on the running container
- docker exec -it superset-viz superset fab create-admin --username admin --firstname Superset --lastname Admin --email admin@gold.com --password admin123

- docker exec -it superset-viz superset db upgrade

- docker exec -it superset-viz superset init