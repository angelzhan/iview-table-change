<template>
    <table cellspacing="0" cellpadding="0" border="0" :style="styleObject">
        <colgroup>
            <col v-for="(column, index) in columns" :width="setCellWidth(column, index, false)">
        </colgroup>
        <tbody :class="[prefixCls + '-tbody']">
            <template  v-for="(row, index) in data">
                <template v-if="!row.pid && row.pid != 0">
                     <tr 
                        :key="row"
                        v-show="displayValue[row._index]"
                        :class="['ivu-table-row-' + row.nodeIndex , rowClasses(row._index)]"
                        @mouseenter.stop="handleMouseIn(row._index)"
                        @mouseleave.stop="handleMouseOut(row._index)"
                        @click.stop="clickCurrentRow(row._index)"
                        @dblclick.stop="dblclickCurrentRow(row._index)">

                       <!--  <td v-for="column in columns" :t="index"  :class="alignCls(column, row)"  >
                           <Cell
                               :fixed="fixed"
                               :prefix-cls="prefixCls"
                               :row="row"
                               :column="column"
                               :natural-index="index"
                               :index="row._index"
                               :checked="rowChecked(row._index)"
                               :disabled="rowDisabled(row._index)"
                               :iconStatus="iconPos[row._index]"
                               ></Cell>
                       </td> -->
                       <template v-for="(column,n) in colPos[index]"  >
                          
                            <td :class="alignCls(column, row)" v-if="column.rowSpan && !column.colSpan" :rowSpan="column.rowSpan"   >
                                <Cell
                                  :fixed="fixed"
                                  :prefix-cls="prefixCls"
                                  :row="row"
                                  :column="column"
                                  :natural-index="index"
                                  :index="row._index"
                                  :checked="rowChecked(row._index)"
                                  :disabled="rowDisabled(row._index)"
                                  :iconStatus="iconPos[row._index]"
                                  >
                                </Cell>
                            </td>
                            <td :class="alignCls(column, row)" v-if="column.rowSpan && column.colSpan" :rowSpan="column.rowSpan"  :colSpan="column.colSpan"  >
                                <Cell
                                  :fixed="fixed"
                                  :prefix-cls="prefixCls"
                                  :row="row"
                                  :column="column"
                                  :natural-index="index"
                                  :index="row._index"
                                  :checked="rowChecked(row._index)"
                                  :disabled="rowDisabled(row._index)"
                                  :iconStatus="iconPos[row._index]"
                                  >
                                </Cell>
                            </td>
                            <td :class="alignCls(column, row)" v-if="!column.rowSpan && column.colSpan" :colSpan="column.colSpan"   >
                                <Cell
                                  :fixed="fixed"
                                  :prefix-cls="prefixCls"
                                  :row="row"
                                  :column="column"
                                  :natural-index="index"
                                  :index="row._index"
                                  :checked="rowChecked(row._index)"
                                  :disabled="rowDisabled(row._index)"
                                  :iconStatus="iconPos[row._index]"
                                  >
                                </Cell>
                            </td>
                            <td :class="alignCls(column, row)" :v="column.hide" v-if=" column.hide != 1"  >
                                     
                                <Cell
                                   :fixed="fixed"
                                   :prefix-cls="prefixCls"
                                   :row="row"
                                   :column="column"
                                   :natural-index="index"
                                   :index="row._index"
                                   :checked="rowChecked(row._index)"
                                   :disabled="rowDisabled(row._index)"
                                   :iconStatus="iconPos[row._index]"
                                   >
                                 </Cell>
                            </td>

                       </template>
                    </tr>
     
               
                </template>
                <template v-else>
                    <tr 
                     :key="row"
                     :class="['ivu-table-row-' + row.nodeIndex , rowClasses(row._index)]"
                     v-show="displayValue[row._index]"
                     @mouseenter.stop="handleMouseIn(row._index)"
                     @mouseleave.stop="handleMouseOut(row._index)"
                     @click.stop="clickCurrentRow(row._index)"
                     @dblclick.stop="dblclickCurrentRow(row._index)">
                       
                        <template v-for="(column,n) in colPos[index]"  >
                          
                            <td :class="alignCls(column, row)" v-if="column.rowSpan && !column.colSpan" :rowSpan="column.rowSpan"   >
                                <Cell
                                  :fixed="fixed"
                                  :prefix-cls="prefixCls"
                                  :row="row"
                                  :column="column"
                                  :natural-index="index"
                                  :index="row._index"
                                  :checked="rowChecked(row._index)"
                                  :disabled="rowDisabled(row._index)"
                                  :iconStatus="iconPos[row._index]"
                                  >
                                </Cell>
                            </td>
                            <td :class="alignCls(column, row)" v-if="column.rowSpan && column.colSpan" :rowSpan="column.rowSpan"  :colSpan="column.colSpan"  >
                                <Cell
                                  :fixed="fixed"
                                  :prefix-cls="prefixCls"
                                  :row="row"
                                  :column="column"
                                  :natural-index="index"
                                  :index="row._index"
                                  :checked="rowChecked(row._index)"
                                  :disabled="rowDisabled(row._index)"
                                  :iconStatus="iconPos[row._index]"
                                  >
                                </Cell>
                            </td>
                            <td :class="alignCls(column, row)" v-if="!column.rowSpan && column.colSpan" :colSpan="column.colSpan"   >
                                <Cell
                                  :fixed="fixed"
                                  :prefix-cls="prefixCls"
                                  :row="row"
                                  :column="column"
                                  :natural-index="index"
                                  :index="row._index"
                                  :checked="rowChecked(row._index)"
                                  :disabled="rowDisabled(row._index)"
                                  :iconStatus="iconPos[row._index]"
                                  >
                                </Cell>
                            </td>
                            <td :class="alignCls(column, row)" :v="column.hide" v-if=" column.hide != 1"  >
                                     
                                <Cell
                                   :fixed="fixed"
                                   :prefix-cls="prefixCls"
                                   :row="row"
                                   :column="column"
                                   :natural-index="index"
                                   :index="row._index"
                                   :checked="rowChecked(row._index)"
                                   :disabled="rowDisabled(row._index)"
                                   :iconStatus="iconPos[row._index]"
                                   >
                                 </Cell>
                            </td>

                       </template>

                    </tr>
              
                </template>


                
                <!-- -->
            </template>
         
        </tbody>
    </table>
