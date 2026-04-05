# What is a "Thermal Runaway?"
The Marlin firmware, on which the CR6 Community Firmware is based, includes four thermal control system failure protection mechanisms.

In all four cases, Marlin monitors the temperature reported by the thermistors and compares it to the commanded temperatures, for both the hotend and the heated bed.  

If either hotend or bed heater system incurs one of these error conditions, then Marlin shuts the printer down immediately:

1. **Thermal Runaway protection** shuts down the printer if the reported temperature drifts "too far away" from the target temperature "for too long".
2. **Heater Failure** shuts down the printer if the reported temperature increases "too slowly", when heating is commanded.
3. **MINTEMP** shuts down the printer if a temperature sensor reports a value less than the MINTEMP value set in Configuration_adv.h.  This is intended to detect short-circuited thermistors. (Assumes a negative thermal coefficient (NTC)-type thermistor)
4. **MAXTEMP** shuts down the printer if a temperature sensor reports a value higher than the MAXTEMP value set in Configuration_adv. This is intended to detect open-circuited thermistors. (Assumes a negative thermal coefficient (NTC)-type thermistor)

# My printer shuts down immediately upon power-up, with a Thermal Runaway failure
We had several CR6-SE operators using either the 4.5.3 or the 1.1.0.3 board report this behaviour. 
In one case, the operator confirmed the following troubleshooting procedure with the Creality Support technician:
* Disconnect all connectors from board with the exception of 24 V power, Bed Heater, and screen output. 
* If the issue persists and a FW flash does not resolve the issue then the board is toast and you have to replace it.
In that case, installing a replacement 1.1.0.3 board solved the problem.

NOTES: 
1. As of 61F_090522_v2, the refactored DWIN_SET firmware has included nozzle and bed temperature readouts on the Thermal Runaway and Heater Failed warning screens, to help isolate the cause of a shutdown to the channel that likely caused it.  Those users who had an immediate thermal runaway shutdown on power up reported "all zeroes" on that screen.  A special edit made to Marlin to delay that shutdown for those users revealed 300+ C on both bed and nozzle.
2. There is also a "Thermistor Failure" warning screen in the User Interface screens files, but Marlin makes no mention of this warning in this configuration summary: [https://marlinfw.org/docs/configuration/configuration.html](https://marlinfw.org/docs/configuration/configuration.html)  It is possible that this screen is not used by the current Marlin design.

