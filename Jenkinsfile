import hudson.FilePath
import groovy.json.JsonBuilder
import groovy.json.JsonOutput

node {

stage("Testing Post") {


printf "Before builder"   
JsonBuilder builder = new JsonBuilder()
printf "After builder"
builder.post {
   build {
    number "lamp"
    log 'log'
    url "lamp"
    status "lamp"
    scm {
     culprits {}
     changes {}
     commit "lamp"
     url "lamp"
     branch "lamp"
    }
    timestamp "lamp"
    notes ''
    artifacts {}
    phase 'COMPLETED'
    full_url 'lamp'
    queue_id 0
   }
   display_name "lamp"
   name "lamp"
   url "lamp"
  }
printf "Json Built"
def json = builder.toString()
printf "json: ${json}"
}
}




