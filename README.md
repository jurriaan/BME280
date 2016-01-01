


# BME280
Provides an Arduino library for reading and interpreting Bosch BME280 data.

## Table of Contents

---

* [BME280](#bme280)
* [Table of Contents](#table_of_contents)
* [Summary](#summary)
* [Installation](#installation)
* [Usage](#usage)
* [Methods](#methods)

		** [BME280(uint8_t tosr = 0x1, uint8_t hosr = 0x1, uint8_t posr = 0x1, uint8_t mode = 0x3, uint8_t st = 0x5, uint8_t filter = 0x0, bool spiEnable = false, uint8_t bme_280_addr = 0x76)](#bme280(uint8_t_tosr_=_0x1,_uint8_t_hosr_=_0x1,_uint8_t_posr_=_0x1,_uint8_t_mode_=_0x3,_uint8_t_st_=_0x5,_uint8_t_filter_=_0x0,_bool_spienable_=_false,_uint8_t_bme_280_addr_=_0x76))
		** [bool  begin()](#begin)
		** [float ReadTemperature(bool celsius = true)](float_readtemperature(bool_celsius_=_true))
		** [float ReadPressure(uint8_t unit = 0x0)](#float_readpressure(uint8_t_unit_=_0x0))
		** [float ReadHumidity()](#float_readhumidity())
		** [void  ReadData(float& pressure, float& temp, float& humidity, bool metric = true, uint8_t p_unit = 0x0)](#void _readdata(float&_pressure,_float&_temp,_float&_humidity,_bool_metric_=_true,_uint8_t_p_unit_=_0x0))
		** [float CalculateAltitude(bool metric = true, float seaLevelPressure = 101325)](#float_calculatealtitude(bool_metric_=_true,_float_sealevelpressure_=_101325))
		** [float CalculateAltitude(float pressure, bool metric = true, float seaLevelPressure = 101325)](#float_calculatealtitude(float_pressure,_bool_metric_=_true,_float_sealevelpressure_=_101325))
		** [float CalculateDewPoint(bool metric = true)](#float_calculatedewpoint(bool_metric_=_true))
		** [float CalculateDewPoint(float temp, float hum, bool metric = true)](#float_calculatedewpoint(float_temp,_float_hum,_bool_metric_=_true))
* [Contributing](#contributing)
* [History](#history)
* [Credits](#credits)
* [License](#license)
<snippet>
<content>
## Summary
---
Reads temperature, humidity, and pressure. Calculates altitude and dew point. Provides functions for english and metric. Also reads pressure in Pa, hPa, inHg, atm, bar, torr, N/m^2 and psi.

## Installation
---
To use this library download the zip file, uncompress it to a folder named BME280. Move the folder to {Arduino Path}/libraries.

## Usage
---
Include the library at the top of your Arduino script. `#include <BME280>`
Create a global or local variable. `BME280 bme`
In your start up call `bme.begin()`.
Read the temperature, humidity, pressure, altitude and/or dew point.

`float pres, temp, hum`
`bme.ReadData(pres, temp, hum)`

or

`temp = bme.ReadTemperature()`
`hum = bme.ReadHumidity()`
`pres = bme.ReadPressure()`

`float altitude, dewPoint`
`altitude = bme.CalculateAltitude()`
`dewPoint = bme.CalculateDewPoint()`

## Methods
---

#### BME280(uint8_t tosr = 0x1, uint8_t hosr = 0x1, uint8_t posr = 0x1, uint8_t mode = 0x3, uint8_t st = 0x5, uint8_t filter = 0x0, bool spiEnable = false, uint8_t bme_280_addr = 0x76)
---
  Constructor used to create the class. All parameters have default values.
  Return: None

    * Temperature Oversampling Rate (tosr): uint8_t, default = 0x1
      values: B000 = Skipped, B001 = x1, B010 = x2, B011 = x4, B100 = x8, B101/other = x16

    * Humidity Oversampling Rate (hosr): uint8_t, default = 0x1
      values: B000 = Skipped, B001 = x1, B010 = x2, B011 = x4, B100 = x8, B101/other = x16

    * Pressure Oversampling Rate (posr): uint8_t, default = 0x1
      values: B000 = Skipped, B001 = x1, B010 = x2, B011 = x4, B100 = x8, B101/other = x16

    * Mode: uint8_t, default = forced
      values: Sleep = B00, Normal = B01 and B10, Forced = B11

    * Standby Time (st): uint8_t, default = 1000ms
      values: B000 = 0.5ms, B001 = 62.5ms, B010 = 125ms, B011 = 250ms, B100 = 250ms, B101 = 1000ms, B110 = 10ms, B111 = 20ms

    * Filter: uint8_t, default = None
      values: B000 = off, B001 = 2, B010 = 4, B011 = 8, B100/other = 16

    * SPI Enable: bool, default = false
      values: true = enable, false = disable

    * BME280 Address: uint8_t, default = 0x76
      values: any uint8_t




#### bool  begin()
---
  Method used at start up to initialize the class. Starts the I2C interface.
  Return: bool, true = success, false = failure (no device found)

#### float ReadTemperature(bool celsius = true)
---
  Read the temperature from the BME280 and return a float.
  Return: float = temperature

    * Celsius: bool, default = true
      values: true = return temperature in degrees Celsius, false = return
      temperature in degrees Fahrenheit


#### float ReadPressure(uint8_t unit = 0x0)
---
  Read the pressure from the BME280 and return a float with the specified unit.
  Return: float = pressure

    * Unit: uint8_t, default = 0x0
      values: B000 = Pa, B001 = hPa, B010 = Hg, B011 = atm, B100 = bar,
      B101 = torr, B110 = N/m^2, B111 = psi

#### float ReadHumidity()
---
  Read the humidity from the BME280 and return a percentage as a float.
  Return: float = percent relative humidity

#### void  ReadData(float& pressure, float& temp, float& humidity, bool metric = true, uint8_t p_unit = 0x0)
---
  Read the data from the BME280 with the specified units.
  Return: None, however, pressure, temp and humidity are changed.

    * Pressure: float, reference
      values: reference to storage float for pressure

    * Temperature: float, reference
      values: reference to storage float for temperature

    * Humidity: float, reference
      values: reference to storage float for humidity

    * Metric: bool, default = true
      values: true = meters, false = feet

    * Pressure Unit: uint8_t, default = 0x0
        values: B000 = Pa, B001 = hPa, B010 = Hg, B011 = atm, B100 = bar,
        B101 = torr, B110 = N/m^2, B111 = psi

#### float CalculateAltitude(bool metric = true, float seaLevelPressure = 101325)
---
  Read the data from the BME280 with the specified units and then calculate the altitude.
  Return: float = altitude

    * Metric: bool, default = true
      values: true = meters, false = feet

    * Sea Level Pressure: float, unit = Pa, default = 101325
      values:  any float


#### float CalculateAltitude(float pressure, bool metric = true, float seaLevelPressure = 101325)
---
  Calculate the altitude based on the pressure with the specified units.
  Return: float = altitude

    * Pressure: float, unit = Pa
      values: any float

    * Metric: bool, default = true
      values: true = meters, false = feet

    * Sea Level Pressure: float, unit = Pa, default = 101325
      values:  any float

#### float CalculateDewPoint(bool metric = true)
---
  Read BME280 data and calculate the dew point with the specified units.
  Return: float = dew point

    * Metric: bool, default = true
      values: true = return temperature in degrees Celsius, false = return
      temperature in degrees Fahrenheit

#### float CalculateDewPoint(float temp, float hum, bool metric = true)
---
  Calculate the dew point based on the temperature and humidity with the specified units.
  Return: float = dew point

    * Temperature: float, unit = Celsius if metric is true, Fahrenheit if metric is false
      values: any float

    * Humidity: float, unit = % relative humidity
      values: any float

    * Metric: bool, default = true
      values: true = return degrees Celsius, false = return degrees Fahrenheit

## Contributing
---
1. Fork the project.
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request.

## History
---
Jan 1, 2016 - Version 1.0.0 released.

## Credits
---
Written by Tyler Glenn, 2016.

## License
---
GNU GPL, see License.txt
</content>
</snippet>
