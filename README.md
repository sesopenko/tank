# tank

The Apex Fusion code for my aquarium. Apex units have poor restoration capability, in case of failure, so I've documented all of my outlet scripts here. Feel free to use them for your own tank, if you find anything useful.

## Naming convention:

Each outlet's name ends with the outlet number. This makes it easy to determine what's plugged into where.

## Feed cycles

Feed A: 20 minutes

All of the big powerheads turn off and only the return pump & little powerheads run to maintain circulation.

## Devices

### Device 3_7 "BigPH7"

Big powerhead

```
Fallback ON
Set OFF
If Time 12:00 to 21:00 Then ON
If FeedA 005 Then OFF
```

### Device 3_8 "Doser8"

Ph control. fallback ON, Probe name: pH, High value: 9.0, low value: 8.90, on when: low

```
Fallback ON
If pH > 9.00 Then OFF
If pH < 8.90 Then ON
```

### Device 4_1 "Feed_4_1"

Control type: feeder, First feeding 11:00, 1 drum rotation, 1 feeding per day, feed cycle A

```
OSC 000:00/000:30/000:30 Then ON
If Time 00:00 to 11:00 Then OFF
If Time 11:02 to 00:00 Then OFF
If FeedA 000 Then ON
```

### Device 3_3 "flrscnt_3"

Control type: Light

Fallback: Off, On time: 15:00, off time: 21:00, shutdown pobe: Tmp, Shutdown value: 82.0, hysterysis: 000:01

```
Fallback OFF
Set OFF
If Time 15:00 to 21:00 Then ON
If Tmp > 82.0 Then OFF
Min Time 000:01 Then OFF
```

### Device 3_6 "fuge_6"

```
Fallback OFF
Set OFF
If Time 01:00 to 15:00 Then ON
If Tmp > 82.0 Then OFF
Min Time 000:01 Then OFF
```

### Device 3_4 "heater2_4"

```
Fallback OFF
If Tmp < 79.0 Then ON
If Tmp > 79.2 Then OFF
```

### Device 3_1 "return1"

```
Fallback ON
Set ON
If FeedB 000 Then OFF
```

### Device 3_2 "skimmer2"

This depends on return pump outlet being properly named so that if the return pump isn't on then the skimmer doesn't run. This prevents a skimer overflow which can crash the tank and kill animals with nutrient overload.

```
Fallback OFF
Set ON
If Output return1 = OFF Then OFF
If Time 12:00 to 23:59 Then OFF
If FeedA 030 Then OFF
If FeedB 030 Then OFF
If FeedC 030 Then OFF
If FeedD 030 Then OFF
Defer 005:00 Then ON
```

### Device 3_5 "tunze_5"

All of the tunze powerheads are plugged into here.

```
Fallback ON
Set ON
If FeedA 000 Then OFF
If FeedB 000 Then OFF
```
