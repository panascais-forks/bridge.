<template>
    <div>
        <v-overlay
            :style="`display: ${is_visible ? 'block' : 'none'};`"
            @contextmenu="() => is_visible = false"
        >
            <v-menu
                v-model="is_visible"
                :position-x="x_position"
                :position-y="y_position"
                absolute
            >
                <v-list class="context-menu">
                    <v-list-item
                        v-for="(item, i) in items"
                        :key="`${y_position}.${x_position}.${i}`"
                        @click="item.action"
                        dense
                    >
                        <v-list-item-action class="context-action"> {{ item.title }} </v-list-item-action>
                    </v-list-item>
                </v-list>
            </v-menu>
        </v-overlay>
    </div>    
</template>

<script>
    export default {
        name: "context-menu-main",
        data() {
            return {

            }
        },
        computed: {
            is_visible: {
                get() {
                    return this.$store.state.ContextMenu.is_visible;
                },
                set(value) {
                    this.$store.commit("setContextMenuVisibility", value);
                }
            },
            x_position() {
                return this.$store.state.ContextMenu.x_position;
            },
            y_position() {
                return this.$store.state.ContextMenu.y_position;
            },
            items() {
                return this.$store.state.ContextMenu.menu;
            }
        }
    }
</script>

<style>
    .context-menu .context-action {
        margin: 0 !important;
    }
</style>