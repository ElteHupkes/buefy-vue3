<template>
    <transition name="fade">
        <article
            v-show="isActive"
            class="message"
            :class="[type, size]"
        >
            <header v-if="$slots.header || title" class="message-header">
                <div v-if="$slots.header">
                    <slot name="header" />
                </div>
                <p v-else-if="title">
                    {{ title }}
                </p>
                <button
                    v-if="closable"
                    type="button"
                    class="delete"
                    @click="close"
                    :aria-label="ariaCloseLabel"
                />
            </header>
            <section class="message-body" v-if="$slots.default">
                <div class="media">
                    <div v-if="computedIcon && hasIcon" class="media-left">
                        <b-icon
                            :icon="computedIcon"
                            :pack="iconPack"
                            :class="type"
                            both
                            :size="newIconSize"
                        />
                    </div>
                    <div class="media-content">
                        <slot />
                    </div>
                </div>
            </section>
            <b-progress
                v-if="autoClose && progressBar"
                :value="remainingTime - 1"
                :max="duration / 1000 - 1"
                :type="type"
                :rounded="false"
            />
        </article>
    </transition>
</template>

<script>
import MessageMixin from '../../utils/MessageMixin.js'

export default {
    name: 'BMessage',
    mixins: [MessageMixin],
    props: {
        ariaCloseLabel: String
    }
}
</script>
