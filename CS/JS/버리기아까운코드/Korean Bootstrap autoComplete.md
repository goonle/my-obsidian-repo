Override from [gch1p](https://github.com/gch1p)/**[bootstrap-5-autocomplete](https://github.com/gch1p/bootstrap-5-autocomplete)**

I shouldn't use module.js so need to change it to use Class.
And There was an highlight error for Korean. so i modify code to use it

```javascript
class Autocomplete {
	
	DEFAULTS = {
	  threshold: 1,
	  maximumItems: 5,
	  highlightTyped: true,
	  highlightClass: 'text-warning',
	  label: 'label',
	  value: 'value',
	  showValue: false,
	  showValueBeforeLabel: false,
	};
	
  constructor(field, options) {
	this.field = field;
	this.options = Object.assign({}, this.DEFAULTS, options);
	this.dropdown = null;

	field.parentNode.classList.add('dropdown');
	field.setAttribute('data-bs-toggle', 'dropdown');
	field.classList.add('dropdown-toggle');

	const dropdown = this.ce(`<div class="dropdown-menu"></div>`);
	if (this.options.dropdownClass)
	  dropdown.classList.add(this.options.dropdownClass);

	this.insertAfter(dropdown, field);

	this.dropdown = new bootstrap.Dropdown(field, this.options.dropdownOptions);

	field.addEventListener('click', (e) => {
	  if (this.createItems() === 0) {
		e.stopPropagation();
		this.dropdown.hide();
	  }
	});

	field.addEventListener('input', () => {
	  if (this.options.onInput)
		this.options.onInput(this.field.value);
	  this.renderIfNeeded();
	});

	field.addEventListener('keydown', (e) => {
	  if (e.keyCode === 27) {
		this.dropdown.hide();
		return;
	  }
	  if (e.keyCode === 40) {
		this.dropdown._menu.children[0]?.focus();
		return;
	  }
	});
  }

  setData(data) {
	this.options.data = data;
	this.renderIfNeeded();
  }

  renderIfNeeded() {
	if (this.createItems() > 0)
	  this.dropdown.show();
	else
	  this.field.click();
  }

  createItem(lookup, item) {
	let label;
	if (this.options.highlightTyped) {
	  let idx = this.removeDiacritics(item.label)
		  .toLowerCase()
		  .indexOf(this.removeDiacritics(lookup).toLowerCase());
	  const className = Array.isArray(this.options.highlightClass) ? this.options.highlightClass.join(' ')
		: (typeof this.options.highlightClass == 'string' ? this.options.highlightClass : '');
		//추가로직
		if(this.isKorean(lookup)){
			idx = item.label.indexOf(lookup[0]);
			if(idx == -1){
				var subIdx = item.label.normalize("NFD").indexOf(lookup.normalize('NFD'));
				idx = item.label.normalize('NFD').substring(subIdx, -1).normalize('NFKC').length;
			}
		}
	  label = item.label.substring(0, idx)
		+ `<span class="${className}">${item.label.substring(idx, idx + lookup.length)}</span>`
		+ item.label.substring(idx + lookup.length, item.label.length);
	} else {
	  label = item.label;
	}

	if (this.options.showValue) {
	  if (this.options.showValueBeforeLabel) {
		label = `${item.value} ${label}`;
	  } else {
		label += ` ${item.value}`;
	  }
	}

	return this.ce(`<button type="button" class="dropdown-item" data-label="${item.label}" data-value="${item.value}">${label}</button>`);
  }

  createItems() {
	const lookup = this.field.value;
	if (lookup.length < this.options.threshold) {
	  this.dropdown.hide();
	  return 0;
	}

	const items = this.field.nextSibling;
	items.innerHTML = '';

	const keys = Object.keys(this.options.data);

	let count = 0;
	for (let i = 0; i < keys.length; i++) {
	  const key = keys[i];
	  const entry = this.options.data[key];
	  const item = {
		  label: this.options.label ? entry[this.options.label] : key,
		  value: this.options.value ? entry[this.options.value] : entry
	  };

	  if (this.removeDiacritics(item.label).toLowerCase().indexOf(this.removeDiacritics(lookup).toLowerCase()) >= 0) {
		items.appendChild(this.createItem(lookup, item));
		if (this.options.maximumItems > 0 && ++count >= this.options.maximumItems)
		  break;
	  }
	}

	this.field.nextSibling.querySelectorAll('.dropdown-item').forEach((item) => {
	  item.addEventListener('click', (e) => {
		let dataLabel = e.currentTarget.getAttribute('data-label');
		let dataValue = e.currentTarget.getAttribute('data-value');

		this.field.value = dataLabel;

		if (this.options.onSelectItem) {
		  this.options.onSelectItem({
			value: dataValue,
			label: dataLabel
		  });
		}

		this.dropdown.hide();
	  })
	});

	return items.childNodes.length;
  }
  
	  /**
	 * @param html
	 * @returns {Node}
	 */
	ce(html) {
	  let div = document.createElement('div');
	  div.innerHTML = html;
	  return div.firstChild;
	}

	/**
	 * @param elem
	 * @param refElem
	 * @returns {*}
	 */
	insertAfter(elem, refElem) {
	  return refElem.parentNode.insertBefore(elem, refElem.nextSibling);
	}

	/**
	 * @param {String} str
	 * @returns {String}
	 */
	removeDiacritics(str) {
	  return str
		  .normalize('NFD')
		  .replace(/[\u0300-\u036f]/g, '');
	}
	
	isKorean(str){
		let kor = str.normalize('NFD').replace(/[\u3131-\uD7a3]/g,'');
		return kor.length > 0;
	}

}
```

[from : bootstrap 4 autocomplete](https://github.com/Honatas/bootstrap-4-autocomplete/blob/master/dist/bootstrap-4-autocomplete.js)
[from : bootstrap 5 autocomplete](https://github.com/gch1p/bootstrap-5-autocomplete/blob/master/autocomplete.js)

