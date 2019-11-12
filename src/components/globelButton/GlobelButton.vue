<script>
export default {
    template: `
    <div>
        <slot name="first"></slot>
        <button type="button" :style="style" @click="changeBg">
            {{title}}
        </button>
        <slot name="last"></slot>
    </div>
    `
    ,
    created(){
        const styled = this.styled || {};
        if(!styled) return;
        if(styled instanceof Object || JSON.stringify(styled) !== '{}'){
            for(let key in styled){
                this.style[key] = styled[key];
            }
        }
    },
    data(){
        return {
            style: {
                backgroundColor: '#b50136',
                fontSize: '12px',
                color: '#fff'
            }
        }
    },
    methods: {
        changeBg(){
            this.style.backgroundColor = 'green';
            this.$emit('change-color', 'green');
        }
    },
    props: {
        title: {
            type: String,
            default: function(){
                return '暂未定义title'
            }
        },
        styled: {
            type:Object,
            default: function(){
                return {}
            }
        }
    }
}
</script>
