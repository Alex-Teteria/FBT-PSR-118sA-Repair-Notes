# FBT-PSR-118sA-Repair-Notes
Repair notes, reconstructed schematic fragments, component replacements, and troubleshooting documentation for the FBT PSR 118sA active subwoofer.

## Fault Description

Вихід з ладу вихідних MOSFET транзисторів типу IRFB38N20D. Усі несправні транзистори мали коротке замикання між виводами Drain, Source та Gate (D-S-G), внаслідок чого спрацьовував запобіжник по живленню.

Під час подальшої діагностики було виявлено такі несправності:

### Main Amplifier Board

* вихід з ладу вузла Active Gate Drive Shunt в одному із силових плечей;
* вихід з ладу двох драйверів IR2110;
* вихід з ладу стабілітрона +5 V у колі живлення драйверів;
* керамічний конденсатор біля одного із силових MOSFET мав відгорілий вивід.

### PWM Board

Стабілізатор 78L05 перебував у режимі обмеження струму. Подальша перевірка показала наявність короткого замикання по шині +5 V.

Після послідовного випаювання цифрових мікросхем серії 74HC було виявлено несправні компоненти:

* 74HC04D;
* 74HCU04D;
* 74HC00D.

## Circuit Modifications

### DC Offset Adjustment

Після заміни операційних підсилювачів TL072 та TL074 у вузлі формування сигналу зворотного зв'язку з'явилося значне постійне зміщення на виході підсилювача.

Перевірка елементів вузла не виявила несправностей, однак штатна схема не передбачала можливості компенсації зміщення.

Для забезпечення регулювання DC offset було додано:

* підстроювальний резистор RV1 (100 kΩ), підключений між шинами живлення +16 V та -16 V;
* резистор R7 (1 MΩ), через який регульована напруга подається до сумуючого вузла каскаду на TL072.

Таке доопрацювання дозволило компенсувати постійне зміщення та відновити нормальний режим роботи підсилювача.

Додані компоненти:

* RV1 — 100 kΩ;
* R7 — 1 MΩ.  
[Фрагмент схеми із доданим DC Offset Adjustment](./schematics/DC_Offset_Adjustment.PDF)  

## Disclaimer

The schematic fragments published in this repository were reconstructed from PCB inspection and measurements and are provided for educational and repair documentation purposes. They are not official manufacturer documentation.  

## License

This work is licensed under CC BY 4.0.

See the LICENSE file for details.
