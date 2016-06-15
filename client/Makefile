include ../config.mk

.PHONY: all install uninstall reallyclean clean

CC=gcc
CROSS_COMPILE=mips-openwrt-linux-

#all : mosquitto_pub mosquitto_sub

#mosquitto_pub : pub_client.o client_shared.o
#	${CROSS_COMPILE}${CC} $^ -o $@ ${CLIENT_LDFLAGS}

#mosquitto_sub : sub_client.o client_shared.o
#	${CROSS_COMPILE}${CC} $^ -o $@ ${CLIENT_LDFLAGS}

#pub_client.o : pub_client.c ../lib/libmosquitto.so.${SOVERSION}
#	${CROSS_COMPILE}${CC} -c $< -o $@ ${CLIENT_CFLAGS}

#sub_client.o : sub_client.c ../lib/libmosquitto.so.${SOVERSION}
#	${CROSS_COMPILE}${CC} -c $< -o $@ ${CLIENT_CFLAGS}

#client_shared.o : client_shared.c client_shared.h
#	${CROSS_COMPILE}${CC} -c $< -o $@ ${CLIENT_CFLAGS}

all : mosquitto_client

mosquitto_client : mosquitto_client.o 
	${CROSS_COMPILE}${CC} $^ -o $@ ${CLIENT_LDFLAGS}
mosquitto_client.o : mosquitto_client.c mosquitto_client.h ../lib/libmosquitto.so.${SOVERSION}
	${CROSS_COMPILE}${CC} -c $< -o $@ ${CLIENT_CFLAGS}
	

../lib/libmosquitto.so.${SOVERSION} :
	$(MAKE) -C ../lib

install : all
	$(INSTALL) -d ${DESTDIR}$(prefix)/bin
	$(INSTALL) -s --strip-program=${CROSS_COMPILE}${STRIP} mosquitto_pub ${DESTDIR}${prefix}/bin/mosquitto_pub
	$(INSTALL) -s --strip-program=${CROSS_COMPILE}${STRIP} mosquitto_sub ${DESTDIR}${prefix}/bin/mosquitto_sub

uninstall :
	-rm -f ${DESTDIR}${prefix}/bin/mosquitto_pub
	-rm -f ${DESTDIR}${prefix}/bin/mosquitto_sub

reallyclean : clean

clean : 
	-rm -f *.o mosquitto_pub mosquitto_sub mosquitto_client
