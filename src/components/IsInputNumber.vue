<template>
	<div class="input-number">

		<div class="input-plus-minus" v-if="mode === 'plus-minus'">
			<button
					type="button"
					aria-label="Decrease Value"
					class="input-number-handler input-number-handler-minus"
					:class="{'disabled': disabled }"
					@click="decrease">
					<span class="icon-input-number-handler">
						-
					</span>
			</button>
		</div>

		<!-- input  -->
		<div class="input-number-input-wrap">
			<input
				class="input-number-input"
				:class="{
					'plus-minus': mode === 'plus-minus',
					'top-down': mode === 'top-down',
				}"
				type="number"
				:disabled="disabled"
				:max="max"
				:min="min"
				v-model="inlineValue"
				@change="onChange($event)">
		</div>

		<div class="input-plus-minus" v-if="mode === 'plus-minus'">
			<button
					type="button"
					aria-label="Increase Value"
					class="input-number-handler input-number-handler-plus"
					:class="{'disabled': disabled }"
					@click="increase">
					<span class="icon-input-number-handler">
						+
					</span>
			</button>
		</div>

		<!-- action button top down -->
		<div class="input-top-down" v-if="mode === 'top-down'">
			<div class="input-number-handler-wrap">
				<!-- increase (+) -->
				<button
					type="button"
					aria-label="Increase Value"
					class="input-number-handler input-number-handler-up"
					:class="{'disabled': disabled }"
					@click="increase">
					<span class="icon-input-number-handler">
						+
					</span>
				</button>
				<!-- decrease (-) -->
				<button
					type="button"
					aria-label="Decrease Value"
					class="input-number-handler input-number-handler-down"
					:class="{'disabled': disabled }"
					@click="decrease">
					<span class="icon-input-number-handler">
						-
					</span>
				</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'input-number',
	props: {
		max: {
			type: Number,
			default: 10000000,
		},
		min: {
			type: Number,
			default: 0,
		},
		step: {
			type: Number,
			default: 1,
		},
		value: {
			type: Number,
			default: 0,
		},
		disabled: {
			type: Boolean,
			default: false,
		},
		mode: {
			type: String,
			default: 'top-down'
		},
	},
	data() {
		return {
			inlineValue: 0,
		};
	},
	watch: {},
	created() {
		this.inlineValue = this.value;
	},
	methods: {
		onChange(e) {
			e.preventDefault();
			let value = e.target.value;
			// eslint-disable-next-line
			if (isNaN(value) || value === '') {
				value = 1;
			}

			if (parseInt(value) > this.max || parseInt(value) < this.min) {
				value = 1;
			}

			this.inlineValue = value;
			this.$emit('change', parseInt(value));
		},

		// on click (+) btn to increase
		increase() {
			if (!this.disabled) {
				if (this.value < this.max) {
					const newValue = this.value + 1;
					this.inlineValue = newValue;
					this.$emit('change', parseInt(newValue));
				}
			}
		},

		// on click (-) btn to decrease
		decrease() {
			if (!this.disabled) {
				const value = this.value;
				let newValue = value;
				if (value !== 0) {
					newValue = value - 1;
				}
				this.inlineValue = newValue;
				this.$emit('change', parseInt(newValue));
			}
		},

	},
};
</script>

<style lang="scss">

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
</style>
