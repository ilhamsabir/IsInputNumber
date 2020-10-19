# Is Input Number

This is vue component input number with button handler.
[Live Demo Here](https://vsnp7.csb.app/).


### Installation
```sh
$ npm install -d is-input-number
```

### Setup
##### Global
```javascript
import IsInputNumber from 'is-input-number';

Vue.use(IsInputNumber)

```

### Usage
```html
<template>

	<IsInputNumber
		mode="top-down"
		:max="300"
		:min="1"
		:disabled="false"
		:value.sync="value"
		@change="onChange"
	/>

</template>

<script>
// this for implement on local file
import IsInputNumber from 'is-input-number';

export default {
	// this for implement on local file
	components: {
		IsInputNumber,
	},
	data() {
		value: 1,
	},
	methods: {
		onChange (value) {
			this.value = value;
		}
	}
}
</script>


```

### Style SCSS
```scss
.input-number {
	display: flex;

	.input-number-input-wrap {
		width: 60px;
		// height: 30px;

		/* Chrome, Safari, Edge, Opera */
		input::-webkit-outer-spin-button,
		input::-webkit-inner-spin-button {
			-webkit-appearance: none;
			margin: 0;
		}

		/* Firefox */
		input[type=number] {
			-moz-appearance: textfield;
		}
	}

	.input-number-input {
		box-sizing: border-box;
		list-style: none;
		width: 100%;
		color: rgba(0,0,0,.85);
		font-size: 14px;
		line-height: 1.5715;
		background-color: #fff;
		background-image: none;
		transition: all .3s;
		padding: .3rem .6rem;
		border: 1px solid #d9d9d9;

		height: 100%;
		text-align: center;

		&:disabled,
		&[readonly] {
			background-color: #f5f5f5;
			opacity: 1;
		}

		&.top-down {
			border-radius: 3px;
			border-top-right-radius: 0;
			border-bottom-right-radius: 0;
			border-right: 0;
		}

		&.plus-minus {
			border-radius: 0px;
			border-left: 0;
			border-right: 0;
		}
	}

	.input-plus-minus {
		.input-number-handler {
				padding: .3rem .7rem;
				cursor: pointer;
				font-size: 18px;
				background: #fff;
				border: 1px solid #ddd;
				height: 44px;
				width: 34px;
		}

		.input-number-handler-minus {
			margin-right: -1px;
			border-right: 0px;
		}

		.input-number-handler-plus {
			margin-left: -1px;
			border-left: 0;
		}
	}

	.input-top-down {
		.input-number-handler-wrap {
			display: flex;
			flex-direction: column;
			// border: 1px solid #ddd;
			background: #fff;

			.input-number-handler {
				padding: .3rem .7rem;
				cursor: pointer;
				font-size: 8px;
				background: #fff;
				border: 1px solid #ddd;

				&:hover {
					background: #40a9ff;
					color: #fff;
				}

				&.disabled {
					background: #f5f5f5;
					user-select: none;

					&:hover {
						background: #f5f5f5;
						color: rgb(143, 142, 142);
					}
				}
			}

			.input-number-handler-up {
				border-bottom: 0px solid #ddd;
				border-top-right-radius: 3px;
			}

			.input-number-handler-down {
				border-bottom-right-radius: 3px;
			}
		}
	}
}
```


## Attributes

- __mode:__ Set Default Mode (String) "top-down" or "plus-minus", default 'top-down'.
- __value:__ Add a default value to input (integer), default 0.
- __min:__ Minimum value for input number (integer), default 1.
- __max:__ Maximum value for input number (integer), default 10000000.
- __disabled:__ Set input number disabled (boolean), default false.

## Events

#### @change

Event is fired when value is changed.

## License
MIT license

© 2020 [Ilham Sabir](https://github.com/ilhamsabir)