## Steelcon16 Arduino Build Environment

This is a simple vagrant config to allow development of the Arduino provided within the Steelcon16 goodiebag.

To use this, simply install vagrant and virtualbox extension pack, and then run the following:

```
git clone https://github.com/xpn/vagrant-arduino.git
cd vagrant-arduino
vagrant up
```

If you would like to compile and upload the simple echo demo, then you can run:

```
vagrant ssh
sudo platformio run -d /arduino/ --target upload
sudo cat /dev/ttyUSB0
```
