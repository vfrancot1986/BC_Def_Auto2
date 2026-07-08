# BC_Def_Auto2
Desafio de Automação - 02
Projeto local calvo em: "C:/projects/BC_Def_Auto2"

# Instalar o postman:
https://www.postman.com/downloads/

# Instalar o CLI do postman:

https://learning.postman.com/docs/postman-cli/postman-cli-installation/

# Executar o runner (Windows) CMD:

postman collection run "C:/projects/BC_Def_Auto2/postman/collections/Col_BC_Def_Auto2" -e "C:/projects/BC_Def_Auto2/postman/environments/Dev.environment.yaml"

# Configurar a pipeline do Github Actions no Windows:
name: Automated API tests using Postman CLI

on: push

jobs:
  automated-api-tests:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Postman CLI
        run: |
          powershell.exe -NoProfile -InputFormat None -ExecutionPolicy AllSigned -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://dl-cli.pstmn.io/install/win64.ps1'))"
      - name: Login to Postman CLI
        run: postman login --with-api-key ${{ secrets.POSTMAN_API_KEY }}
      - name: Run API tests
        run: |
          postman collection run "2659129-8c920553-7b71-460c-bb12-2a038ba09540" -e "f984dee6-15dc-442c-9bdb-5b6f4ef1417c" \
		  --reporters cli,junit \
          --reporter-junit-export results.xml
		- name: Upload artifact
			uses: actions/upload-artifact@v4
			with:
			  name: postman-results
			  path: results.xml