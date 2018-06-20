## gsm_a6 Library for Arduino (for Ai-Thinker A6 module )

This library for Arduino to use Ai-Thinker A6 modules. This library tested on Thinker A6 (5V Module) and ESP8266.

This library use SoftwareSerial library. So please dont forget this library's limits. Dont use this library on Arduino's hardware serial ports 0 and 1!

### Connection & Pinouts
ESP8266 |   A6      |    Notes  
-------------|-------------|------------
+3.3v| +5.0v!| Power supply input
4 RX_PIN | TX |  
5 TX_PIN | RX |
2   RESET_PIN | RST| Reset Pin(if need)
GND | GND |

### How I use this library?

Firstly inport this library on your Arduino IDE. Then you can use this:

```markdown
#import <gsm_a6.h>

#define RX 4
#define TX 5
#define RESET 2
#define BAUD 9600

/*
 * Defaults => RX: 4 | TX: 5 | Reset: 2 | LED Pin: 10 | LED Flag: true | Baud Rate: 9600
 * GSMSim gsm;
 * GSMSim gsm(RX, TX);
 * GSMSim gsm(RX, TX, RESET);
 * GSMSim gsm(RX, TX, RESET, LED_PIN, LED_FLAG);
 */

GSMSim gsm(RX, TX, RESET);

void setup() {
  gsm.start();
  //gsm.start(9600);
}

```

For more details see Examples.

### Which functions i can use?

#### Module Functions

Name|Return|Notes
:-------|:-------:|:-----------------------------------------------:|
start()|none|Begin the library with 9600 baud rate
start(uint8_t baud_rate)|none|Begin the library with given baud rate
reset()|none|Reset the module
setPhoneFunc(uint8_t level)|true or false|level can be take 0,1 or 4 0-minimum, 1-full, 4-disable
signalQuality()|integer|0-31 -> 0-poor, 31-full, 99-unknown
isRegistered()|true or false|Is module connected to gsm operator?
isSimInserted()|true or false|
pinStatus()|integer|0-ready, 1-sim pin, 2-sim puk, 3-ph sim pin, 4-ph sim puk, 5-sim pin2, 6-sim puk2, 7-unknown
operatorName()|String|returns NOT_CONNECTED if not connected!
operatorNameFromSim()|String|Only works on simcom modules. returns NOT_CONNECTED if not connected!
phoneStatus()|integer|Phone activity status 0-ready, 2-unknown, 3-ringing, 4-call in progress, 99-unkonown
echoOff()|true or false|Echo mode off (for module)
echoOn()|true or false|Echo mode on (for module)
moduleManufacturer()|String|
moduleModel()|String|
moduleRevision()|String|
moduleIMEI()|String|
moduleIMSI()|String|
moduleICCID()|String|
ringerVolume()|integer|
setRingerVolume(uint8_t level)|true or false|level must between 0-100
speakerVolume()|integer|
setSpeakerVolume(uint8_t level)|true or false|level must between 0-100
moduleDebug()|String|print verbose


#### Call functions
Name|Return|Notes
:-------|:-------:|:-----------------------------------------------:|
call(char* phone_number)|true or false|If colp active, it always return true.
callAnswer()|true or false|
callHangoff()|true of false|
callStatus()|integer|Return codes as same as phoneStatus function
callSetCOLP(bool active)|true or false|If active is true, when call status change, module send call details to SoftwareSerial
callIsCOLPActive|true or false|True COLP is active else passive
callActivateListCurrent(bool active)|true or false|say the caller :)
callReadCurrentCall(String serialRaw)|String|Return call status and number like STATUS:xxx\|NUMBER:xxx - This only read when you give raw serial data to this function. It not fetch the raw serial data!


#### SMS functions
Name|Return|Notes
:-------|:-------:|:-----------------------------------------------:|
smsTextMode(bool textModeON)|true or false|TEXT mode or PDU mode.
smsSend(char* number, char* message)|true or false|Message must be in 160 characters and in text mode only use ascii characters.
smsListUnread()|String|If no message found it returns NO_SMS else returns SMSIndexNo:x,y,z. If you have a lot of un read messages, return only SMSIndexNo:
smsRead(uint8_t index)|String|If not message on given index, it return INDEX_NO_ERROR else a string about message.
smsRead(uint8_t index, bool markRead)|String|This function can mark message read or unread when opened.
smsReadFromSerial(String serialRaw)|String|Read sms from serial raw data.
smsIndexFromSerial(String serialRaw)|integer|Get sms index number from serial raw.
smsReadMessageCenter()|String|Get SMS Message Center number.
smsChangeMessageCenter(char* messageCenter)|true or false|Change SMS Message Center number.
smsDeleteOne(uint8_t index)|true or false|Delete sms in given index.
smsDeleteAllRead()|true or false|Delete all read messages.
smsDeleteAll()|true or false|Delete all messages.

#### DTMF functions
Name|Return|Notes
:-------|:-------:|:-----------------------------------------------:|
dtmfSet(bool active, uint8_t interval, bool reportTime, bool soundDetect)|true or false|Activate or deactivate DTMF tones.
dtmfRead(String serialRaw)|String|Get pressed key info from DTMF on serial raw data.


#### USSD functions
Name|Return|Notes
:-------|:-------:|:-----------------------------------------------:|
ussdSend(char* code)|true or false|Send USSD command.
ussdRead(String serialRaw)|String|



### Credits 
Erdem ARSLAN - GSM Library for SIMCOM Modules on Arduino - https://github.com/erdemarslan/GSMSim

Cristian Steib - Sim800l Arduino library - https://github.com/cristiansteib/Sim800l

Vittorio Esposito - Sim800L-Arduino-Library-revised - https://github.com/VittorioEsposito/Sim800L-Arduino-Library-revised

Thanks.


### Support or Contact

If you have any question about this library, please contact only on GitHub.
