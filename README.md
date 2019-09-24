# Pretty fast XML parser

* Simple event-based XML parser with minimal copying.
* Designed for high-speed parsing of very large XML files (like OSM XML files).
* Should be pretty fast.

## Usage

```
#include "pfxml.h"

[...]

pfxml::file xml("myfile.xml");

while (xml.next()) {
  const auto& cur = xml.get();
  std::cout << cur.name << std::endl;  // .name is the xml tag name
  std::cout << cur.level << std::endl;  // .level is the tags tree level
  std::cout << cur.attrs.size() << std::endl;  // .attrs contains the parameters
}
```

## String Handling

All strings contained in the current element returned by `xml.get()` above are only valid until `xml.next()` is called. If you need the strings afterwards, you have to copy them. Furthermode, all strings are `const char*` pointers. Keep in mind that something like `cur.name == "mytag"` will not work. You have to compare strings via `strcmp()`.

## Errors

In case the XML was malformed, an exception is thrown.

## Speed

No thorough performance evaluation yet. Searching `switzerland-latest.osm` for the ID of the first defined `<way>` object takes roughly 30 seconds when compiled with `-O3` on an Intel(R) Core(TM) i5 with 2 GHz and a SSD. For comparison, finding the first `<way>` object with GNU grep takes 17 seconds on the same machine.

## TODOs

Performance evaluation, tests. Contributors welcome.
