# virusubiquiti
remover virus

FILE=/etc/persistent/mf.tar

# Check virus
if [ -e "$FILE" ] ; then
    echo "Infected"
    #Acess folder
    cd /etc/persistent
    #Remove the virus
    rm mf.tar
    rm -R .mf
    rm -R mcuser
    rm rc.poststart
    #Remove mcuser in passwd
    cat /etc/passwd | grep -v mcuser >> /etc/passwd2
    cat /etc/passwd2 >> /etc/passwd
    rm /etc/passwd2
    #Write new config
    cfgmtd -w -p /etc/
    cfgmtd -f /tmp/system.cfg -w
    #Kill process
    killall -9 search
    killall -9 mother
    killall -9 sleep
    echo "Clear Completed"
    reboot
else
    echo "Clear"
    exit
fi
