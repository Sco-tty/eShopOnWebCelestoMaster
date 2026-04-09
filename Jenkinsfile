pipeline {
  agent any
  stages {
    stage('Restore') {
      steps {
        bat 'dotnet restore eShopOnWeb.sh --verbosity normal'
      }
    }

    stage('Build') {
      steps {
        bat 'dotnet build eShopOnWeb.sh -c Release --no-Restore'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            bat 'dotnet test tests/UnitTests -c Release --no-build --verbosity normal'
          }
        }

        stage('IntegrationTest') {
          steps {
            bat 'dotnet test tests/IntegrationTests -c Release --no-build --verbosity normal'
          }
        }

        stage('FunctionalTests') {
          steps {
            bat 'dotnet test tests/FunctionalTests -c Release --no-build --verbosity normal'
          }
        }

      }
    }

    stage('Deployement') {
      steps {
        bat '@echo off echo === PUBLICATION DES PROKETS INDIVIDUELS === echo Publication de Web... dotnet publish src\\Web\\Web.csproj -c Release -o "C:\\publish\\aspnet\\Web" --no-nuild echo === DEPLOYEMENT TERMINE ==='
      }
    }

  }
}