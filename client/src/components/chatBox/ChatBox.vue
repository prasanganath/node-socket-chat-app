<template>
<div class="tab-pane message-body active" id="inbox-message-1">
	<top-bar/>

	<div class="message-chat">
	    <div class="chat-body">
	    	<div v-for="msg in messages">
		        <bubble-info v-if="msg.to == me._id" :message="msg"/>
		        <bubble-me v-else :message="msg"/>
	    	</div>
	    </div>

	    <message-input/>
	</div>
</div>
</template>

<script>
	import BubbleInfo from './messages/BubbleInfo.vue'
	import BubbleMe from './messages/BubbleMe.vue'
	import MessageInput from './messages/MessageInput.vue'
    import TopBar from './messages/TopBar.vue'

	export default {
		name: 'ChatBox',
		components: {BubbleInfo, BubbleMe, MessageInput, TopBar},
		data () {
			return {
				messages : [],
			}
		},
		computed: {
			me: function () {
				return window.User
			}
		},
		methods: {

		},

		mounted () {

			// window.socket.on('chat', (msg) => {
				// this.messages.push(msg)
			// })

			// window.socket.on('connect', function () {
					// socket.emit('get-contact', "getcontact")
			// })

			window.Event.$on('send-message', (msg) => {
				socket.emit('send-message', msg);
				this.messages.push(msg)
			})
			// window.socket.on('send-message', (msg) => {
				// console.log(msg)
				// this.messages.push(msg)
			// })

            window.Event.$on('contact-selected', (messages) => {
            	this.messages = messages.messages
            })
		}
	}
</script>