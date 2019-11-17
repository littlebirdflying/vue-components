<template>
    <button class="m-button" :class="{[`icon-${iconPosition}`]: true}">
        <m-icon class="icon" v-if="icon" :name="icon"></m-icon>
        <m-icon class="loading" name="loading"></m-icon>
        <div class="content">
            <slot></slot>
        </div>
    </button>
</template>
<script>
    export default {
        // props: ['icon', 'iconPosition']
        props: {
            icon: {},
            iconPosition: {
                type: String,
                default: 'left',
                validator(value) { // 属性检查器
                    return !(value !== 'left' && value !== 'right');
                }
            }
        }
    }
</script>
<style lang="scss">
    @keyframes spin {
        0% {transform: rotate(0deg)}
        100% {transform: rotate(360deg)}
    }
    .m-button {
        font-size: var(--font-size);
        height: var(--button-height);
        padding: 0 1em;
        border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        display: inline-flex;
        justify-content: center;
        align-items: center;
        vertical-align: middle; /*解决按钮上下不对齐的问题，默认是base-line，由inline引起*/
        &:hover {
            border-color: var(--border-color-hover);
        }
        &:active {
            background-color: var(--button-active-bg);
        }
        &:focus {
            outline: none;
        }
        > .icon {
            order: 1;
            margin-right: .1em;
        }
        > .content {
            order: 2;
        }
        &.icon-right {
            > .icon {
                order: 2;
                margin-right: 0;
                margin-left: .1em;
            }
            > .content {
                order: 1;
            }
        }
        .loading {
            animation: spin 2s infinite linear;
        }
    }

</style>
