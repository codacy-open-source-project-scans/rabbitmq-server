export PATH :=$(CURDIR):$(PATH)
HOSTNAME := $(shell hostname)
MVN_FLAGS += -Ddeps.dir="$(abspath $(DEPS_DIR))" \
			 -Dhostname=$(HOSTNAME) \
			 -Dcerts.dir=$(SSL_CERTS_DIR) \
			 -Dmqtt.ssl.port=$(MQTT_SSL_PORT) \
			 -Dmqtt.port=$(MQTT_PORT) \
			 -Dmqtt.port.2=$(MQTT_PORT_2) \
			 -Dmqtt.port.3=$(MQTT_PORT_3) \
			 -Damqp.port=$(AMQP_PORT)

.PHONY: deps tests v5tests ssltests clean distclean

deps:
	mkdir -p lib
	@mvnw dependency:copy-dependencies -DoutputDirectory=lib

tests:
	# Note: to run a single test
	# @mvnw -q $(MVN_FLAGS) -Dtest=MqttTest#subscribeMultiple test
	@mvnw -q $(MVN_FLAGS) -Dtest=MqttTest test

ssltests:
	@mvnw -q $(MVN_FLAGS) -Dtest=MqttSSLTest test

v5tests:
	@mvnw -q $(MVN_FLAGS) -Dtest=MqttV5Test test

v5ssltests:
	@mvnw -q $(MVN_FLAGS) -Dtest=MqttV5SSLTest test

clean:
	@mvnw clean

distclean: clean
	rm -f lib/*.jar
