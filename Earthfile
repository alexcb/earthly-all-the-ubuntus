VERSION 0.7

ip:
  FROM alpine
  RUN apk add curl
  RUN --no-cache curl -s http://icanhazip.com

test:
  FROM alpine
  RUN ls -la

test2:
  FROM alpine
  ARG i
  IF [ $i -gt 0 ]
    FROM busybox
    RUN ls -la
  END

stress:
  FROM progrium/stress
  ARG i
  RUN echo i=$i && stress --cpu 1 --io 1 --vm 1 --vm-bytes 8M --timeout 10s

wat:
  FROM busybox
  ARG tag
  RUN echo using ubuntu:$tag
  FROM ubuntu:$tag
  RUN cat /etc/lsb-release

lots:
  FROM alpine
  COPY tags .
  FOR i IN $(cat tags)
    BUILD +wat --tag=$i
  END
  RUN echo ok

lots-wait:
  FROM alpine
  COPY tags .
  FOR i IN $(cat tags)
    WAIT
      BUILD +wat --tag=$i
    END
  END
  RUN echo ok
