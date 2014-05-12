XAML Coding guidelines
======================

## How to contribute

You can open an issue on this project to raise an issue/argument about an existing rule, or to submit a new rule. For each submission, please at least produce the following items:

- Cause
- Rule description
- Justification
- How to fix violation

You can also add a code sample with violation, and a code sample with violation fixed.

### Want to translate the XAML coding guidelines in another language ?

Sure ! Please create an issue, and we can discuss how we can work on creating multilingual version of these guidelines.

## Guidelines principles

- **Be easy to follow**: Each rule must be explained as simple as possible. Any developer on his/her 1st day with Xaml must be able to follow these rules,
- **Be as uncontroversial as possible**: These rules must be out of debate. We're not here to determine if it's better to have a white-themed Visual Studio or a black-themed one (Pro-Tip: the correct answer is of course black). So, each rule must have a justification. An inspiration from [StyleCop](http://www.stylecop.com/docs/StyleCop%20Rules.html) rules can be useful,
- **Be usable for any Xaml-Based project**: Windows Phone, WPF or Universal apps. It must apply for all of them. If a rule only apply to one platform, it should go under a platform-specific section.


## Rules

### XA1x. Code readability

#### XA1001 - Put one attribute per line
##### **Cause**
Multiple attributes are declared on the same line.

##### **Rule description**
A violation of this rule occurs whenether an element has multiple attributes declared on the same line. For example: 

```xml
<Button x:Name="MyButton" Text="Hello world" Foreground="Blue"  />
```

Quickly, this can leads to *forgotten attributes*, because the XAML code editor is often splitted in two with code view and design view. We could apply a specific rule, like "limit to 60 column caracters" or "limit to 2 attributes per line". However, all these rules create special cases and interpretations that lead to difficulties in implementing this rule in our brain. Therefore, it's more suitable to apply a simple rule anytime.

##### **How to fix violation**
To fix a violation of this rule, place only one attribute per line.

You can also use the default key combo `Ctrl+K, Ctrl+F` to automatically format the current selection/document.

```xml
<Button x:Name="MyButton" 
        Text="Hello world" 
        Foreground="Blue"  />
```

#### XA1002 - Put the first attribute on the element line

##### **Cause**
When an element has at least one attribute defined, the first line contains only the element.

##### **Rule description**
A violation of this rule occurs whenether an element is the only thing declared on the line.

```xml
<Button 
    x:Name="MyButton" 
    Text="Hello world" 
    Foreground="Blue"  />
```

Declaring only the element without one of the attributes can leads to too many carriage return when the element is containing only one attribute. We can't create an exception fo these one-attribute element declarations.

Moreover, adding the attributes on the subsequent leads can lead to a tab alignment which is under the element. This alignment is not relarly optimal for reading.

##### **How to fix violation**
Place the first attribute on the same line as the element opening.
```xml
<Button x:Name="MyButton" 
        Text="Hello world" 
        Foreground="Blue"  />
```

#### XA1003 - Within an element, order attributes alphabetically or with the proposed solution
##### **Cause**
Within an element tag, attributes are unordered.
```xml
<Button Text="Hello world" 
        Foreground="Blue"
        TextAlignment="Center"
        />
```

##### **Rule description**
A violation of this rule occurs whenether attributes within an element are not ordered alphabetically within an element declaration.

**Current proposal and discussions**
There are discussions about this rule. Please see the [related proposal](https://github.com/cmaneu/xaml-coding-guidelines/issues/1).

##### **How to fix violation**
Order all attributes in alphabetical order, with respect of the related rules.

```xml
<Button Foreground="Blue"
        Text="Hello world" 
        TextAlignment="Center"
        />
```


##### **Related rules**

- **XA1004**: Put the x:Name or x:Key
- **XA1005**: Put the attached properties at the beginning of the element, eventually after the x:Name/x:Key

#### XA1004 - Put the x:Name or x:Key
##### **Cause**
Within an element tag, with the attribute `x:Name` or `x:Key` declared, this attribute is not the first declared.

```xml
<Button Text="Hello world" 
        x:Name="ValidationButton"
        TextAlignment="Center"
        />
```

##### **Rule description**
A violation of this rule occurs when an element declare multiple attributes, and at least a `x:Name` or `x:Key` attribute, this attribute must be placed first.

The attributes are more important than any others because:
- They identify the uniqueness of that control, 
- The identify that the control is used elsewere (storybard, code behind, binding, ...), and therefore, any changes made to that control must be done carefully.


##### **Related rules**

- **XA1005**: Put the attached properties at the beginning of the element, eventually after the x:Name/x:Key
- **XA2001**: Name elements with the `x:Name` attribute

##### **How to fix violation**
Place the `x:Name` or `x:Key` attribute first.
```xml
<Button x:Name="ValidationButton"
        Text="Hello world" 
        TextAlignment="Center"
        />
```



#### XA1005 - Put the attached properties at the beginning of the element, eventually after the x:Name/x:Key
##### **Cause**
Attached properties are declared in any order within the element properties.

```xml
<Button x:Name="ValidationButton"
        Text="Hello world" 
        Grid.Column="2"
        Grid.Row="0"
        TextAlignment="Center"
        />
```

##### **Rule description**
A violation of this rule occurs when an element declares attached properties, and their declaration is not at the top of all attributes declarations, except the `x:Name` and `x:Key` attributes.

Attached properties can change the appearence or behavior of your control. They can also surcharge some of the control properties. Declaring them at the top helps you identifiy these cases.

##### **How to fix violation**
Place all the attached properties, in an alphabetical order, first. If `x:Name` and `x:Key` attributes are declared, they are declared before any attached property declaration.

```xml
<Button x:Name="ValidationButton"
        Grid.Column="2"
        Grid.Row="0"
        Text="Hello world" 
        TextAlignment="Center"
        />
```


#### XA1006 - If an element has no content, use a self-closing element
##### **Cause**
##### **Rule description**
##### **How to fix violation**



### XA2x. Naming

#### XA2001 - Name elements with the `x:Name` attribute
#### XA2002 - Use Pascal Casing
#### XA2003 - Suffix XAML names with a type indication
#### XA2004 - Do not use a precise type indication suffix, unless it's required
#### XA2005 - Name only node used in code-behind, element binding or animation




# XA3x. Maintenability

#### XA3001 - Use the rule of 3 to decide if a value must be declared as a resource
#### XA3002 - All the implicit styles must be placed at the top of the file, and must be annotated with a comment




### XA4x. Resource files organization

#### XA4001 - Put the default styles within App.xaml, put the others styles in another file
#### XA4002 - Within a resource file, declare the elements in the following order
#### XA4003 - When defining a SolidColorBrush resource, always define a Color resource as well


## Guidelines authors

Please see [repository contributors](https://github.com/cmaneu/xaml-coding-guidelines/graphs/contributors).


## Work in progress

### Attributes ordering proposal