</template>
<script>
    // todo :key="row"
    import Cell from './cell.vue';
    import Mixin from './mixin';
    import store from './store';
    export default {
        name: 'TableBody',
        mixins: [ Mixin ],
        components: { Cell },
        data (){
            return {
               status:store.state.status,
               displayValue:this.makeDisplayValue()[0],
               iconPos:this.makeDisplayValue()[1],
               colPos:this.makeColPos(),
               dataIndexPos:[]
            }
        },
        props: {
            prefixCls: String,
            styleObject: Object,
            columns: Array,
            data: Array,    // rebuildData
            objData: Object,
            columnsWidth: Object,
            fixed: {
                type: [Boolean, String],
                default: false
            },
            iconStatus:Boolean
        },
        methods: {
            makeColPos (){
                let v = this,
                    pos = new Array();
                for(let i = 0; i< v.data.length; i++){
                    pos.push(this.makeNewColumn(v.columns));
                }
                return pos;
            },
            makeNewColumn (columns){
                   let pos = [];
                    columns.forEach((n,i) =>{
                    let m =  Object.assign(Object.create(null),n);
                    pos.push(m);
                   })
                   return pos;
            },
            compile (){
                this.columns.forEach((column,i) =>{
                    
                    if (column.render) {
                      let isRealRender = false;
                      try {
                          column.render(this.row, this.column, this.index);
                      }
                      catch (err) {
                          isRealRender = true;
                      }
                      if(!isRealRender){
                        this.data.forEach((item,n) =>{
                            
                            const template = column.render(item, this.columns, n);
                            console.log(template)
                            if(typeof template == "object" && template.props.colSpan && !template.props.rowSpan){
                                this.makeColSpan(n,i,template.props.colSpan);
                            }else if(typeof template == "object" && template.props.rowSpan && !template.props.colSpan){
                                this.makeRowSpan(n,i,template.props.rowSpan);
                            }else if(typeof template == "object" && template.props.rowSpan && template.props.colSpan){
                                this.makeColAndRow(n,i,template.props.rowSpan,template.props.colSpan);
                            }
                            return template.children;
                        });
                      }
                    }
                });
                
            },
            makeColSpan(dataIndex,colIndex,colSpan,rowSpan){//需要合并的tr,第几个td,输入的合并格数
                let colSpanNum = 0;//实际合并多少格
                if((colIndex + colSpan) <= this.columns.length){
                    colSpanNum = colSpan
                }else{
                    colSpanNum = this.columns.length - colIndex;
                }
                let pos = Object.assign(Object.create(null),this.colPos);
                pos[dataIndex][colIndex].colSpan = colSpanNum;
             
                for(let i = 0; i < colSpanNum; i++){
                
                    if(rowSpan && rowSpan!=0){
                      let rowSpanNum = 0;
                      if((dataIndex + rowSpan) <= this.data.length){
                          rowSpanNum = rowSpan
                      }else{
                          rowSpanNum = this.data.length - dataIndex;
                      }

                      for(let t = 0; t < rowSpanNum ; t++){
                        pos[dataIndex + t][colIndex + i].hide = 1;
                      }
                    }else{

                       pos[dataIndex][colIndex + i].hide = 1;
                    }
                }
                
             },
            makeRowSpan(dataIndex,colIndex,rowSpan){
                let pos = Object.assign(Object.create(null),this.colPos);
                 pos[dataIndex][colIndex].rowSpan = rowSpan;
              
               
                let rowSpanNum = 0;
                if((dataIndex + rowSpan) <= this.data.length){
                    rowSpanNum = rowSpan
                }else{
                    rowSpanNum = this.data.length - dataIndex;
                }
                for(let i = 0; i < rowSpanNum; i++){
                    pos[dataIndex + i][colIndex].hide = 1;
                }
               

            },
            makeColAndRow (dataIndex,colIndex,rowSpan,colSpan){
              this.makeRowSpan(dataIndex,colIndex,rowSpan);
              this.makeColSpan(dataIndex,colIndex,colSpan,rowSpan);
            },
            makeDisplayValue (){
                let pos = [],
                    stretchPos = [];//树原始状态集
                 store.state.status.forEach((n,i) =>{
                      let parnode = true;
                    n.forEach((m,t)=>{
                        if(m[0] == -1){
                            stretchPos.push(m[1]);
                            pos.push(true);
                            if(!m[1]) parnode = false;
                        }else{
                            stretchPos.push(m[1]);
                            if(parnode && stretchPos[m[0]]){
                                pos.push(true);
                            }else{
                                pos.push(false);
                            }
                            if(t == n.length - 1){
                                if(!m[1]) parnode = false;
                            }

                             
                        }
                       
                    })
                })
              
                return [pos,stretchPos];
            },
            rowClasses (_index) {
                return [
                    `${this.prefixCls}-row`,
                    this.rowClsName(_index),
                    {
                        [`${this.prefixCls}-row-highlight`]: this.objData[_index] && this.objData[_index]._isHighlight,
                        [`${this.prefixCls}-row-hover`]: this.objData[_index] && this.objData[_index]._isHover
                    }
                ];
            },
            rowChecked (_index) {
                return this.objData[_index] && this.objData[_index]._isChecked;
            },
            rowDisabled(_index){
                return this.objData[_index] && this.objData[_index]._isDisabled;
            },
            rowClsName (_index) {
                return this.$parent.rowClassName(this.objData[_index], _index);
            },
            handleMouseIn (_index) {
                this.$parent.handleMouseIn(_index);
            },
            handleMouseOut (_index) {
                this.$parent.handleMouseOut(_index);
            },
            clickCurrentRow (_index) {
                this.$parent.clickCurrentRow(_index);
            },
            dblclickCurrentRow (_index) {
                this.$parent.dblclickCurrentRow(_index);
            },showRelated (grid,sIndex){//实际上是改变status..[grid,sIndex]组ID，节点索引
                let status = store.state.status;
                if(status[grid][sIndex][1]){
                    status[grid][sIndex][1] = false;
                }else{
                    status[grid][sIndex][1] = true;
                }
                

                store.commit('status',status);
                this.displayValue = this.makeDisplayValue()[0];
                this.iconPos = this.makeDisplayValue()[1]
            },
        },
        mounted (){
            this.$nextTick(() => {
                this.compile();
            });
        }
    };
</script>
