# UNS

UNS (Universal NameSpace) is a simple format for assigning a unique, universal
namespace to any object using an abbreviated URI.

The concept of using URIs to create namespaces has been around for years. For
example, Java uses a format for package names consist of domain names in
reverse order: com.example.foo. Other namespace conventions use fully qualified
URIs such as `https://www.example.com/foo/bar`.

The problem with using fully qualified domain names is that they have a lot of
clutter. In particular, the scheme (e.g. `https://`) often seems unnecessary.

UNS provides a standard format for assigning namespaces using just the domain
name and path of a URI. Those namespaces can be used in hash keys, file names,
and other settings.

Consider, for example: `idocs.com/color`. That's a simple, readable string.
It's clear that it's within the `idocs.com` domain, and presumably has
something to do with color. It's easily distinguished from, say,
`github.com/foo/color`, which might be a similar but distinct resource.

A UNS consists of a domain name and path. It should not include queries (i.e.
a question mark followed by a string). Shorter is better, so avoid including
`www.` The path should not include tildes (`~`), because that character is used
in the file name version of the UNS.

So, using the example above, a UNS could be expressed in any of three ways:

+---------------------------------------+
| namespace  | idocs.com/color          |
| URI        | https://idocs.com/color  |
| file name  | idocs.com~color          |
+---------------------------------------+

As long as the naming rules are followed, the UNS can be losslessly converted
between any of the three formats.