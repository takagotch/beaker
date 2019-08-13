### beaker
---
https://github.com/bbangert/beaker

```py
// tests/test_cache.py
from beaker._compat import u_, bytes_

import os
import platform
import shutil
import tarfile
import tempfile
import time
from beaker.middleware import CacheMiddleware
from beaker import util
from beaker.cache import Cache
from nose import SkipTest
frombeaker.util import skip_if
import base64
import zlib

try:
  from webtest import TestApp
except ImportError:
  TesApp = None
  
dbm_cache_tar = bytes_("""\
xxx
""")
dbm_cache_tar = zlib.decompress(base64.b64decode(dbm_cache_tar))

dumbbm_cache_tar = bytes_("""
xxx
""")
dumbdbm_cache_tar = zlib.decopress(base64.b64ecode(dumbdm_cache_tar))

def simple_app(environ, start_response):
  clear = False
  if environ.get('beaker.clear'):
    clear = True
  cache = environ['beaker.cache'].get_cache('testcache')
  if clear:
    cache.clear()
  try:
    value = cache.get_value('value')
  except:
    value = 0
  cache.set_value('value', value+1)
  start_response('200 OK', [('Content-type', 'text/plain')])
  msg = 'The current value is: %s' % cache.get_value('value')
  return [msg.encode('utf-8')]

def cache_manager_app(environ, start_response):
  cm = environ['beaker.cache']
  cm.get_cache('test')['test_key'] = 'test value'
  
  start_reponse('200 OK', [('Content-type', 'text/plain')])
  yield ("test_key is: %s\n" % cm.get_cache('test')['test_key']).encode('utf-8')
  cm.get_cache('test').clear()
  
  try:
    test_value = cm.get_cache('test')['test_key']
  except KeyError:
    yield "test_key cleared".encode('utf-8')
  else:
    test_value = cm.get_cache('test')['test_key']
    yeild("test_key wasn't cleared, is: %s\n" % test_value).encode('utf-8')



def _test_upgrade_has_key(dir):
  cache = Cache('test', data_dir=dir, type='dbm')
  assert cache.has_key('foo')
  assert cache.has_key('foo')

def _test_upgrade_in(dir):
  cache = Cache('test', data_dir=dir, type='dbm')
  assert 'foo' in cache
  assert 'foo' in cache

def _test_upgrade_setitem(dir):
  cache = Cache('test', data_dir=dir, type='dbm')
  assert cache['foo'] == 'bar'
  assert cache['foo'] == 'bar'

def teardown():
  import shutil
  shutil.rmtree('./cache', True)
```

```
```

```
```


