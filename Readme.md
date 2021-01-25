# Pop LegalServer Notes


Introduce two `html`-formatted Instruction blocks into a Case Profile, and your users can pin important case notes by adding the token, _#POP!_ to the note.

Notes with the special token will pop from the regular collection of case notes into the first instruction. If you placed the first instruction at the top of the Case profile, then the 'Popped' notes will appear at the top of the Case Profile.

## Instructions for case handlers

To pin a note, just write the keyword, "#POP!" at the top of a note. The note will pop from its normal spot up to the container for pinned notes.

Simply edit the note to remove _#POP!_ to restore the note to its original place. 



## Administrator Instructions

Download index.html and open it in your browser for a working example of the code.

1. Add an instruction to a case profile that contains a `<div>` element with a special `id`. This element will serve as the container for pinned notes. 

Make sure you format this instruction as HTML.

```
        <div id="popped-notes-container"
             style="border: 1px black solid"></div>
 

```

2. Add a second instruction at the bottom of the case profile. Make sure to format this instruction as HTML as well.

This instruction contains javascript code. The code finds all the notes with the special keyword, _#POP!_ and moves them into the `<div>` above.

```
                            <script type="text/javascript">

                                var importantNotes = document.evaluate("//div[@class='notes' and div[contains(text(),'#POP!')]]",
                                    document,
                                    null,
                                    XPathResult.ORDERED_NODE_ITERATOR_TYPE, null)

                                var container = document.getElementById("popped-notes-container");
                                var notes = []

                                var nextNode = importantNotes.iterateNext()
                                while (nextNode) {
                                    console.log("adding node.")
                                    notes.push(nextNode);
                                    nextNode = importantNotes.iterateNext()
                                }

                                notes.forEach((note) => {
                                    container.appendChild(note)
                                })



                            </script>

```


## Questions

**Why would I pin case notes?** Staff may wish to highlight certain information, such as "Client prefers text to phone messages, except on Tuesdays, when they're at their aunt's house" that isn't structured enough for a custom field and not necessarily so urgent that it needs a "case alert". 

**Can I change the keyword?** Yes! Find the line `var keyword = "#POP!"` and change the keyword to whatever you like.  



