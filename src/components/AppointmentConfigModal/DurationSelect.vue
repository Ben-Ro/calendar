<!--
  - @copyright Copyright (c) 2021 Richard Steinmetz <richard@steinmetz.cloud>
  -
  - @author Richard Steinmetz <richard@steinmetz.cloud>
  -
  - @license GNU AGPL version 3 or any later version
  -
  - This program is free software: you can redistribute it and/or modify
  - it under the terms of the GNU Affero General Public License as
  - published by the Free Software Foundation, either version 3 of the
  - License, or (at your option) any later version.
  -
  - This program is distributed in the hope that it will be useful,
  - but WITHOUT ANY WARRANTY; without even the implied warranty of
  - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
  - GNU Affero General Public License for more details.
  -
  - You should have received a copy of the GNU Affero General Public License
  - along with this program. If not, see <http://www.gnu.org/licenses/>.
  -
  -->

<template>
	<Select
		:label="label"
		:value="value"
		:disabled="disabled"
		:options="options"
		@update:value="$emit('update:value', parseInt($event))" />
</template>

<script>
import Select from './Select'

export default {
	name: 'DurationSelect',
	components: {
		Select,
	},
	props: {
		label: {
			type: String,
			default: '',
		},
		value: {
			type: Number,
			default: 5 * 60,
		},
		disabled: {
			type: Boolean,
			default: false,
		},
		allowZero: {
			type: Boolean,
			default: false,
		},
		max: {
			type: Number,
			default: 60 * 60,
		},
	},
	computed: {
		options() {
			// TODO: shouldn't this use the translatePlural (n) function?
			const options = [
				{ value: 0, label: this.t('calendar', '0 minutes') },
				{ value: 5 * 60, label: this.t('calendar', '5 minutes') },
				{ value: 10 * 60, label: this.t('calendar', '10 minutes') },
				{ value: 15 * 60, label: this.t('calendar', '15 minutes') },
				{ value: 30 * 60, label: this.t('calendar', '30 minutes') },
				{ value: 45 * 60, label: this.t('calendar', '45 minutes') },
				{ value: 60 * 60, label: this.t('calendar', '1 hour') },
				{ value: 2 * 60 * 60, label: this.t('calendar', '2 hours') },
				{ value: 6 * 60 * 60, label: this.t('calendar', '6 hours') },
				{ value: 24 * 60 * 60, label: this.t('calendar', '1 day') },
				{ value: 2 * 24 * 60 * 60, label: this.t('calendar', '2 days') },
				{ value: 7 * 24 * 60 * 60, label: this.t('calendar', '1 week') },
			]
			if (!this.allowZero) {
				options.splice(0, 1)
			}

			return options.filter(option => option.value <= this.max)
		},
	},
}
</script>
