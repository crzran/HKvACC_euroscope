# HKvACC_euroscope
This is Ran CHEN/CID:1626714 's contribution to the VATSIM Hong Kong

Two mayor updates have been added to the plugins, first is the VCH, second is the ACDM.
1. VCH (Available both in dep list and startup list)
VCH is added to replace the sequencing related to giving clearance, and it has more functions. By left clicking the VCH, it gives the controller multiple options,
including p&s, taxi, clearance, etc.after making a left click, it will automatically start timing how long time is the aircraft waiting. When the clearance is addressed,
simply left click it again and select no reqeust)

2. ACDM (Available ONLY on startup list)
The protocode of ACDM is accredited to Ruig Roger, VATSPA, and i would like to express my very big thx to Pablo Zhang/S3, VATSPA, for his teaching

ACDM, which means Airport Collaborative Decision-Making, is for determing the startup time etc in order to increase efficiency of an airport under high traffic volumn
All of the things mentioned below are available on https://github.com/rpuig2001/CDM#cdm-plugin-v2
   1. Definition of terms
      EOBT: Estimated off block time.

      TOBT: Target off block time.

      TSAT: Target Start-Up Approval Time.

      TTOT: Target Take Off Time.

      TSAC: Target Start-Up Approval Communicated.

      ASAT: Actual Start-Up Approval Time.

      ASRT: Actual Start-Up Request Time.

      CTOT: Calculated Take Off Time.
      
      Most of the terms are self-explanatory. But just to be clear, EOBT is directly pulled from the flight plan and TOBT depends on the time when you give the pushback
      clearance
    2. User mannual
        ## MASTER AND SLAVE:
           - Master: The master is the "admin" of the CDM and is the only controller who calculates the times (TSAT, TTOT and ASRT)
           - Use ``.cdm master {airport}`` command (**TO LET THE CDM DO IT'S JOB, ONLY 1 CONTROLLER CAN BE THE MASTER AT THE SAME TIME**).
           - Slave: The Slave Monitors the CDM and has some limited actions.
           - Default type, so, you don't need to change anything unless you are now a master, where you can use ``.cdm slave {airport}`` command.
           
         ### HOW TO DO A CONTROLLER CHANGE CORRECTLY:
           1. Check to have the same *CDMconfig.xml* and *taxizones.txt* configuration, otherwise it won't work correctly.
           2. The **Old controller** changes to Slave with command ``.cdm slave``.
           3. Once there are no master controllers, the **new controlles** gets the master "rol" with the command ``.cdm master {airport}``.
           4. That's it!
           
         #### HOW TO ADDRESS CTOT IN EVENTS THAT REQUIRE BOOKING
           - Add CTOTs which will be imported on Euroscope start-up or with the command ".cdm ctot". Add CTOTs with the following format: ``CALLSIGN,CTOT`` or       ``XXXXXX,CTOT``, ex: ``XXXXXX,1745`` - XXXXXX is vatsim user's CID or ``VLG11P,1745`` (Each line has an aircraft)
           
         ### ASSUMPTION OF CAPABILITY OF RUNWAY
            - All runways are assumed to be capable of dealing with 30 planes per hour under normal visibility, while for low visibility, the number is 10/h
            
         #### ALIAS AVAILABLE
            - ``.cdm reload`` - Reloads all CDM plugin configs and taxizones file.
            - ``.cdm refresh`` - Force the refresh phase to do it now.
            - [DISABLED] ``.cdm ctot`` - Loads ctot.txt data.
            - ``.cdm save`` - Saves data to savedData.txt.
            - ``.cdm load`` - Loads savedData.txt.
            - ``.cdm master {airport}`` - Become the master of the selected airport.
            - ``.cdm slave {airport}`` - Turn back to slave of the selected airport.
            - ``.cdm refreshtime {seconds}`` - It changes the refresh rate time in seconds (Default 30, MAX 99 Seconds).
            - ``.cdm delay {minutes}`` - Adds delay minutes to all traffics that have a TSAT greater then now. (it doesn't apply if TSAT has already passed) - WAIT   SOME SECONDS TO UPDATE AFTER APPLIED.
            - ``.cdm lvo`` - Toggle lvo ON or OFF.
            - ``.cdm realmode`` - Toggle realmode ON or OFF.
            - ``.cdm remarks`` - Toggle set TSAT to Euroscope scratchpad ON or OFF.
            - ``.cdm rates`` - Updates rates values from rate.txt.
            - ``.cdm help`` - Sends a message with all commands.
          ### ## Functions and colors:
            - Column A: It toggles an A to remember the controller that the plane is waiting for something.
            - ![#f5ef0d](https://via.placeholder.com/15/f5ef0d/000000?text=+) `YELLOW` or defined ``color5``: Always this color.

            - Column EOBT: It gets the EOBT set by the pilot in the flightplan.

            - Column TOBT: TOBT will calculate TSAT and TTOT from the TOBT time. To delete it simple edit the time and press enter deleting the content.
            - If there is no ASRT or "Ready Start-up GREEN", at TOBT+5, TSAT and other times will be invalidated.
            - To add a TOBT, use the Ready TOBT Function to set the actual time as a TOBT or the Edit TOBT to set a 4 digits time. (Right click to add)
            - ![#8fd894](https://via.placeholder.com/15/8fd894/000000?text=+) `LIGHT GREEN` or defined ``color2``: From EOBT-35 to EOBT-5.
            - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`  or defined ``color1``: After EOBT-5.

            - Column E: It shows a letter depending on the plane timmings:
            - P: EOBT is farther than the Actual Time - 35min.
            - C: EOBT is less than 35min and TOBT hasn't expired (TOBT+6) or TSAT hasn't expired (TSAT+6).
            - I: TSAT has expired.

            - Column TSAT: It is the TTOT - the taxi time defined in the taxizones.txt, be aware, rwy 25C and 07C are not designed

            - Column TTOT: The plugin calculates a TSAT based on this column, the TTOT, you can't have planes with same TTOT, the time between departures is calculated             from the rate/hour. So if you need 40 departures/hour, the plugin will calculate it for you with no equal TTOTs.
            - Color defined as ``color9``.

            - Column TSAC: With the left click you can directly set the tsat and with the right click you can remove it or set the time you want. If this field is +/-             5min that the TSAT, the color change to orange to indicate that his TSAT has changed more than 5min.
            - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN` or defined ``color1``: If between +/- 5min of TSAT.
            - ![#ed852e](https://via.placeholder.com/15/ed852e/000000?text=+) `ORANGE` or defined ``color4``: If +/- 5min of TSAT.

            - Column ASAT: It sets the time when ST-UP, TAXI or DEPA state is set on the first time.
            - ![#00c000](https://via.placeholder.com/15/00c000/000000?text=+) `DARK GREEN`  or defined ``color1``: If actual time < ASAT - 5min.
            - ![#f5ef0d](https://via.placeholder.com/15/f5ef0d/000000?text=+) `YELLOW` or defined ``color5``: From ASAT+5 to always.

            - Column ASRT: It shows the requested StartUp time, It can be added to the list with the toggle function or sending a REA Msg.
            - Color defined as ``color10``.
  
            - Column Ready Start-up: It shows if the plane is Ready for Start-up or not together with the ASRT. (ASRT and Ready Start-up do the same, but this column  is a way to represent the real ready start-up function from IRL because Euroscope doesn't have this function)
            - ``Toggle Ready Start-up function`` sets RSTUP with ASRT or removes it if already set.
            - Color defined as ``GREEN`` when RSTUP is set.
            - Color defined as ``RED`` when RSUP is NOT set.

            - Column CTOT: It shows aircraft's CTOT which can be added, modified, removed or reloaded.
            - Color defined as ``color11``.
     3. Advise for future training
        1. In practical training, train the trainee how to effective use VCH
        2. In practical training, teach the what the different words, such as CTOT means in startup list
        3. Strongly recommend the trainee to use the startup menu
        4. Train the trainee how to use those functions since they will be handy for especially GND and DEL
     
     4. Notes
        1. This is the very first version of the plugin update, and especially the ACDM, is customized by Ryan Chen. There may be inaccuracy in TTOT, if any controller
        found that there is a significant difference between the TTOT and the ATOT, which is the actual take off time. Please record the aircraft's departure gate
        number, runway in use, and the actual time taken. Then, contact Ryan Chen whether through Discord or email: 2642608411@qq.com
        2. This file is intended only for the VATSIM HKvACC. Any unauthorized use is prohibited.
          
           
