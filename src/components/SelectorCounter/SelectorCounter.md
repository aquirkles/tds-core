## Minimal usage

```
<SelectorCounter />
```

## Disabled


```
<SelectorCounter disabled />
```

## Success


```
<SelectorCounter successful />
```

## Invalid


```
<SelectorCounter invalid />
```

## Accessibility

Customizing the incrementor and decrementor labels is a helpful way to accurately describe a Selector Counter’s controls, especially when there are more than one present on the page.

The component exposes a focus() method that you can call to place the cursor in the number field.

### Contextual prefix and suffix

The contextPrefix and contextSuffix props can be used to define text that helps the user understand changes in the field’s value. For example, this code produces a field whose value is announced as “You chose [number] smartphone plans” whenever the number changes.

The contextual prefix & suffix can be used together or separately. They’re also optional - if an accessible field can be built using the standard label/description/aria markup, then use those first.

```
initialState = {
  succeeded: false,
  curr: 0
};

const handleNumber = (curr) => {
  setState({curr, succeeded: false});
};

const handleSubmit = (e) => {
  e.preventDefault();

  state.invalid = (state.curr === 5);
  setState({ succeeded: !invalid});

  if (state.invalid) {
    this.counter.focus();
  }
};

const successful = state.succeeded;
const invalid = (state.curr === 5);

const listError = invalid? 'list--error':'';
const listChecked = successful? 'list--checked':'';

const fieldError = invalid? 'field--error':'';
const fieldSuccess = successful? 'field--success':'';

const helperError = invalid? 'helper--error':'';
const helperSuccess = successful? 'helper--success':'';

<form onSubmit={handleSubmit}>
  <div className={`field ${fieldError} ${fieldSuccess}`}>
    <label htmlFor="ex-selcounter">How many smartphone plans?</label>
    <div id="ex-selcounter-desc">
      <p className="text--small">Instructions</p>
      <ul className={`list list--compact ${listError} ${listChecked}`}>
        <li className="list__item">Do not pick 5</li>
      </ul>
    </div>
    <SelectorCounter
      ref={(counter) => this.counter = counter}
      id="ex-selcounter"
      incrementorLabel="Add a plan"
      decrementorLabel="Remove a plan"
      onChange={handleNumber}
      invalid={invalid}
      successful={successful}
      aria-described-by="ex-selcounter-desc"
      contextPrefix="You chose"
      contextSuffix="smartphone plans"
     />
  </div>
  <button className="button button--primary">Submit</button>
</form>
```