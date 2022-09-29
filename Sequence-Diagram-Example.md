# Mermaid Sequence Diagram Examples

## Basic sequence diagram example

```mermaid
  sequenceDiagram
  Alice ->> John: Hello John, how are you?
  John -->> Alice: Great!
  Alice -) John: Awesome. See you later!  
```

> **Note:** The word "end" could potentially break the diagram, due to the way that the mermaid language is scripted. If unavoidable, one must use parentheses(), quotation marks "", or brackets {},[], to enclose it.

-----

## Syntax

### Participants

The participants can be defined implicitly as in the first example on this page. The participants or actors are rendered in order of appearance in the diagram source text. Sometimes you might want to show the participants in a different order than how they appear in the first message. It is possible to specify the actor's order of appearance by doing the following:

```mermaid
sequenceDiagram
  participant Alice
  participant Bob
  
  Alice ->> Bob: Hi Bob
  Bob ->> Alice: Hi Alice
```

### Actors

If you specifically want to use the actor symbol instead of a rectangle with text you can do so by using actor statements as per below.

```mermaid
sequenceDiagram
  actor Alice
  actor Bob
  
  Alice ->> Bob: Hi Bob
  Bob ->> Alice: Hi Alice
```

### Aliases

The actor can be assigned to a reference variable.

```mermaid
sequenceDiagram
  participant A as Alice
  participant J as John

  A ->> J: Hello John, how are you?
  J ->> A: I'm fine Alice  
```

-----

## Messages

Messages can be of two displayed either solid or with a dotted line.

Pattern:
`[Actor][Arrow][Actor]:Message text`

| Type | Description                                |
| ---- | ------------------------------------------ |
| ->   | Solid line without arrowhead               |
| -->  | Dotted line without arrowhead              |
| ->>  | Solid line with arrowhead                  |
| -->> | Dotted line with arrowhead                 |
| -x   | Solid line with a cross                    |
| --x  | Dotted line with a cross                   |
| -)   | Solid line with an open arrowhead (async)  |
| --)  | Dotted line with an open arrowhead (async) |

-----

## Activations

It is possible to activate and deactivate an actor. (de)activation can be dedicated declarations:

```mermaid
  sequenceDiagram
    Alice ->> John: Hello John, how are you?
    activate John
    John -->> Alice: Great!
    deactivate John
```

There is also a shortcut notation by appending +/- suffix to the message arrow:

```mermaid
  sequenceDiagram
    Alice ->> +John: Hello John, how are you?
    John -->> -Alice: Great!
```

Activations can be stacked for same actor:

```mermaid
  sequenceDiagram
    Alice ->> +John: Hello John, how are you?
    Alice ->> +John: John, can you hear me?
    John -->> -Alice: Hi Alice, I can hear you.
    John -->> -Alice: I feel great!
```

-----

## Notes

It is possible to add notes to a sequence diagram. This is done by the notation Note [ right of | left of | over ] [Actor]: Text in note content.

```mermaid
  sequenceDiagram
    participant John
    Note right of John: Text in note
```

It is also possible to create notes spanning two participants:

```mermaid
  sequenceDiagram
    Alice -> John: Hello John, how are you?
    Note over Alice, John: A typical interaction
```

-----

## Loops

It is possible to express loops in a sequence diagram. This is done by the notation.

> loop Loop text
> ... statements ...
> end

Example:

```mermaid
  sequenceDiagram
    Alice -> John: Hello John, how are you?
    loop Every minute
      John --> Alice: Great!
    end
```

-----

## Alternative Paths

It is possible to express alternative paths in a sequence diagram. This is done by the notation.

> alt Describing text
> ... statements ...
> else
> ... statements ...
> end

or if there is sequence that is optional (if without else)...

> opt Describing text
> ... statements ...
> end

```mermaid
  sequenceDiagram
    Alice ->> Bob: Hello Bob, how are you?
    alt is sick
      Bob ->> Alice: Not so good :(
    else is well
      Bob ->> Alice: Feeling fresh like a daisy
    end

    opt Extra response
      Bob ->> Alice: Thanks for asking
    end  
```

-----

## Parallels

It is possible to show actions that are happening in parallel. This is done by the notation.

> par [Action 1]
> ... statements ...
> and [Actions 2]
> ... statements ...
> and [Action N]
> ... statements ...
> end

Example:

```mermaid
  sequenceDiagram
    par Alice to Bob
      Alice ->> Bob: Hello guys!
    and Alice to John
      Alice ->> John: Hello guys!
    end

    Bob -->> Alice: Hi Alice!
    John -->> Alice: Hi Alice!
```

It is also possible to nest parallel blocks.

```mermaid
  sequenceDiagram
    par Alice to Bob
      Alice ->> Bob: Go help John
    and Alice to John
      Alice ->> John: I want this done today
      par John to Charlie
        John ->> Charlie: Can we do this today?
      and John to Diana
        John ->> Diana: Can you help us today?
      end 
    end  
```

