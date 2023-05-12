<template>
    <div class="modal" v-if="props.visible">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title">{{ props.title }}</h4>
                    <button type="button" class="close" @click="closeModal">
                        <span>➕</span>
                    </button>
                </div>
                <div class="modal-body">
                    <slot></slot>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" @click="closeModal">
                        取消
                    </button>
                    <button type="button" class="btn btn-primary" @click="confirm">
                        确定
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script setup>
import { defineEmits, defineProps } from 'vue';
const props = defineProps({
    title: {
        type: String,
        default: "标题",
    },
    visible: {
        type: Boolean,
        default: false,
    },
})

const emit = defineEmits(["update", "confirm"]);

const closeModal = () => {
    emit("update", props.visible);
}
const confirm = () => {
    emit("confirm");
    emit("update", props.visible);
}
</script>
  
<style scoped lang="less">
.modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1000;
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal-title {
    color: #1211ff;
    font-size: 1rem;
}

.modal-dialog {
    max-width: 600px;
    margin: 0 auto;
    background-color: #fff;
    border: 1px solid #1211ff;
}

.close {
    border: none;
    outline: none;
    cursor: pointer;

    span {
        color: #1211ff;
        display: block;
        background-color: #fff;
        transform: rotate(45deg);
    }
}

.modal-header,
.modal-footer {
    padding: 10px 20px;
    background-color: #fff;
    border-bottom: 1px solid #1211ff;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.modal-header .modal-title {
    margin: 0;
    font-weight: 500;
}

.modal-body {
    padding: 40px;
    color: #1211ff;
}

.modal-footer button {
    margin-left: 10px;
    padding: 6px 12px;
    width: 80px;
    outline: none;
    border: none;
    border-radius: 2px;
    color: #1211ff;
}

.modal-footer button:nth-child(2) {
    background-color: #fff;
    color: #1211ff;
    border: 1px solid #1211ff;
}

.modal-footer button:nth-child(2):hover {
    background-color: #1211ff;
    color: #fff;
}

.modal-footer button:nth-child(1) {
    background-color: #fff;
    color: #1211ff;
    border: 1px solid #1211ff;
}

.modal-footer button:nth-child(1):hover {
    background-color: #1211ff;
    color: #fff;
}</style>