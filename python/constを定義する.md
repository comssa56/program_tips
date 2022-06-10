# const‚ğ’è‹`‚·‚é
python‚É‚Íconst‚Æ‚¢‚¤ŠT”O‚ª‚È‚¢B  
‚»‚ñ‚È¢ŠE‚É‚à–³—‚â‚èconst‚ğì‚èo‚·p‚ª‚ ‚Á‚½B

Ql:
http://code.activestate.com/recipes/414140-constant-types-in-python/

```python
# const.py
class _consttype:
    class _ConstTypeError(TypeError):
        pass
    def __repr__(self):
        return "Constant type definitions."
    def __setattr__(self, name, value):
        v = self.__dict__.get(name, value)
        if type(v) is not type(value):
            raise self._ConstTypeError, "Can't rebind %s to %s" % (type(v), type(value))
        self.__dict__[name] = value
    def __del__(self):
        self.__dict__.clear()

import sys
sys.modules[__name__] = _consttype()
```
```python
# another.py
import const

const.A = 1
const.B = 'test'
const.A = 2 # raise self._ConstTypeError,
```


