<script>
  import { tick } from "svelte";

  let text =
    "Nel mezzo del cammin di nostra vita\nmi ritrovai per una selva OSCURA,\nché la diritta via era smarrita.";

  async function handleKeydown(event) {
    if (event.key !== "Tab") return;

    event.preventDefault();

    const { selectionStart, selectionEnd, value } = this;
    const selection = value.slice(selectionStart, selectionEnd);

    const replacement = /[a-z]/.test(selection)
      ? selection.toUpperCase()
      : selection.toLowerCase();

    text =
      value.slice(0, selectionStart) + replacement + value.slice(selectionEnd);

    await tick();
    this.selectionStart = selectionStart;
    this.selectionEnd = selectionEnd;
  }
</script>

<style>
  body {
    padding: 8rem;
  }

  textarea {
    width: 100%;
    height: 200px;
  }
</style>

<body>
  <p>
    Hello, here's a simple tool to lowercase/UPPERCASE text in
    <b>mass.</b>
  </p>
  <p>
    Just select some text and hit the
    <b>
      <code>Tab</code>
    </b>
    key to toggle uppercase
  </p>
  <textarea value={text} on:keydown={handleKeydown} />

</body>
