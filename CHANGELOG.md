# Changelog

## vNEXT
### Highlights :tada:
+ **Slinky now has support for React 16.3 features**
  + Use the new Context API with a [statically-typed interface](https://slinky.shadaj.me/docs/context/) [PR #125](https://github.com/shadaj/slinky/pull/125)
+ **Slinky now has support for React Native**, available in the `slinky-native` module. Try it out with [create-react-native-scala-app](https://github.com/shadaj/create-react-native-scala-app.g8)
+ **Slinky now has support for React VR**, available in the `slinky-vr` module. Try it out with [create-react-vr-scala-app](https://github.com/shadaj/create-react-vr-scala-app.g8)
+ Want to write fancier unit tests for your Slinky app? Slinky now comes with an interface for `react-test-renderer`, available under the `slinky-testrenderer` module. [PR #119](https://github.com/shadaj/slinky/pull/119)

### Details
+ The `@react` macro now produces nicer APIs for external components that have default values for all props parameters. [PR #119](https://github.com/shadaj/slinky/pull/119)
+ Add more variations for `ExternalComponent` that support providing a statically-typed interface for the component instance: `ExternalComponentWithRefType`, `ExternalComponentWithAttributesWithRefType`, `ExternalComponentNoPropsWithRefType`, `ExternalComponentNoPropsWithAttributesWithRefType` [PR #119](https://github.com/shadaj/slinky/pull/119)
+ Bring back the `WithRaw` trait, which makes it possible to access the original object of a read value [PR #122](https://github.com/shadaj/slinky/pull/122)
+ Fix exceptions when declaring custom tags and attributes in a component class [PR #118](https://github.com/shadaj/slinky/pull/118)
+ Fix exceptions when reading the null-prototype in Node.js [PR #121](https://github.com/shadaj/slinky/pull/121)

## v0.3.2
+ Improve support for creating custom tags and attributes (see docs for details) [PR #116](https://github.com/shadaj/slinky/pull/116)

## v0.3.1
+ Fix compilation errors when using an `Option` of a component instance in a tag tree [PR #111](https://github.com/shadaj/slinky/pull/111)
+ Reduce warnings for unused imports when using the `@react` macro annotation [PR #112](https://github.com/shadaj/slinky/pull/112)

## v0.3.0
### Highlights
+ Slinky now has **full support for React 16** features such as fragments, portals, and streaming server-side-rendering
+ The tag API has been remodeled to be more efficient and flexible (see https://slinky.shadaj.me/docs/abstracting-over-tags/)
+ The `@react` macro annotation is now compatible with many more use cases, such as pulling values from a companion object, and has improved support in IntelliJ

### Details
+ **BREAKING!**: The package `me.shadaj.slinky` has been renamed to `slinky` [PR #103](https://github.com/shadaj/slinky/pull/103)
+ **BREAKING**: Stateless components that use the `@react` macro annotation must extend the `StatelessComponent` class instead of just `Component` [PR #69](https://github.com/shadaj/slinky/pull/69)
+ **BREAKING**: Callbacks passed to `setState` are now Scala functions, so there is no need to force implicit conversions [PR #71](https://github.com/shadaj/slinky/pull/71)
+ **BREAKING**: The tag construction flow now requires attributes to come before children. In addition, an empty list of attributes is no longer allowed. When generating tags with dynamic attributes, you will now need to construct the tag as `tag(attrs.head, attrs.tail: _*)` to satisfy this requirement [PR #73](https://github.com/shadaj/slinky/pull/73)
+ Add support for portal elements, which were introduced in React 16 [PR #65](https://github.com/shadaj/slinky/pull/65)
+ Greatly improve IntelliJ support for Slinky with special macro annotation behavior [PR #69](https://github.com/shadaj/slinky/pull/69)
+ Add an alternative `apply` method to eliminate compiler warnings when using propless components [PR #70](https://github.com/shadaj/slinky/pull/70)
+ Add better error message when `@react` annotation is used on a component with no `Props` type declaration [PR #72](https://github.com/shadaj/slinky/pull/72)
+ Better support for converting Slinky types to scalajs-react types when an implicit conversion to `ReactElement` is needed [PR #73](https://github.com/shadaj/slinky/pull/73)
+ Large performance gains in tag construction, with over 5x improvements for some components! [PR #73](https://github.com/shadaj/slinky/pull/73)
+ Add missing global HTML attributes: `spellCheck`, `contentEditable`, and `tabIndex` [PR #77](https://github.com/shadaj/slinky/pull/77)
+ Fix compilation errors when trying to use findDOMNode and passing in an annotated component [PR #78](https://github.com/shadaj/slinky/pull/78)
+ Add no-callback forceUpdate and make it available in annotated components [PR #78](https://github.com/shadaj/slinky/pull/78)
+ Fix bugs involving using companion object values from a `@react` annotated component [PR #80](https://github.com/shadaj/slinky/pull/80)
+ Add a `*` tag for external components that can take any attribute [PR #81](https://github.com/shadaj/slinky/pull/81)
+ Add support for error boundaries, which were added in React 16 [PR #82](https://github.com/shadaj/slinky/pull/82)
+ Add support for all `ReactElement` types introduced in React 16, such as numbers and booleans [PR #83](https://github.com/shadaj/slinky/pull/83)
+ Add remaining methods from ReactDOMServer, including those introduced in React 16 [PR #84](https://github.com/shadaj/slinky/pull/84)
+ Add the custom `on` attribute for AMP pages, introduced in React 16 [PR #85](https://github.com/shadaj/slinky/pull/85)
+ Add facade for `React.Children`, including a new type `ReactChildren` for `props.children` [PR #86](https://github.com/shadaj/slinky/pull/86)
+ Add facade for `ReactDOM.unmountComponentAtNode` [PR #88](https://github.com/shadaj/slinky/pull/88)
+ Fix mapping of undefined values in a case class. Such values now do not become a property in the written object [PR #95](https://github.com/shadaj/slinky/pull/95)
+ Add readers for `js.Array[T]` [PR #100](https://github.com/shadaj/slinky/pull/100)
+ Add common supertype `Tag` for all tag elements to allow abstracting over them [PR #101](https://github.com/shadaj/slinky/pull/101)
+ Add common supertype `Attr` with the typeclass `supports[Tag]` to allow abstracting over supported attributes (see `TagTest` for example) [PR #101](https://github.com/shadaj/slinky/pull/101)

## v0.2.0
+ **BREAKING**: Instead of taking key and refs as additional parameters next to props, they are now taken in through the methods `withKey` and `withRef` (components and external components only)
+ **BREAKING**: Introduce the experimental macro annotation `@react` to simplify component and external component creation with auto-generated companion object for a component class (or external component object). This is a major change to how applications with Slinky are written, so please see the notes at the end of the changelog [PR #29](https://github.com/shadaj/slinky/pull/29)
  + **BREAKING**: This change also renames the `Component` class to `ComponentWrapper`. The `Component` class is now used for the `@react` annotation.
+ **BREAKING**: Rename `ExternalComponentWithTagMods` to `ExternalComponentWithAttributes` and take attributes as a curried parameter instead of an extra parameter after `Props` [PR #26](https://github.com/shadaj/slinky/pull/26)
+ **BREAKING**: Introduce `ExternalComponentNoProps` and `ExternalComponentNoPropsWithAttributes` for cases where an external component takes no props [PR #58](https://github.com/shadaj/slinky/pull/58)
+ **BREAKING**: Slinky now expects that the `-P:scalajs:sjsDefinedByDefault` compiler option is enabled in the `@react` macro annotation []
+ Have mouse attributes such as `onMouseDown` take a `MouseEvent` instead of just an `Event` [PR #27](https://github.com/shadaj/slinky/pull/27)
+ Add support for generating `Reader` and `Writer` for sealed traits, value classes, and case objects (through a Magnolia upgrade) [PR #45](https://github.com/shadaj/slinky/pull/45)
+ Fix bug with hot loading not updating instances of readers and writers [PR #49](https://github.com/shadaj/slinky/pull/49)
+ Fix bug with hot loading using the wrong proxy component when there are multiple components classes in the tree [PR #50](https://github.com/shadaj/slinky/pull/50)
+ Add support for reading and writing js.Dynamic (and anything that extends js.Any) [PR #51](https://github.com/shadaj/slinky/pull/51)
+ Add support for reading and writing union types (js.|) [PR #52](https://github.com/shadaj/slinky/pull/52)
+ Slinky's implementation of mapping Scala types to JS types is now available as a separate module `slinky-readwrite` [PR #54](https://github.com/shadaj/slinky/pull/54)
+ Improve type safety of ExternalComponentWithAttributes by restricting the type parameter to tag types [PR #55](https://github.com/shadaj/slinky/pull/55)

### `@react` macro annotation (experimental)
One of Slinky's main goals is to have React components written in Scala look very similar to ES6. In version 0.1.x, Slinky required
extra boilerplate for defining an object that contained `apply` methods and then creating a `Def` inner class that contained the actual component logic.

This version includes the `@react` macro annotation, which makes it possible to directly write the class containing component logic and have Slinky generate
the companion object for constructing component instances. The macro annotation also now generates special `apply` methods when your Props is a case class
so that constructing Scala components looks more similar to JSX, with the Props values directly taken as parameters of the `apply`.

Note that the macro annotation is **experimental** and **not required**. To use the original component style simply replace the `extends Component` with `extends ComponentWrapper` and your
components should continue to function as they did before.

As an example of migrating an existing component to the new macro annotation style, take a simple component that displays a header:
```scala
import me.shadaj.slinky.core.WrapperComponent
import me.shadaj.slinky.web.html._

object HelloMessage extends WrapperComponent {
  case class Props(name: String)
  type State = Unit

  @ScalaJSDefined
  class Def(jsProps: js.Object) extends Definition(jsProps) {
    def render() = {
      div(s"Hello ${props.name}")
    }
  }
}
``` 

to use the new macro annotation style, we essentially extract out the definition class, move the `Props` and `State` types into the class, and extend `Component` instead of `Definition`:
```scala
import me.shadaj.core.{Component, react}
import me.shadaj.slinky.web.html._

@react class HelloMessage extends Component {
  case class Props(name: String)
  type State = Unit
  
  def render() = {
    div(s"Hello ${props.name}")
  }
}
```

If we want to use this component, we now have a new option for constructing it directly passing in the Props values
```scala
HelloMessage(HelloMessage.Props("Shadaj")) // old style
HelloMessage("Shadaj") // now possible!
HelloMessage(name = "Shadaj") // now possible, closest to JSX
```

The `@react` annotation is also available for external components. For external components, the annotation generates the new `apply` method style in the same style as Scala components.
```scala
import me.shadaj.slinky.core.annotations.react
import me.shadaj.slinky.core.ExternalComponent

@react object React3 extends ExternalComponent {
  case class Props(mainCamera: String, width: Int, height: Int,
                   onAnimate: Option[() => Unit] = None, alpha: Boolean = false)

  override val component: js.Object = js.Dynamic.global.React3.asInstanceOf[js.Object]
}
```

this makes it possible to construct the external component as
```scala
React3(mainCamera = "camera", width = 800, height = 800)
```

## v0.1.1
+ Have ExternalComponentsWithTagMods take the tag type as a type parameter instead of an abstract type [PR #19](https://github.com/shadaj/slinky/pull/19)
+ Added support for reading and writing values of type `js.UndefOr[T]` [PR #18](https://github.com/shadaj/slinky/pull/18)
+ Components and external components with a `Props` type of `Unit` can now be constructed without any parameters, instead of having to pass in `()` as props [PR #12](https://github.com/shadaj/slinky/pull/12)
+ Boolean attributes, such as `disabled`, can now be used without specifying a value to closer match JSX. For example, a disabled input can now be constructed as `input(disabled)` without providing the `:= true` [PR #14](https://github.com/shadaj/slinky/pull/14)

## v0.1.0
+ Initial release
