<script>
export default {
    props: {
        level: Number,
        required: true
    },
    render(createElement){
        return createElement(
            'h'+this.level,
            this.$slots.default
        )
    },
    mounted(){
        console.log(this.$slots)
    }
}
</script>
