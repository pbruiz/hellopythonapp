node {
  stage('Construir y Desplegar') {
    openshiftBuild bldCfg: 'hellopythonapp',
      namespace: 'development01',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'development01'
  }
  stage('Aprobar (Pruebas)') {
    input message: 'Aprobado para Pruebas?',
      id: 'approval'
  }
  stage('Desplegar en Pruebas') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'development01',
      srcTag: 'latest',
      destinationNamespace: 'testing01',
      destStream: 'hellopythonapp',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'testing01'
  }
  stage('Aprobar (Produccion)') {
    input message: 'Aprobado para Produccion?',
      id: 'approval'
  }
  stage('Desplegar en Produccion') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'development01',
      srcTag: 'latest',
      destinationNamespace: 'production01',
      destStream: 'hellopythonapp',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'production01'
  }
}
