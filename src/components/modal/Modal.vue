<script>
export default {
    props: {
        modalTitle: {
            type: String,
            default: '这是一个模态框'
        }
    },
    template: `
        <div class="modal">
            <div class="modal-header">
                <h4>{{modalTitle}}</h4>
            </div>
            <div class="modal-content">
                <div>
                    <slot name="modal-content">在这里添加内容</slot>
                </div>
            </div>
            <div class="modal-footer">
                <slot name="modal-footer">
                    <input class="btn blue" type="button" value="确定" @click="okHandle" />
                    <input class="btn" type="button" value="取消" @click="cancelHandle" />
                </slot>
            </div>
        </div>
    `,
    methods: {
        okHandle(){
            alert('我触发了');
            this.$emit('on-ok');
        },
        cancelHandle(){
            alert('取消了');
            this.$emit('on-cancel')
        }
    }
}
</script>
<style scoped>
p,h4{ margin:0; }
.modal{ width: 500px;background-color: #fff;border: 1px solid rgba(0,0,0,.2);border-radius: 6px;box-shadow: 0 3px 9px rgba(0,0,0,.5);}
.modal-header { padding: 15px;border-bottom: 1px solid #e5e5e5;}
.modal-content div { padding: 20px;}
.modal-footer { padding: 15px;text-align: right;border-top: 1px solid #e5e5e5;}
.btn {padding: 5px 15px;border: none;outline: none;}
.blue { color: #fff;background-color: #39f;border-color: #39f;}
</style>
