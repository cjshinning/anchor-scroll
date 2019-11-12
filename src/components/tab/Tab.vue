<script>
    export default {
        data:function(){
            return {
                switchIndex:0,
                flag:false
            }
        },
        components:{
            "tab-nav":{
                props:{
                    customClass:String
                },
                template:"<div class='tab-nav' v-bind:class='customClass'><slot></slot></div>"
            },
            "nav-item":{
                props:{
                    customClass:String
                },
                template:"<div class='nav-item' v-bind:class='customClass'><slot></slot></div>"
            },
            "tab-panel":{
                props:{
                    customClass:String
                },
                template:"<div class='tab-panel tab-content'  v-bind:class='customClass'><slot></slot></div>"
            },
            "panel-item":{
                props:{
                    customClass:String
                },
                template:"<div class='wrapper-tabContent tab-pane' v-bind:class='customClass'><slot></slot></div>"
            }
        },
        props:{
            "index":{
                default:0
            },
            "type":{
                default:"simple"
            },
            "navClass":{
                default:""
            },
            panelClass:{
                default:""
            }
        },
        methods:{
            switchChange:function(index){
                var _self = this;
                _self.switchIndex=index;
                _self.$emit("change",index)
            },
            renderRich(createElement){
                var _self=this,$items=_self.$slots["tab-item"],$childNavs=[],$childContents=[],$contentFixed=_self.$slots["tab-panel-fixed"];

                var _=_self._;


                $childContents.push(createElement("panel-item",{
                    props:{
                        customClass:"tab-fixed"
                    }
                },$contentFixed));

                if(!_self.flag){
                    _.forEach($items,function(item,itemIndex){
                        if(!_self.flag&&item.data["attrs"]&&item.data["attrs"].active!==undefined){
                            _self.switchIndex=itemIndex;
                            return false;
                        }
                    });
                    _self.flag=true;
                }



                for(var itemIndex=0,len=$items.length;itemIndex<len;itemIndex++){

                    _.forEach($items[itemIndex]["children"],function(_child){
                        if(_child.data){
                            if(_child.data["slot"]=="nav"){
                                $childNavs.push(createElement('nav-item',{
                                    props:{
                                        customClass:[_child.data.staticClass||"",itemIndex==_self.switchIndex?"active":""].join(" "),
                                    },
                                    nativeOn:{
                                        click:_self.switchChange.bind(this,itemIndex)
                                    }
                                },_child.children));
                            }else if(_child.data["slot"]=="panel"){
                                $childContents.push(createElement("panel-item",{
                                    props:{
                                        customClass:[_child.data.staticClass||"",itemIndex==_self.switchIndex?"active":""].join(" "),
                                    },
                                },_child.children));
                            }
                        }
                    })
                }

                return createElement("div",{
                    class:"tab"
                },[
                    createElement("tab-nav",{
                        props: {
                            customClass: _self.navClass
                        }
                    },$childNavs),
                    createElement("tab-panel",{
                        props:{
                            customClass:_self.panelClass
                        }
                    },$childContents)
                ]);
            },
            renderSimple(createElement){
                var _self=this, $items=this.$slots["tab-item"]||[],
                    itemsIndex=0,itemsLen=$items.length,$childTitle=[],$childContent=[],$contentFixed=_self.$slots["tab-panel-fixed"];
                $childContent.push(createElement("panel-item",{
                },$contentFixed));
                var _=_self._;
                if(!_self.flag){
                    _.forEach($items,function(item,itemIndex){
                        if(!_self.flag&&item.data["attrs"]&&item.data["attrs"].active!==undefined){
                            _self.switchIndex=itemIndex;
                            return false;
                        }
                    });
                    _self.flag=true;
                }
                for(;itemsIndex<itemsLen;itemsIndex++){
                    $childTitle.push(createElement("li",{
                        class:{
                            active:this.switchIndex==itemsIndex,
                            "tab-title":true
                        },
                        on:{
                            click:this.switchChange.bind(this,itemsIndex)
                        },
                        directives:[
                            {
                                name:"show",
                                value:!$items[itemsIndex].data.attrs.disable
                            }
                        ],
                    },[
                        createElement("a",{
                            domProps:{
                                innerHTML:$items[itemsIndex].data.attrs["nav"]
                            }
                        })
                    ]));

                    $childContent.push(createElement("div",{
                        class:"wrapper-tabContent tab-pane "+(this.switchIndex==itemsIndex?"active":""),
                    },[
                        createElement("div",{
                            directives:[
                                {
                                    name:"show",
                                    value:!$items[itemsIndex].data.attrs.disable
                                }
                            ]
                        },[$items[itemsIndex]])

                    ]))
                }
                return createElement("div",{
                    class:"tab"
                },[
                    createElement("div",{
                        class:"tab-header"
                    },[
                        createElement("ul",{
                            class:["tab-nav nav nav-tabs mb",""].join(" "+_self.navClass)
                        },$childTitle),
                        createElement("div",{
                            class:"tab-more"
                        },_self.$slots["more"])

                    ]),
                    createElement("div",{
                        class:["tab-panel tab-content",""].join(" "+_self.panelClass)
                    },$childContent)
                ])
            },
            renderSimpleNew(createElement){
                var _self=this, $items=this.$slots["tab-item"]||[],
                    itemsIndex=0,itemsLen=$items.length,$childTitle=[],$childContent=[],$contentFixed=_self.$slots["tab-panel-fixed"];
                $childContent.push(createElement("panel-item",{
                },$contentFixed));
                var _=_self._;
                if(!_self.flag){
                    _.forEach($items,function(item,itemIndex){
                        if(!_self.flag&&item.data["attrs"]&&item.data["attrs"].active!==undefined){
                            _self.switchIndex=itemIndex;
                            return false;
                        }
                    });
                    _self.flag=true;
                }
                for(;itemsIndex<itemsLen;itemsIndex++){

                    var hasInitTitle=false,hasInitContent=false;
                    _.forEach($items[itemsIndex]["children"],function(_child){
                        if(_child.data&&_child.data.slot){
                            if(_child.data["slot"]=="nav"){
                                hasInitTitle=true;
                                $childTitle.push(createElement("li",{
                                    class:{
                                        active:_self.switchIndex==itemsIndex,
                                        "tab-title":true
                                    },
                                    on:{
                                        click:_self.switchChange.bind(this,itemsIndex)
                                    },
                                    directives:[
                                        {
                                            name:"show",
                                            value:!$items[itemsIndex].data.attrs.disable
                                        }
                                    ],
                                },[
                                    createElement("a",{
                                    },_child.children)
                                ]));

                            }else if(_child.data["slot"]=="panel"){

                                hasInitContent=true;
                                $childContent.push(createElement("div",{
                                    class:"wrapper-tabContent tab-pane "+(_self.switchIndex==itemsIndex?"active":""),
                                },_child.children))
                            }
                        }
                    })

                    !hasInitTitle&&$childTitle.push(createElement("li",{
                        class:{
                            active:this.switchIndex==itemsIndex,
                            "tab-title":true
                        },
                        on:{
                            click:this.switchChange.bind(this,itemsIndex)
                        },
                        directives:[
                            {
                                name:"show",
                                value:!$items[itemsIndex].data.attrs.disable
                            }
                        ],
                    },[
                        createElement("a",{
                            domProps:{
                                innerHTML:$items[itemsIndex].data.attrs["nav"]
                            }
                        })
                    ]));

                    !hasInitContent&&$childContent.push(createElement("div",{
                        class:"wrapper-tabContent tab-pane "+(this.switchIndex==itemsIndex?"active":""),
                    },[
                        createElement("div",{
                            directives:[
                                {
                                    name:"show",
                                    value:!$items[itemsIndex].data.attrs.disable
                                }
                            ]
                        },[$items[itemsIndex]])

                    ]))
                }
                return createElement("div",{
                    class:"tab"
                },[
                    createElement("div",{
                        class:"tab-header"
                    },[
                        createElement("ul",{
                            class:["tab-nav nav nav-tabs mb",""].join(" "+_self.navClass)
                        },$childTitle),
                        createElement("div",{
                            class:"tab-more"
                        },_self.$slots["more"])

                    ]),
                    createElement("div",{
                        class:["tab-panel tab-content",""].join(" "+_self.panelClass)
                    },$childContent)
                ])
            }
        },

        created:function(){
            this.switchIndex=this.index;
        },
        render:function(createElement){
            var _self= this;
            switch (_self.type){
                case "simple":
                    return _self.renderSimpleNew(createElement);
                    break;
                case "rich":
                    return _self.renderRich(createElement)
                default:
                    return _self.renderSimpleNew(createElement);
                    break;
            }
        },
        watch:{
            index(){
                this.switchIndex=this.index;
            }
        }
    }
</script>
<style lang="scss">
    .tab-fixed{
        display:block!important;;
    }
    .tab-header{
        position:relative;
        .tab-more{
            position: absolute;
            right: 0px;
            bottom: 4px;
        }
    }
    .tab-nav{

        border-bottom:1px solid #ddd;

        .nav-item{
            border-top-left-radius: 5px;
            border-top-right-radius: 5px;
            border:1px solid #fff;
            padding:10px;
            display:inline-block;
            &.active{
                border:1px solid #ddd;
                border-bottom:0px;
                position:relative;
                a{
                    color: #555;
                    cursor:pointer;
                }
                &:hover{
                    background:none;
                }
                &:after{
                    content: "";
                    display: block;
                    position: absolute;
                    left: 0px;
                    right: 0px;
                    bottom: -2px;
                    background: #ffffff;
                    width: 100%;
                    height: 1px;
                }
            }
            &:hover{
               background:#fbfbfb;
                cursor:pointer;
            }
        }
    }
    .tab-panel{
        padding:10px;
    }
</style>