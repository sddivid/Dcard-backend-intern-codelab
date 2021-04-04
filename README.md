Dcard


services
  haproxy-dcard
  dcarddrawcardfrontend
  dcarddrawcardbackend
  redis-server
  mongo
  jmeter-master
  jmeter-slave-1
  jmeter-slave-2
  jmeter-slave-3


rm -rf ${PWD}/jmeter/compose
${PWD}/jmeter/http-request-test.jmx
${PWD}/haproxy/haproxy.cfg
