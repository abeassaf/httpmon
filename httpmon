#! /bin/sh
# This script will run cron every minute. It will count the number of processes running for apache2 (debian/Ubuntu)
# or httpd (RedHat/Centosa). It will run once started from cron and loop second time after 30 seconds sleep and then
# exit, efectivly running every 30 seconds. The cron job will send the std ouput and error 
# to /var/log/httpmon/*.log. logrotate will rotate the logs in that directory. 
counter=0
while [ $counter -lt 2 ]
do
NumProc=$(pgrep -c 'httpd|apache2')
echo $(date)
if [ $NumProc -lt 10 ]
  then
echo “[LOW] Web Server OK!”
elif [ $NumProc -gt 20 ] && [ $NumProc -lt 100 ]
then  
echo “[HIGH] Web Server Working hard!”
else
echo “[CRITICAL] Web Server under heavy load, restart required” 
echo  "Restarting Apache serever ...."
result=$(service apache2 restart)

fi
counter=$(($counter+1))
if [ $counter -eq 2 ]
then
exit
fi
sleep 30
done
