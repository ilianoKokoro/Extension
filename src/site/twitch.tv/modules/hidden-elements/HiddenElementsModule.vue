<template />

<script setup lang="ts">
import { watchEffect } from "vue";
import { declareModule } from "@/composable/useModule";
import { declareConfig } from "@/composable/useSettings";
import { hiddenElementSettings } from "./hiddenElements";

const { markAsReady } = declareModule("hidden-elements", {
	name: "Hidden Elements",
	depends_on: [],
});

watchEffect(() => {
	hiddenElementSettings.forEach((setting) => {
		document.body.classList.toggle(setting.class, setting.isHidden.value);
	});
});

markAsReady();
</script>

<script lang="ts">
/**
 * Settings configuration for hidden elements feature
 */
export const config = [
	// Chat elements
	declareConfig("layout.hide_channel_leaderboard", "TOGGLE", {
		path: ["Site Layout", "Chat"],
		label: "Hide Channel Leaderboard",
		hint: "If checked, the channel leaderboard at the top of chat will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_chat_input_box", "TOGGLE", {
		path: ["Site Layout", "Chat"],
		label: "Hide Chat Input Box",
		hint: "If checked, the 'Send a message' chatbox will be hidden (WARNING! the 7tv icon will disappear but can be accessed again at the top right of Twitch)",
		defaultValue: false,
	}),
	declareConfig("layout.hide_buttons_below_chatbox", "TOGGLE", {
		path: ["Site Layout", "Chat"],
		label: "Hide Buttons Below Chatbox",
		hint: "If checked, the buttons below the chatbox will be hidden (such as channel points, settings, 'chat', etc.)",
		defaultValue: false,
	}),
	declareConfig("layout.hide_stream_chat_bar", "TOGGLE", {
		path: ["Site Layout", "Chat"],
		label: "Hide Stream Chat Bar",
		hint: "If checked, the bar above chat which says 'Stream Chat' will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_community_highlights", "TOGGLE", {
		path: ["Site Layout", "Chat"],
		label: "Hide Community Highlights",
		hint: "If checked, community highlights at the top of chat will be hidden (such as hype trains, pinned messages, drops, etc.)",
		defaultValue: false,
	}),
	declareConfig("layout.hide_community_challenge_contributions", "TOGGLE", {
		path: ["Site Layout", "Chat"],
		label: "Hide Community Challenge Contributions",
		hint: "If checked, community challenge contribution notifications in the chat will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_pinned_hype_chats", "TOGGLE", {
		path: ["Site Layout", "Chat"],
		label: "Hide Pinned Hype Chats",
		hint: "If checked, the list of recent hype chats will be hidden",
		defaultValue: false,
	}),
	declareConfig("chat.hide_timestamps_vods", "TOGGLE", {
		label: "Hide VOD Timestamps",
		path: ["Chat", "VODs"],
		hint: "If checked, timestamp for chat will be hidden",
		defaultValue: false,
	}),
	// Main page elements (Twitch Features)
	declareConfig("layout.hide_bits_buttons", "TOGGLE", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Bits Buttons",
		hint: "If checked, the 'Bits' related buttons will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_hype_chat_button", "TOGGLE", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Hype Chat Button",
		hint: "If checked, the 'Hype Chat' related button will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_subscribe_button", "TOGGLE", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Subscribe Buttons",
		hint: "If checked, the 'Subscribe' buttons will be hidden under stream and in theater mode (includes 'gift a sub' button)",
		defaultValue: false,
	}),
	declareConfig("layout.hide_prime_offers", "TOGGLE", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Prime Offers",
		hint: "If checked, the 'Prime Offers' button on the top bar will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_unfollow_button", "TOGGLE", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Unfollow Button",
		hint: "If checked, the 'Unfollow' button will be hidden (under stream and in theater mode)",
		defaultValue: false,
	}),
	declareConfig("layout.hide_live_notification_button", "TOGGLE", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Live Notification Button",
		hint: "If checked, the 'Turn notifications off/on' button under the stream will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_channel_point_balance_button", "TOGGLE", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Channel Point Balance Button",
		hint: "If checked, the channel point balance button under the chat input box will be hidden",
		defaultValue: false,
	}),
	// Side bar elements
	declareConfig("layout.hide_recommended_channels", "TOGGLE", {
		path: ["Site Layout", "Sidebar"],
		label: "Hide Recommended Channels",
		hint: "If checked, the 'recommended channels' section of the side bar will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_viewers_also_watch", "TOGGLE", {
		path: ["Site Layout", "Sidebar"],
		label: "Hide Viewers Also Watch",
		hint: "If checked, the 'viewers also watch' section of the side bar will be hidden",
		defaultValue: false,
	}),
	// Player elements
	declareConfig("layout.hide_top_bar_of_stream", "TOGGLE", {
		path: ["Site Layout", "Video Player"],
		label: "Hide Top Bar of Stream",
		hint: "If checked, the top bar of the stream which shows on hover will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_player_controls", "TOGGLE", {
		path: ["Site Layout", "Video Player"],
		label: "Hide Player Controls",
		hint: "If checked, the controls shown at the bottom of a stream on hover will be hidden",
		defaultValue: false,
	}),
	declareConfig("player.hide_player_extensions", "TOGGLE", {
		path: ["Player", ""],
		label: "Hide Player Extensions",
		hint: "If checked, the player extensions will be hidden",
		defaultValue: false,
	}),
	declareConfig("player.hide_onscreen_celebrations", "TOGGLE", {
		path: ["Player", ""],
		label: "Hide On-Screen Celebrations",
		hint: "If checked, on-screen celebrations will be hidden",
		defaultValue: false,
	}),
	declareConfig("layout.hide_whispers", "DROPDOWN", {
		path: ["Site Layout", "Twitch Features"],
		label: "Hide Whispers",
		hint: "Choose when to hide whispers, fullscreen means when chat is hidden",
		options: [
			["Never", 0],
			["Fullscreen", 1],
			["Allways", 2],
		],
		defaultValue: 0,
	}),
	declareConfig("layout.hide_stories", "TOGGLE", {
		path: ["Site Layout", "Sidebar"],
		label: "Hide Stories",
		hint: "If checked, Stories will be hidden from the side bar",
		defaultValue: false,
	}),
];
</script>

<style lang="scss">
.seventv-hide-buttons-below-chatbox {
	div[data-test-selector="chat-input-buttons-container"] {
		display: none !important;
	}
}

.seventv-hide-stream-chat-bar {
	button[data-a-target="right-column__toggle-collapse-btn"],
	div[class$="stream-chat-header"] {
		display: none !important;
	}
}

.seventv-hide-leaderboard {
	section[data-test-selector="chat-room-component-layout"] > div:first-child > div:first-child {
		display: none !important;
	}
}

.seventv-hide-bits-buttons {
	button[data-a-target="bits-button"],
	button[data-a-target="top-nav-get-bits-button"] {
		display: none !important;
	}
}

.seventv-hide-hype-chat-button {
	button[aria-label="Hype Chat"] {
		display: none !important;
	}
}

.seventv-hide-top-bar-of-stream {
	div[class$="top-bar"] {
		display: none !important;
	}
}

.seventv-hide-player-controls {
	div[data-a-target="player-controls"] {
		display: none !important;
	}
}

.seventv-hide-community-highlights {
	div[class^="community-highlight-stack"] {
		display: none !important;
	}
}

.seventv-hide-community-challenge-contributions {
	div[msg-id*="community-challenge-contribution"] {
		display: none !important;
	}
}

.seventv-hide-pinned-hype-chats {
	div[class$="paid-pinned-chat-message-list"] {
		display: none !important;
	}
}

.seventv-hide-timestamps-vods {
	div[class$="vod-message__header"],
	.seventv-chat-vod-message-timestamp {
		display: none !important;
	}
}

.seventv-hide-recommended-channels {
	div[class$="side-nav--collapsed"]
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(3)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(2)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(3) {
		display: none !important;
	}

	div[class$="side-nav--expanded"]
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(3)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(2)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(4) {
		display: none !important;
	}
}

.seventv-hide-viewers-also-watch {
	div[class$="side-nav--collapsed"]
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(3)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(2)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(4) {
		display: none !important;
	}

	div[class$="side-nav--expanded"]
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(3)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(2)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(1)
		> *:nth-child(5) {
		display: none !important;
	}
}

.seventv-hide-prime-offers {
	div[class$="top-nav__prime"] {
		display: none !important;
	}
}

.seventv-hide-unfollow-button {
	button[data-test-selector="unfollow-button"] {
		display: none !important;
	}
}

.seventv-hide-live-notification-button {
	button[data-a-target="notifications-toggle"] {
		display: none !important;
	}
}

.seventv-hide-subscribe-button {
	button[data-a-target="subscribed-button"],
	button[data-a-target="subscribe-button"] {
		display: none !important;
	}
}

.seventv-hide-chat-input-box {
	div[class$="chat-input__textarea"] {
		display: none !important;
	}
}

.seventv-hide-channel-point-balance-button {
	.community-points-summary {
		display: none !important;
	}
}

/* stylelint-disable */
.seventv-hide-player-ext {
	.video-player .extension-taskbar,
	.video-player .extension-container,
	.video-player .extensions-dock__layout,
	.video-player .extensions-notifications,
	.video-player .extensions-video-overlay-size-container {
		display: none !important;
	}
}

.seventv-hide-onscreen-celebrations {
	div.celebration__overlay {
		display: none !important;
	}
}

.seventv-hide-whispers-fullscreen {
	div.whispers-open-threads:not(.whispers--right-column-expanded-beside) {
		display: none !important;
	}
}

.seventv-hide-whispers-all {
	div.whispers-open-threads {
		display: none !important;
	}
}

.seventv-hide-stories {
	div[class$="storiesLeftNavSection--csO9S"] {
		display: none !important;
	}
	button:has(div[class$="storiesLeftNavSectionCollapsedButton--txKvw"]) {
		display: none !important;
	}
}
/* stylelint-enable */
</style>
