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
