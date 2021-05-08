# Annotations

## Custom Annotations

- https://www.baeldung.com/java-custom-annotation
- https://mkyong.com/java/java-custom-annotations-example/
- https://www.javatpoint.com/java-annotation

## Links

- https://dzone.com/articles/creating-custom-annotations-in-java
- https://dzone.com/videos/devnexus2015/how-annotations-work-java?utm_medium=feed&utm_source=feedpress.me&utm_campaign=Feed:%20dzone%2Fjava

## why

- https://stackoverflow.com/questions/4285592/why-java-annotations

## The bad

- https://www.yegor256.com/2016/04/12/java-annotations-are-evil.html

  - there is one big problem with annotations—they encourage us to implement object functionality outside of an object, which is against the very principle of encapsulation.
  - The control is lost (not inverted, but lost!). The object is not in charge any more. It can’t be responsible for what’s happening to it.
  - That’s because we don’t want to duplicate the same code over and over again, right? That’s correct, duplication is bad, but tearing an object apart is even worse.
  - Object composition, which is the most important process in object design, is hidden somewhere behind the scenes.... We must see how our objects are composed. We may not care about how they work, but we must see the entire composition process.

- https://blog.softwaremill.com/the-case-against-annotations-4b2fb170ed67
- https://javadevguy.wordpress.com/2016/01/13/evil-annotations/
- https://dzone.com/articles/are-annotations-bad
- https://doanduyhai.wordpress.com/2012/04/21/magics-is-evil/
- https://blog.softwaremill.com/the-case-against-annotations-4b2fb170ed67
