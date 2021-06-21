<template>
	<div v-if="sortedData.length" class="timeline">
		<div class="circle"></div>
		<div class="timeline__item" v-for="item in sortedData" :key="item._id">
			<div class="content">
				<h2
					v-if="item.name.first.length && item.name.last.length"
					class="content__heading"
				>
					{{ fullName(item.name.first, item.name.last) }}
				</h2>
				<div class="content__picture">
					<img :src="`src/assets/profile-pictures/${item.picture}.jpeg`" />
				</div>
				<p v-if="item.registered.length" class="content__date">
					{{ timestamp(item.registered) }}
				</p>
				<p v-if="item.about.length" class="content__about">
					{{ item.about }}
				</p>
				<div v-if="item.tags.length">
					<span class="content__tag" v-for="tag in item.tags" :key="tag">
						{{ tag }}
					</span>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import moment from 'moment';

export default {
	name: 'VerticalTimeline',

	props: {
		inputData: {
			type: Array,
			required: true,
			default: () => [],
		},
		reversed: {
			type: Boolean,
			required: true,
			default: false,
		},
	},
	methods: {
		fullName(first, last) {
			return first + ' ' + last;
		},
		timestamp(date) {
			return moment(date, 'dddd, MMMM Do YYYY, h:mm:ss a').format(
				'MMMM Do YYYY'
			);
		},
	},
	computed: {
		sortedData() {
			const inputData = this.inputData;

			inputData.sort((a, b) => {
				return new Date(a.registered) - new Date(b.registered);
			});

			if (this.reversed) inputData.reverse();

			return inputData;
		},
	},
};
</script>

<style lang="scss">
@import '@/assets/styles/variables.scss';

.circle::before,
.circle::after {
	content: '';
	position: absolute;
	width: 30px;
	height: 30px;
	border-color: $base-font;
	background-color: $base-font;
	border-radius: 50%;
	left: 90%;
	transform: translateX(-50%);
	@media screen and (min-width: 1024px) {
		left: 50%;
	}
}
.circle::after {
	bottom: 0;
}

.timeline {
	position: relative;
	max-width: 1200px;
	margin: 0 auto;
	& * {
		box-sizing: border-box;
	}

	&::after {
		content: '';
		position: absolute;
		width: 6px;
		background-color: $base-font;
		top: 0;
		bottom: 0;
		left: 90%;
		margin-left: -3px;
		@media screen and (min-width: 1024px) {
			left: 50%;
		}
	}
	&__item {
		padding: 10px 40px;
		position: relative;
		background-color: inherit;
		width: 90%;
		@media screen and (min-width: 1024px) {
			width: 50%;
		}
		&::after {
			content: '';
			position: absolute;
			width: 25px;
			height: 25px;
			right: -19px;
			background-color: $base-background;
			border: 6px solid $base-font;
			top: calc(50% - 16px);
			border-radius: 50%;
			z-index: 1;
			@media screen and (min-width) {
				top: calc(50% - 16px);
			}
		}
		&:nth-child(even) {
			left: 0;
			@media screen and (min-width: 520px) {
				&::before {
					content: '';
					position: absolute;
					top: 50%;
					right: 0;
					width: 50%;
					z-index: -1;
					height: 6px;
					background-color: $base-font;
				}
			}
			.content {
				@media screen and (min-width: 520px) {
					padding: 20px 50px 20px 30px;
					margin-right: 60px;
					&::before {
						content: '';
						position: absolute;
						height: 15px;
						width: 15px;
						top: 50%;
						right: -5px;
						background-color: $base-font;
						border: 6px solid $base-font;
						top: calc(50% - 10px);
						border-radius: 50%;
						z-index: 1;
					}
				}
			}
		}
		&:nth-child(odd) {
			@media screen and (min-width: 520px) {
				&::before {
					content: '';
					position: absolute;
					top: 50%;
					right: 0;
					width: 50%;
					z-index: -1;
					height: 6px;
					background-color: $base-font;
					@media screen and (min-width: 1024px) {
						left: 0;
					}
				}
			}
			@media screen and (min-width: 1024px) {
				left: 50%;
			}
			.content {
				@media screen and (min-width: 520px) {
					padding: 20px 50px 20px 30px;
					margin: 0 60px 0 0;
					&::before {
						content: '';
						position: absolute;
						height: 15px;
						width: 15px;
						top: 50%;
						right: -5px;
						background-color: $base-font;
						border: 6px solid $base-font;
						top: calc(50% - 10px);
						border-radius: 50%;
						z-index: 1;
						@media screen and (min-width: 1024px) {
							left: -5px;
						}
					}
				}
				@media screen and (min-width: 1024px) {
					padding: 20px 30px 20px 50px;
					margin: 0 0 0 60px;
				}
			}
			&::after {
				@media screen and (min-width: 1024px) {
					left: -18px;
				}
			}
		}
	}
	.content {
		background-color: $base-background;
		position: relative;
		&__about {
			line-height: 1.6rem;
			text-align: center;
		}
		&__picture img {
			border-radius: 50%;
		}
		&__heading {
			color: $base-font;
		}
		&__date {
			font-size: 1.2em;
			color: $second-font;
			font-weight: 600;
			text-align: center;
		}
		&__tag {
			padding: 5px 10px;
			margin-right: 5px;
			background-color: $base-font;
			font-size: 10px;
			color: $base-background;
			border-radius: 5px;
		}
	}
}
</style>
