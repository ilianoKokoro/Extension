<template>
	<template v-for="[key, mod] of Object.entries(modules)" :key="key">
		<ModuleWrapper
			:mod="mod.default"
			@mounted="onModuleUpdate(key as unknown as KickModuleID, mod.config ?? [], $event)"
		/>
	</template>
</template>

<script setup lang="ts">
import { defineAsyncComponent, provide } from "vue";
import { useStore } from "@/store/main";
import { SITE_CURRENT_PLATFORM } from "@/common/Constant";
import { useActor } from "@/composable/useActor";
import { useCookies } from "@/composable/useCookies";
import { getModule } from "@/composable/useModule";
import { useSettings } from "@/composable/useSettings";
import { useUserAgent } from "@/composable/useUserAgent";
// import { useApp } from ".x/composable/useApp";
import { useUserdata } from "./composable/useUserdata";
import { KickModuleID } from "@/types/kick.module";

const ModuleWrapper = defineAsyncComponent(() => import("@/site/global/ModuleWrapper.vue"));

const store = useStore();
const actor = useActor();
const ua = useUserAgent();

ua.preferredFormat = store.avifSupported ? "AVIF" : "WEBP";
store.setPreferredImageFormat(ua.preferredFormat);
store.setPlatform("KICK", ["7TV"], []);

document.body.setAttribute("seventv-kick", "true");

const cookies = useCookies();
const auth = cookies.get("XSRF-TOKEN");
const sessionToken = cookies.get("session_token");

const user = auth ? await useUserdata(auth, sessionToken) : null;

if (user) {
	const updateIdentity = (data: typeof user) => {
		if (!data || !data.id) return;

		store.setIdentity("KICK", {
			id: data.id.toString(),
			numID: data.id,
			username: data.streamer_channel.slug,
			bio: data.bio,
			email: data.email,
			discord: data.discord,
			facebook: data.facebook,
			instagram: data.instagram,
			tiktok: data.tiktok,
			twitter: data.twitter,
			youtube: data.youtube,
		});

		actor.setPlatformUserID("KICK", data.id.toString());
	};

	//TODO: subscribe for allowing new login

	updateIdentity(user);
}

provide(SITE_CURRENT_PLATFORM, "KICK");
const modules: Record<string, { default: ComponentFactory; config: SevenTV.SettingNode[] }> = import.meta.glob(
	"./modules/**/*Module.vue",
	{
		eager: true,
	},
);
for (const key in modules) {
	const modPath = key.split("/");
	const modKey = modPath.splice(modPath.length - 2, 1).pop();

	modules[modKey!] = modules[key];
	delete modules[key];
}

const settings = useSettings();
function onModuleUpdate(mod: KickModuleID, config: SevenTV.SettingNode[], inst: InstanceType<ComponentFactory>) {
	const modInst = getModule(mod);
	if (!modInst) return;

	settings.register(config);
	modInst.instance = inst;
}
</script>
