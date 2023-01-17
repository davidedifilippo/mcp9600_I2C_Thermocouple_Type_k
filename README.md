## mcp9600_I2C_Thermocouple_Type_k

Digital Thermocouple EMF to Temperature Converter with I2C interface  

Includiamo la libreria che permette di gestire il dispositivo:

      #include <SparkFun_MCP9600.h>
      
 Creiamo un oggetto di tipo MCP9600:
 
       MCP9600 tempSensor;
      
## Fase di setup 

Inizializziamo l'interfaccia di comunicazione I2C alla velocità standard di 100KHz supportata da tutti i dispositivi:

    Wire.begin();
    Wire.setClock(100000);
    
 Inizializziamo l'interfaccia I2C impostando l'indirizzo del dispositivo:
 
    tempSensor.begin();       // Uses the default address (0x60) for SparkFun Thermocouple Amplifier
    
 Controlliamo se il sensore risponde:
    
      if(tempSensor.isConnected()){
            Serial.println("Il dispositivo ha risposto!");
       }
    else {
        Serial.println("Il dispositivo non risponde! Freezing.");
        while(1); //blocca l'esecuzione
    }
    
 ## Fase di loop
  
    if(tempSensor.available()){
             Serial.print("Temperatura giunto caldo: ");
             Serial.print(tempSensor.getThermocoupleTemp());
             Serial.print(" °C   Ambient: ");
             Serial.print(tempSensor.getAmbientTemp());
        Serial.print(" °C   Temperature Delta: ");
        Serial.print(tempSensor.getTempDelta());
        Serial.print(" °C");
        Serial.println();
        delay(20); //attesa per non sovraccaricare l'interfaccia I2C
    }
