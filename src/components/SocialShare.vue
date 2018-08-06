<template>
	<section class="hero">
		<div class="hero-body">
			<div class="columns is-vcentered">
				<div class="column">
					<h1 class="title has-text-centered is-uppercase">{{ title }}</h1>
				</div>
			</div>
			<div class="columns is-vcentered">
				<div class="column">
					<h2 class="subtitle has-text-centered">{{ description }}</h2>
				</div>
			</div>
			<div class="columns">
				<div class="column has-text-centered">
					<social-sharing
						:url="url"
						:title="title"
						:description="description"
						:quote="description"
						:networks="overriddenNetworks"
						:hashtags="hashtags"
						:twitter-user="username"
						:media="media"
						network-tag="a"
						v-cloak
						inline-template
					>
						<div class="socials">
							<network network="facebook">
								<span class="button is-large" title="Facebook">
									<i class="mdi mdi-facebook"></i>
								</span>
							</network>
							<network network="twitter">
								<span class="button is-large" title="Twitter">
									<i class="mdi mdi-twitter"></i>
								</span>
							</network>
							<network network="whatsapp">
								<span class="button is-large" title="Whatsapp">
									<i class="mdi mdi-whatsapp"></i>
								</span>
							</network>
							<network network="googleplus">
								<span class="button is-large" title="Google+">
									<i class="mdi mdi-google-plus"></i>
								</span>
							</network>
							<network network="linkedin">
								<span class="button is-large" title="LinkedIn">
									<i class="mdi mdi-linkedin"></i>
								</span>
							</network>
							<network network="pinterest">
								<span class="button is-large" title="Pinterest">
									<i class="mdi mdi-pinterest"></i>
								</span>
							</network>
							<network network="telegram">
								<span class="button is-large" title="Telegram">
									<i class="mdi mdi-telegram"></i>
								</span>
							</network>
							<network network="sms">
								<span class="button is-large" title="SMS">
									<i class="mdi mdi-message-text-outline"></i>
								</span>
							</network>
						</div>
					</social-sharing>
				</div>
			</div>
		</div>
	</section>
</template>

<script>
export default {
	name: 'social-share',
    props: {
        hashtags: {
            type: String
        },
        username: {
            type: String
        },
        media: {
            type: String
        },
        useragent: {
            type: String,
            default: 'SmartSolutions'
        }
    },
	data () {
		return {
			url: '',
			overriddenNetworks: {
				"whatsapp": {
					"sharer": "https://api.whatsapp.com/send?text=@description%0D%0A@url",
					"type": "popup"
				},
				"facebook": {
					"sharer": "https://www.facebook.com/dialog/feed?app_id=1928799480767424&display=popup&title=@title&link=@url&redirect_uri=" + encodeURIComponent(window.location.href),
					"type": "popup"
				}
			},
			ios: new RegExp(this.useragent + '-iOS').test(navigator.userAgent)
		}
	},
	created() {
		this.url = document.URL;
		if (this.ios) {
			this.overriddenNetworks = {
				"twitter": {
					"sharer": "twitter://post?text=@title&url=@url&hashtags=@hashtags@twitteruser",
					"type": "direct"
				},
				"telegram": {
					"sharer": "tg://msg?text=@title%20@url%20@description",
					"type": "direct"
				},
				"facebook": {
					"sharer": "https://www.facebook.com/dialog/feed?app_id=1928799480767424&display=page&title=@title&link=@url&redirect_uri=" + encodeURIComponent(window.location.href),
					"type": "direct"
				}
			}
		}
	}
}
</script>

<style scoped>
.column.has-text-centered >>> .button.is-large { margin: 14px; }
.column.has-text-centered >>> .socials { max-width: 356px; margin: 0 auto; }
@media (max-width: 568px) {
	.hero >>> .hero-body { padding-top: 0;}
}
</style>