<script lang="ts" setup>
let year = new Date().getFullYear();
</script>
<template>
    <v-container class="footer">
        <p class="copyright">
            COPYRIGHT 2023-{{ year }} TOOLS.AOE.TOP ALL RIGHT RESERVED
            <a
                href="https://beian.miit.gov.cn/"
                target="_blank"
                rel="nopener norefoerrer"
                >湘ICP备2021011453号-1</a
            >
        </p>
        <div class="friendly-links-section">
            <p class="friendly-links-title">友情链接</p>
            <BaseFriendlyLinks />
        </div>
    </v-container>
</template>
<script lang="ts">
export default {
    name: "Footer",
};
</script>
<style lang="less" scoped>
.footer {
    font-size: 14px;

    .copyright {
        text-align: center;
        color: rgba(
            var(--v-theme-on-background),
            var(--v-medium-emphasis-opacity)
        );
    }

    .friendly-links-section {
        margin-top: 12px;
    }

    .friendly-links-title {
        text-align: center;
        font-weight: 600;
        letter-spacing: 0.08em;
        color: rgba(
            var(--v-theme-on-background),
            var(--v-medium-emphasis-opacity)
        );
        font-size: 12px;
    }

    a {
        text-decoration: none;
        color: rgba(
            var(--v-theme-on-background),
            var(--v-medium-emphasis-opacity)
        );
    }
}
</style>
