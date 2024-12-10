
# extracted from the generated Makefile
freeze_modules_input = {
  'importlib._bootstrap': ['/Lib/importlib/_bootstrap.py', 'importlib._bootstrap.h'],
  'importlib._bootstrap_external': ['/Lib/importlib/_bootstrap_external.py', 'importlib._bootstrap_external.h'],
  'zipimport': ['/Lib/zipimport.py', 'zipimport.h'],
  'getpath': ['/Modules/getpath.py', 'getpath.h'],
  'abc': ['/Lib/abc.py', 'abc.h'],
  'codecs': ['/Lib/codecs.py', 'codecs.h'],
  'io': ['/Lib/io.py', 'io.h'],
  '_collections_abc': ['/Lib/_collections_abc.py', '_collections_abc.h'],
  '_sitebuiltins': ['/Lib/_sitebuiltins.py', '_sitebuiltins.h'],
  'genericpath': ['/Lib/genericpath.py', 'genericpath.h'],
  'ntpath': ['/Lib/ntpath.py', 'ntpath.h'],
  'posixpath': ['/Lib/posixpath.py', 'posixpath.h'],
  'os': ['/Lib/os.py', 'os.h'],
  'site': ['/Lib/site.py', 'site.h'],
  'stat': ['/Lib/stat.py', 'stat.h'],
  'importlib.util': ['/Lib/importlib/util.py', 'importlib.util.h'],
  'importlib.machinery': ['/Lib/importlib/machinery.py', 'importlib.machinery.h'],
  'runpy': ['/Lib/runpy.py', 'runpy.h'],
  '__hello__': ['/Lib/__hello__.py', '__hello__.h'],
  '__phello__': ['/Lib/__phello__/__init__.py', '__phello__.h'],
  '__phello__.ham': ['/Lib/__phello__/ham/__init__.py', '__phello__.ham.h'],
  '__phello__.ham.eggs': ['/Lib/__phello__/ham/eggs.py', '__phello__.ham.eggs.h'],
  '__phello__.spam': ['/Lib/__phello__/spam.py', '__phello__.spam.h'],
  'frozen_only': ['/Tools/freeze/flag.py', 'frozen_only.h'],
}

freeze_module_targets = []
foreach k, v : freeze_modules_input
  freeze_module_targets += custom_target('freeze-' + k,
    input: meson.project_source_root() + v[0],
    output: v[1],
    command: [_freeze_module, k, '@INPUT@', '@OUTPUT@'])
endforeach
