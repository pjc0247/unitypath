unitypath
====

플랫폼별로 분기해서 알맞은 유니티 경로를 찾아주는 gemmmmggem

Install
----
```
gem install unitypath
```

Usage
----
```rb
require 'unitypath'

puts unitypath # "C:\\Program Files (x86)\\Unity\\Editor\\Unity.exe"
```

Sourcecode
----
```rb
require 'rbconfig'

def unitypath
  unity_x64 = "C:\\Program Files\\Unity\\Editor\\Unity.exe"
  unity_x86 = "C:\\Program Files (x86)\\Unity\\Editor\\Unity.exe"
  unity_mac = "/Applications/Unity/Unity.app/Contents/MacOS/Unity"

  case RbConfig::CONFIG['host_os']
    when /mswin|windows|w32/i
      return unity_x64 if File.exist? unity_x64
      return unity_x86 if File.exist? unity_x86
    when /darwin/i
      return unity_mac if File.exist? unity_mac    
  end  

  raise RuntimeError.new("Cannot find unity")
end
```
