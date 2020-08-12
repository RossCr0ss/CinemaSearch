<template>
    <header class="header">
        <nav class="topnav">
            <button type="button" class="btn" @click="showModal">
                <img src="@/assets/magnifiying-glass.svg" class="search-icon" />
            </button>

            <modal v-show="isModalVisible" @close="closeModal" />
        </nav>
    </header>
</template>

<script>
import Modal from '@/components/Modal'
export default {
    name: 'Header',
    components: {
        Modal,
    },
    data() {
        return {
            isModalVisible: false,
        }
    },
    methods: {
        showModal() {
            this.isModalVisible = true
        },
        closeModal() {
            this.isModalVisible = false
        },
    },
}
</script>

<style lang="scss">
.header {
    background-color: #2b3380;
    padding: 10px 0;

    .topnav {
        overflow: hidden;
        display: flex;
        justify-content: flex-end;
        align-items: center;

        button {
            float: right;
            padding: 6px 10px;
            margin-right: 16px;
            background: transparent;
            font-size: 17px;
            border: none;
            cursor: pointer;

            .search-icon {
                width: 14px;
                height: 14px;
            }
        }

        button:hover {
            background: #ccc;
        }
    }
}
</style>
