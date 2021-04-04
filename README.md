ㄔㄡCard


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


HA => F2E => B2E => DB[redis,mongo]

{jmeter_F2E}HA => F2E{jmeter_M} => B2E => DB[redis,mongo]

{jmeter_F2E(GUI)}HA => F2E{jmeter_M} => B2E => {Robo3T(GUI),ARDM(GUI)}DB[redis,mongo]
