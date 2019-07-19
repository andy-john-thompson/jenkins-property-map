//Jenkinsfile showing an example of how to read in values from properties files
def SLAVE="fyre_ubuntu_vm"

def set_property_map() {
  def component_one_properties = readProperties file: "${WORKSPACE}/properties/component_one.properties"
  def component_two_properties = readProperties file: "${WORKSPACE}/properties/component_two.properties"
  def all_properties = component_one_properties +  component_two_properties
  def all_properties_map=all_properties.collect { key, value -> return key+'='+value }
  return all_properties_map
}

node ("${SLAVE}") {
  timestamps {
    stage('checkout scm'){
      checkout scm
    }
    
    stage('use properties'){
      withEnv(set_property_map()) {
        sh '${WORKSPACE}/test_properties.sh'
      }
    }
  }
}
