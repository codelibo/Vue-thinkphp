<template>
    <el-dialog :visible="ifshow" :before-close="handleClose">
      <el-form :model="form">
      <el-form-item label="物料类型"><el-input v-model="form1.type" auto-complete="off"></el-input></el-form-item>
      <el-form-item label="备注"><el-input v-model="form.remark" auto-complete="off"></el-input></el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="showdialog1 = false">取 消</el-button>
        <el-button type="primary" @click="submit1">确 定</el-button>
      </div>
    </el-dialog>
</template>

<script>
export default {
    props:['ifshow'],
    data(){
        return{
            form:{
                type:'',
                remark:''
            },
            handleClose:false
        }
    },
    methods:{
        dialogclose(){
            this.$emit('close')
        },
        submit(){
            this.$http.post('api/submitMaterialType',this.form).then((res)=>{
                if(res.data.code===1){
                    this.$message({message:res.data.msg,type:'success'});
                    this.dialogclose()
                }else{
                    this.$message({message:res.data.msg,type:'error'})
                }
            })
        },
        handleClose(done) {
            this.$confirm('确认关闭？')
                .then(_ => {
                    this.dialogclose()
                })
                .catch(_ => {});
        }
    }
    
}
</script>

<style>

</style>
