<!--
  - @copyright Copyright (c) 2019 Georg Ehrke <oc.list@georgehrke.com>
  -
  - @author Georg Ehrke <oc.list@georgehrke.com>
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
	<div>
		<button
			v-if="showMoreButton"
			@click="showMore">
			{{ $t('calendar', 'More') }}
		</button>
		<button
			v-if="showSaveButton"
			class="primary"
			@click="saveThisOnly">
			{{ $t('calendar', 'Save') }}
		</button>
		<button
			v-if="shoUpdateButton"
			class="primary"
			@click="saveThisOnly">
			{{ $t('calendar', 'Update') }}
		</button>
		<button
			v-if="showUpdateOnlyThisButton"
			class="primary"
			@click="saveThisOnly">
			{{ $t('calendar', 'Update this occurrence') }}
		</button>
		<button
			v-if="showUpdateThisAndFutureButton"
			:class="{ primary: forceThisAndAllFuture}"
			@click="saveThisAndAllFuture">
			{{ $t('calendar', 'Update this and all future') }}
		</button>
	</div>
</template>

<script>
export default {
	name: 'SaveButtons',
	props: {
		canCreateRecurrenceException: {
			type: Boolean,
			required: true,
		},
		isNew: {
			type: Boolean,
			required: true,
		},
		forceThisAndAllFuture: {
			type: Boolean,
			required: true,
		},
		showMoreButton: {
			type: Boolean,
			default: false,
		},
	},
	computed: {
		showSaveButton() {
			return this.isNew && !this.canCreateRecurrenceException
		},
		shoUpdateButton() {
			return !this.isNew && !this.canCreateRecurrenceException
		},
		showUpdateOnlyThisButton() {
			return this.canCreateRecurrenceException && !this.forceThisAndAllFuture
		},
		showUpdateThisAndFutureButton() {
			return this.canCreateRecurrenceException
		},
	},
	methods: {
		saveThisOnly() {
			this.$emit('save-this-only')
		},
		saveThisAndAllFuture() {
			this.$emit('save-this-and-all-future')
		},
		showMore() {
			this.$emit('show-more')
		},
	},
}
</script>
