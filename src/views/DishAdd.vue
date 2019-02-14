<template>
  <div class="">
  <h1>添加菜品</h1>
    <el-form label-width="100px">
      <el-form-item label="菜品图片">
        <el-upload class="xfn-uploader" :action="uploadAction" :on-success="doUploadSucc" name="dishImg" :show-file-list="false">
          <img v-if="imageUrl" :src="imageUrl"/>
        </el-upload>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
  export default {
    data(){
      return {
        imageUrl:'',  //要显示的预览图地址
        uploadAction:     //可处理文件上传的API
        this.$store.state.globalSettings.apiUrl +'/admin/dish/image',
        formData: {
          title:'',
          imgUrl:'',  //菜品图片在服务器上的文件名称
          price:'',
          detail:''
        }
      }
    },
    methods:{
      doUploadSucc(res,file){
        //文件上传成功后，客户端得到响应消息之后的处理函数
        //res: 服务器端返回的响应消息
        //file: 从input[type=file]中读取的第一个上传的文件对象
        console.log(res);
        this.formData.imgUrl = res.fileName;
        this.imageUrl = URL.createObjectURL(file.raw);
        //把上传的文件编码为DataURL字符串
      }
    }
  }
</script>

<!--lang="scss" 不加 scoped，  scoped加>>> 符号样式渗透 -->
<style scoped>
  .xfn-uploader >>> .el-upload{
      border:1px dotted #aaa;
      border-radius: 3px;
      cursor:poinser;
      width:250px;
      height:177px;
      overflow:hidden;
  }
  .xfn-uploader >>> .el-upload:hover { 
    border-color:#409eff;
  }

  img{
    max-width:100%;
  }
</style--> 