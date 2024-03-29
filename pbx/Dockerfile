FROM andrius/asterisk

RUN apk update && apk --no-cache add sngrep sox mpg123

ADD pjsip.conf /etc/asterisk/pjsip.conf
ADD extensions.conf /etc/asterisk/extensions.conf
ADD rtp.conf /etc/asterisk/rtp.conf
