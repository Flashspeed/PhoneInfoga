# This section is under active development

#### `.localScan(InputNumber: string)`

Run local scan on phone number using [phonenumber python library](https://github.com/daviddrysdale/python-phonenumbers).

~~~python3
from phoneinfoga import localScan

number = '+1 555-444-3333'

# Don't forget to specify print option, otherwise it will directly print results
numberScan = phoneinfoga.localScan(number, print=False)
~~~