# Lit Element | CMS

Backoffice supports any native Web Components. But we choose to use a little framework to make it simpler.

Render HTML

```
render() {
	return html`The Rabbit went down a <b>bold</b> hole`;
}
```

Bring Styles

```
static styles = [
	css`
		b {
			border-bottom: 2px solid var(--uui-color-divider);
		}
	`,
];
```

Reactive Properties

Parse value as JS properties

Listen to DOM Events

Learn more

Last updated

Was this helpful?