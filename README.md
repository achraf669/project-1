name: Test Build and Deploy Pipeline
on:
  push:
    branches:
      - main
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Code
      uses: actions/checkout@v2
    - name: Install Dependencies
      run: npm install
    - name: Build Application
      run: npm run build
    - name: Deploy Application
      uses: azure/webapps-deploy@v2
      with:
        app-name: 'my-app'
        publish-profile: ${{ secrets.AzureAppService_PublishProfile }}
        package: .
