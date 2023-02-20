sudo ./svc.sh install $SUDO_USER
sudo ./svc.sh start
sudo ./svc.sh status


Update environment variables
When you configure the service, it takes a snapshot of some useful environment variables for your current logon user such as PATH, LANG, JAVA_HOME, ANT_HOME, and MYSQL_PATH. If you need to update the variables (for example, after installing some new software):
./env.sh
sudo ./svc.sh stop
sudo ./svc.sh start



./config.sh remove


q2dzyjstknjsscgu3fbpjhmv4opt4dags4dixkda3sjicrxk4rcq

