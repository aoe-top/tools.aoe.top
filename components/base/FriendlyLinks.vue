<script lang='ts' setup>
type FriendLink = {
    name: string;
    url: string;
};

const links = ref<FriendLink[]>([])
const pending = ref(true)
const failed = ref(false)

async function loadLinks() {
    try {
        const response = await fetch('https://api.aoe.top/api/friendly/links')
        if (!response.ok) {
            throw new Error(`Failed to load links: ${response.status}`)
        }

        const data = await response.json()
        links.value = Array.isArray(data) ? data : []
    } catch (error) {
        console.error(error)
        failed.value = true
    } finally {
        pending.value = false
    }
}

onMounted(loadLinks)
</script>

<template>
    <div v-if="pending" class="friendly-links-state">友链加载中...</div>
    <div v-else-if="failed" class="friendly-links-state">友链加载失败，请稍后重试。</div>
    <div v-else class="friendly-links-list">
        <a
            v-for="link in links"
            :key="link.url"
            :href="link.url"
            target="_blank"
            rel="noopener noreferrer"
            class="friendly-links-pill"
        >
            {{ link.name }}
        </a>
    </div>
</template>

<style lang='less' scoped>
.friendly-links-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
    margin-top: 12px;
}

.friendly-links-pill,
.friendly-links-state {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 8px 14px;
    border-radius: 999px;
    border: 1px solid rgba(var(--v-theme-on-background), 0.12);
    background: rgba(var(--v-theme-on-background), 0.04);
    color: rgba(var(--v-theme-on-background), var(--v-medium-emphasis-opacity));
    text-decoration: none;
    transition: transform 0.2s ease, border-color 0.2s ease, color 0.2s ease;
}

.friendly-links-pill:hover {
    transform: translateY(-2px);
    border-color: rgba(76, 175, 80, 0.35);
    color: rgb(76, 175, 80);
}

.friendly-links-state {
    width: fit-content;
    margin: 12px auto 0;
}
</style>