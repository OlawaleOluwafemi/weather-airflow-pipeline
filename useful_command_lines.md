# Git
git status
git add .
git commit -m "message"
git push -u origin main
git config --global user.email "olawaleoluwafemi90@gmail.com"
git config --global user.name "OlawaleOluwafemi"
git remote add origin https://github.com/your-username/weather-airflow-pipeline.git ----> this is used to link your github repo
#Pull the remote changes from GitHub and rebase your local commits on top of them: git pull origin main --rebase

# Python
# setting up a venv environment 
    python3 -m venv venv
    source venv/bin/activate
    deactivate
    sudo apt update
    sudo apt install python3-pip python3-venv -y
    pip install requests psycopg2-binary apache-airflow

# Docker
docker-compose up --build -d    This is used to start your infrastructure.
docker-compose up -d
docker-compose down -v
docker logs (put the container name here without the bracket)
#Clear out any dead volume locks: docker compose rm -f

# Install or Use a Proper WSL Distribution
Step 1: Open your Windows Terminal, PowerShell, or Command Prompt.
    wsl --install
    wsl -l -v

Step 2: Configure Docker Desktop to Integration with Your Distro
    To make Docker containers accessible from your actual development distro, you need to turn on integration.
    Open the Docker Desktop application on Windows.Click the Gear Icon (Settings) in the top right corner.
    Navigate to Resources, WSL integration.Toggle the switch to enable integration for your specific distribution (e.g., Ubuntu).
    Click Apply & restart.

Step 3: Connect VS Code to the Correct Distro
    Now that your development distro is ready and linked to Docker, connect VS Code to that instance instead of the Docker internal backend.
    Open VS Code.
    Press Ctrl + Shift + P to open the Command Palette.
    Type and select WSL: Connect to WSL using Distro...
    Select Ubuntu (or your specific Linux distro) from the list—do not choose docker-desktop.

# Install Airbyte
    # Move into the airbyte folder allocation
    cd airbyte
    # Pull down the official deployment launcher scripts
    curl -L https://maps.airbyte.com/launch-airbyte.sh | bash -s -- --with-logging
    # Once the installer finishes running, you can boot your local instance right away with this command:
    abctl local install --low-resource-mode

# PostgresDB
    # Verify the database directly
    docker exec -it postgres-1 psql -U olawale -d source_data -c "SELECT * FROM weather LIMIT 5;"

