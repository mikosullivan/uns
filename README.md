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

## Example

Configuration files are notorious for growing in complexity as features are
added and third-party modules are developed. Namespace collisions can become a
problem when multiple third-party modules address similar issues.

Consider a settings file for a program that allows for thrid party add-ons.
Without any add-ons, a configuration file might look something like this:

    {
        "direction": 1.023,
        "moment": "delta"
    }

Now suppose that a third party add-on is able to add color features to the
application. It might be reasonable to add a setting like this:

    {
        "direction": 1.023,
        "moment": "delta",
        "color": "red"
    }

The problem there is that a single add-on has taken control of the `color`
setting. That may or not be done with coordination with other add-ons or
with the controlling authority of the program. Multiple add-ons, not written in
coordination with others, might have namespace collisions over that setting.

UNS provides a simple, intuitive technique for avoiding namespace collisions.
Using the existing URI infrastructure, a UNS composed of just the domain name and
a path can unambiguously define a namespace without any coordination with
any other development efforts:

    {
        "direction": 1.023,
        "moment": "delta",
        "idocs.com/color": "red"
    }

If another add-on also contributes to some kind of color feature, it can be
easily added without any namespace collisions:

    {
        "direction": 1.023,
        "moment": "delta",
        "idocs.com/color": "red",
        "foo.com/color": {"level":true}
    }

## Format

A UNS consists of a domain name and path. It should not include queries (i.e.
a question mark followed by a string). Shorter is better, so avoid including
`www.` The path should not include tildes (`~`), because that character is used
in the file name version of the UNS.

So, using the example above, a UNS could be expressed in any of three ways:

| format    | example                 |
|-----------|-------------------------|
| namespace | idocs.com/color         |
| URI       | https://idocs.com/color |
| file name | idocs.com~color         |

As long as the naming rules are followed, the UNS can be losslessly converted
between any of the three formats.