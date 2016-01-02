# entrega-06-01
son 2 codigos, antares (coordinador) y seguidor 2 (Router2), el primero lo que hace es ordenar la info enviada por el segundo,
hasta ahora me he roto la cabeza solo para hacer que todo este ordenado en un String.... :( me falta que identifique a cada seguidor por 
ID y que guarde respecto a eso, los codigos son:

  ANTARES

          #include <SoftwareSerial.h>
             
          SoftwareSerial Antares(8, 9); // (DOUT,DIN) -> (RX,TX)
          
          
          
          void setup() {
            Serial.begin(19200);   //initialize serial
            Antares.begin(19200);
            Antares.listen();
            
          }
          
          void loop() {
          
            String rawInfo;
            //int listaB1 [10];
            String data;
            
            if (Antares.isListening()) { 
             
              // lee la info y la entrega ordenada 
              if (Antares.available()) {
                char i = (char)Antares.read();  // imprime todo en una linea
                if ( i == '\r'){                    
                  }
                else {
               rawInfo += i ;
                  } 
                //Serial.print(rawInfo); 
                //if(rawInfo.substring(1,2)=="B1"){ 
                  //rawInfo.remove(1,2);
                  Serial.print(rawInfo);  
                 // }
                      
                  }    
              }
            
          
           }


 SEGUIDOR 2 (es el mismo codigo que 1 y 3, solo cambia el ID )

          #include <SoftwareSerial.h>
             
          SoftwareSerial Seg2(8, 9); // (DOUT,DIN) -> (RX,TX)
          int r; // numero random que simula una lectura
          String ID = "B1"; // Identificacion del modulo 
          
          
          void setup() {
            Serial.begin(19200);   //initialize serial
            Seg2.begin(19200);
            
          }
          
          void loop() {
          
            // simulacion de muestra y tiempo
            r = random(300,350);
          
            //info que manda
            
            Seg2.print(ID);
            Seg2.print(" ");
            Seg2.print(r);
            Seg2.println("\r");
            delay(1000);
            
            //envia la info  
            if (Serial.available()) {
                Seg2.print((char)Serial.read()); 
            }
            
           
            
          }
           
