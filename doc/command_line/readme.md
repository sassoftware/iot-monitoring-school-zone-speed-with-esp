# Execute the project on the Command Line

## Table of Contents

* [Edit Startup Script](#edit-startup-script)
* [Import Dashboard into ESP Streamviewer](#import-dashboard-into-esp-streamviewer)
* [Execute project on ESP Server](#execute-project-on-esp-server)

![](videos/polyline_command_line.mp4)

The following section discusses executing the project using the command line. The advantage of using the command line is you can see the e-mail notification messages in the log.

Instructions are also included in a later section for [executing the project using SAS ESP Studio](doc/esp_studio/readme.md).



## Edit Startup Script

You must edit the startup script, `run_polyline.sh` to specify the correct server directories.

1.	Open `run_polyline.sh` with a text editor. The following is a listing of the file:

    ~~~
    # Register (DateFlux) ESP environment
    export DFESP_HOME=/opt/sas/viya/home/SASEventStreamProcessingEngine/6.2

    export PATH=$DFESP_HOME/bin:$PATH
    export LD_LIBRARY_PATH=$DFESP_HOME/lib:$DFESP_HOME/lib/tk:/opt/sas/viya/home/SASFoundation/sasexe:$DFESP_HOME/ssl/lib

    export PROJDIR=/home/zestem/polyline

    dfesp_xml_server -http 61002 -pubsub 61003 -model file:///home/zestem/polyline/sensor_log.xml -C "server.single_port_mode=true"
    ~~~

2.	Go to the `export PROJDIR=` line and edit the value to be the directory you created. The following is an example.

    ~~~
    export PROJDIR=/home/zestem/polyline
    ~~~

3.	Go to the last line (command to start XML Server) and edit the `-model` parameter to include the full path to the project file. Ensure there are the correct number of forward slashes (/) at the beginning of the filename. The following is an example:

    ~~~
    -model file:///home/zestem/polyline/sensor_log.xml
    ~~~

## Import Dashboard into ESP Streamviewer

The dashboard for ESP Streamviewer is imported before the project is executed. The is to prepare Streamviewer for the streams. You can use the following steps to import the Monitor School Zones dashboard using SAS ESP Streamviewer.

1.	Start SAS ESP Streamviewer.
    A new dashboard appears.

2.	Click <img src='images/images_import.png'>  to open the Import Data screen.

    <img src='images/import_data.png'>

    _Figure 1 - Import Data Screen_

3.	Select **File**, and then **Choose File**. Select the `dashboard.xml` file you downloaded. Click **OK** to import the dashboard.

## Execute project on ESP Server

1.	Change directories to the directory containing the files you uploaded. The following is an example:

    ~~~
    cd /home/zestem/polyline
    ~~~

2.	Type the following to execute the startup script and start the project:

    ~~~
    ./run_polyline.sh
    ~~~

3.  Switch to ESP Streamviewer. The dashboard should be displaying information. You may need to click <img src='images/images_refresh.png'> to refresh the dashboard.

    <img src='images/dashboard.png'>

    _Figure 2 - Monitor School Zones Dashboard_

4.  Switch to the ESP server. You should see information about the e-mail message that will be sent.

    ~~~
    == EMAIL ==
        Sender: zephstemle@gmail.com
        Recipient: zeph.stemle@sas.com
        Subject: Testing
        From: Greenwood Community Schools
        To: Vehicle 1
        Content: You were clocked doing 33.562354 MPH, travelling E in the Greenwood High School school zone.
    == END EMAIL ==
    ~~~


