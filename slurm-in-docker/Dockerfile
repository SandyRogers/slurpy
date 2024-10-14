FROM ubuntu:oracular
LABEL authors="mgnify team"

RUN apt -y update && apt -y upgrade && apt -y install curl nano wget zip bzip2

RUN apt -y install munge python3-pip python-is-python3

RUN apt -y install sudo gosu netcat-traditional slurm-wlm slurmdbd slurm-wlm-jwt-plugin slurm-wlm-mysql-plugin slurmrestd default-jre

RUN mkdir -p /var/spool/slurm/statesave/
RUN dd if=/dev/random of=/var/spool/slurm/statesave/jwt_hs256.key bs=32 count=1
RUN chown slurm:slurm /var/spool/slurm/statesave/jwt_hs256.key
RUN chmod 0600 /var/spool/slurm/statesave/jwt_hs256.key
RUN chown slurm:slurm /var/spool/slurm/statesave
RUN chmod 0755 /var/spool/slurm/statesave

COPY slurm.conf /etc/slurm/slurm.conf
COPY slurmdbd.conf /etc/slurm/slurmdbd.conf
COPY cgroup.conf /etc/slurm/cgroup.conf
RUN chmod 600 /etc/slurm/slurmdbd.conf
RUN chown -R slurm:slurm /etc/slurm/

RUN mkdir -p /run/munge && chown -R munge /run/munge
RUN mkdir -p /var/run/slurm && chown -R slurm:slurm /var/run/slurm
RUN mkdir -p /var/log/slurm && chown -R slurm:slurm /var/log/slurm
RUN mkdir -p /var/spool/slurmctld && chown -R slurm:slurm /var/spool/slurmctld
RUN mkdir -p /var/spool/slurmd && chown -R slurm:slurm /var/spool/slurmd

COPY slurm-node-entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

ENV SLURM_INCLUDE_DIR=/usr/include
ENV SLURM_LIB_DIR=/usr/lib/x86_64-linux-gnu
#RUN wget -qO- https://get.nextflow.io | bash
#RUN chmod +x nextflow
#RUN mv nextflow /usr/bin/

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
