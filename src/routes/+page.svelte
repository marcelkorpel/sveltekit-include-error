<script lang="ts">
  import OrderedMap from "orderedmap";
  import type {MarkSpec, NodeSpec} from "prosemirror-model";
  import {Schema} from "prosemirror-model";

  const documentNode: NodeSpec = {
    content: 'block+'
  };

  const paragraphNode: NodeSpec = {
    content: 'inline*',
    group: 'block',
    parseDOM: [{tag: 'p'}],
    toDOM() {
      return ['p', 0];
    }
  };

  const textNode: NodeSpec = {
    group: 'inline'
  };

  const emMark: MarkSpec = {
    parseDOM: [{tag: 'i'}, {tag: 'em'}, {style: 'font-style=italic'}],
    toDOM() {
      return ['em'];
    }
  }

  const nodes: OrderedMap<NodeSpec> = OrderedMap.from({
    doc: documentNode,
    paragraph: paragraphNode,
    text: textNode,
  });

  const marks: OrderedMap<MarkSpec> = OrderedMap.from({
    em: emMark
  });

  const schema = new Schema({
    nodes: nodes,
    marks: marks
  });
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
