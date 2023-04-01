# supervisor-python
Running a Python application using supervisor

![wallpaper.jpg](wallpaper.jpg)

In Linux, a supervisor is a program that runs in the background and manages other processes on the system.
It is also referred to as a process manager or a daemon. The supervisor's main function is to start, stop,
and restart other processes as needed, and to ensure that they run smoothly and do not crash.

Supervisors are particularly useful for managing long-running processes, such as web servers or databases,
that need to be kept running continuously. They also provide a way to manage multiple instances of the
same process, allowing for load balancing and high availability.

Some popular supervisors in Linux include systemd, Upstart, and Supervisor. These tools provide various
features and capabilities for managing processes, such as automatic restart on failure, dependency
management, and process prioritization.

Supervisord is a powerful process control system for Unix-like operating systems. It can be used to manage
a wide variety of processes and applications. Some common examples include:

|Service|Goal|
|---|---|
|Web servers|Supervisord can be used to manage web servers such as Apache or Nginx, ensuring that they start up automatically on system boot and are restarted if they crash.|
|Database servers|Supervisord can be used to manage database servers like MySQL, PostgreSQL, or MongoDB, ensuring that they are running and available.|
|Task queues|Supervisord can be used to manage task queues like Celery, ensuring that tasks are being executed and retrying them if they fail.|
|Background workers|Supervisord can be used to manage background workers like Redis, ensuring that they are running and processing jobs.|
|Custom scripts|Supervisord can be used to manage custom scripts or applications that you have developed, ensuring that they run continuously and are automatically restarted if they fail.|

## References

- [Running Supervisord](http://supervisord.org/installing.html)

## Architecture

|File|Description|
|---|---|
|[service.py](service.py)|Python application that runs as a service.|
|[supervisord.conf](supervisord.conf)|Supervisor configuration file.|

## Instructions

#### Creating a virtual environment
```bash
virtualenv -p python3 .env
source .env/bin/activate
pip install -r requirements.txt
```

#### Updating the supervisor service registry
```bash
ps -ef | grep supervisor | grep -v supervisord.conf | grep -v grep | grep -v tail | awk '{print $2}' | xargs -I{} kill {} 
supervisord --configuration supervisord.conf --user martincastro --loglevel INFO
```

#### Check the logs
```bash
tail -f /tmp/stderr.log /tmp/stdout.log /tmp/supervisord.log
```
```bash
==> /tmp/supervisord.log <==
2023-04-01 02:26:49,875 INFO success: my-demo-service-0 entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)
2023-04-01 02:26:49,876 INFO success: my-demo-service-1 entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)
2023-04-01 02:26:49,877 INFO success: my-demo-service-2 entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)

==> /tmp/stderr.log <==
Hello, world!
Hello, world!
Hello, world!
Hello, world!
Hello, world!
Hello, world!
Hello, world!
Hello, world!
Hello, world!
```
