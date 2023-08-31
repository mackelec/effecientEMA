# effecientEMA
very efficient EMA for arduino

```
enum SmoothingExponent {
    SMOOTHING_VALUE_1 = 0,
    SMOOTHING_VALUE_2 = 1,
    SMOOTHING_VALUE_4 = 2,
    SMOOTHING_VALUE_8 = 3,
    SMOOTHING_VALUE_16 = 4,
    SMOOTHING_VALUE_32 = 5,
    SMOOTHING_VALUE_64 = 6,
    SMOOTHING_VALUE_128 = 7,
    SMOOTHING_VALUE_256 = 8,
    SMOOTHING_VALUE_512 = 9
};

int updateEMA(int newValue, int currentEMA, SmoothingExponent smoothingExponent)
{
    return ((newValue << smoothingExponent) + (currentEMA << 10) - (currentEMA << smoothingExponent)) >> 10;
}

```

This simple EMA uses simple rotates and integer math.

###  Example

```
enum SmoothingExponent {
    SMOOTHING_VALUE_1 = 0,
    SMOOTHING_VALUE_2 = 1,
    SMOOTHING_VALUE_4 = 2,
    SMOOTHING_VALUE_8 = 3,
    SMOOTHING_VALUE_16 = 4,
    SMOOTHING_VALUE_32 = 5,
    SMOOTHING_VALUE_64 = 6,
    SMOOTHING_VALUE_128 = 7,
    SMOOTHING_VALUE_256 = 8,
    SMOOTHING_VALUE_512 = 9
};

int updateEMA(int newValue, int currentEMA, SmoothingExponent smoothingExponent)
{
    return ((newValue << smoothingExponent) + (currentEMA << 10) - (currentEMA << smoothingExponent)) >> 10;
}

void setup() {
    Serial.begin(9600);
}

void loop() {
    SmoothingExponent currentExponent = SMOOTHING_VALUE_4;  // Choose the desired smoothing value
    
    int newData = random(0, 1000);

    static int emaValue = 0;
    emaValue = updateEMA(newData, emaValue, currentExponent);

    Serial.print("New Data: ");
    Serial.print(newData);
    Serial.print("  EMA: ");
    Serial.println(emaValue);

    delay(1000);
}

```