-----

## Critical Regions

It is possible to show actions that must happen automatically with conditional handling of circumstances. This is done by the notation.

> critical [Action that must be performed]
> ... statements ...
> options [Circumstance A]
> ... statements ...
> option [Circumstance B]
> ... statements ...
> end

Example:

```mermaid
  sequenceDiagram
    critical Establish a connection to the DB
        Service --> DB: connect
    option Network timeout
        Service --> Service: Log error
    option Credentials rejected
        Service --> Service: Log different error
    end
```

It is also possible to have no options at all...

```mermaid
  sequenceDiagram
    critical Establish a connection
      Service --> DB: connect
    end  
```

-----

## Breaks

It is possible to indicate a stop of the sequence within the flow (usually used to model exceptions).

> break
> ... statements ...
> end

Example below:

```mermaid
  sequenceDiagram
    Consumer --> API: Book something
    API --> BookingService: Start booking process
    break when the booking process fails
      API --> Consumer: show failure
    end
    API --> BillingService: Start billing process
```

-----

## Background highlighting

It is possible to highlight flows by providing colored background rects. The colors are defined using rgb and rgba syntax. This is done by the notation:

> rect rgb(0, 255, 0)
> ... content ...
> end

Or...

> rect rgba(0, 0, 255, .1)
> ... content ...
> end

```mermaid
  sequenceDiagram
    participant Alice
    participant John

    rect rgb(191, 223, 255)
    note right of Alice: Alice calls John
    Alice ->> +John: Hello John, how are you?
    
    rect rgb(200, 150, 255)  
    Alice ->> +John: John, can you hear me?
    John -->> -Alice: Hi Alice, I can hear you!
    end

    John -->> -Alice: I feel great!
    end

    Alice ->> +John: Did you want to go to the game tonight?
    John -->> -Alice: Yeah! See you there.
```

-----

## Comments

Comments can be entered within a sequence diagram, which will be ignored by the parser. Comments need to be on their own line, and must be prefaced with ```%%``` (double percent signs). Any text after the start of the comment to the next newline will be treated as a comment, including any diagram syntax.

```mermaid
  sequenceDiagram
    Alice ->> John: Hello John, how are you?
    %% Alice typically doesn't care about the answer to this question
    John -->> Alice: Great!
```

-----

## Entity codes to escape characters

It is possible to escape characters using the syntax exemplified here.

```mermaid
  sequenceDiagram
    A ->> B: I #9829; you!
    B ->> A: I #9829; you #infin; times more!
```

Numbers given are base 10, so ```#``` can be encoded as ```#35```;. It is also supported to use HTML character names.

Because semicolons can be used instead of line breaks to define the markup, you need to use ```#59``` to include a semicolon in message text.

-----

## Sequence Numbers

It is possible to get a sequence number attached to each arrow in a sequence diagram. This can be configured when adding mermaid to the website as shown below:

```markdown
<script>
  mermaid.initialize({ sequence: { showSequenceNumbers: true }, });
</script>
```

It can also be be turned on via the diagram using "autonumber":

```mermaid
  sequenceDiagram
    autonumber
    Alice ->> John: Hello John, how are you?

    loop Healthcheck
      John ->> John: Fighting against sickness
    end

    Note right of John: Rational thoughts!

    John -->> Alice: Great!
    John ->> Bob: How are you?
    Bob -->> John: Jolly good chap!  
```

-----

## Actor menus

Actors can have popup-menus containing individualized links to external pages. For example, if an actor represented a web service, useful links might include a link to the service health dashboard, repo containing the code for the service, or a wiki page describing the service.

This can be configured by adding one or more link lines with the format:

```markdown
  link <actor>: <link-label> @ <link-url>
```

Example:

```mermaid
  sequenceDiagram
    participant Alice
    participant John

    link Alice: Dashboard @ https://dashboard.contoso.com/alice
    link Alice: Wiki @ https://wiki.contoso.com/alice
    link John: Dashboard @ https://dashboard.contoso.com/john
    link John: Wiki @ https://wiki.contoso.com/john

    Alice ->> John: Hello John, how are you?
    John ->> Alice: Great!
    Alice -) John: See you later!
```

### Advanced menu syntax

There is an advanced syntax that relies on JSON formatting. This can be configured by adding the links lines with the format:

```markdown
  links <actor>: <json-formatted link-name link-url pairs>
```

Example:

```mermaid
  sequenceDiagram
    participant Alice
    participant John
    
    links Alice: {"Dashboard": "https://dashboard.contoso.com/alice", "Wiki": "https://wiki.contoso.com/alice"}
    links John: {"Dashboard": "https://dashboard.contoso.com/john", "Wiki": "https://wiki.contoso.com/john"}

    Alice ->> John: Hi John, how are you?
    John -->> Alice: Great!
    Alice -) John: See you later!
```

-----
