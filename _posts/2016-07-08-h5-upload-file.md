h5无刷新上传图片是利用FileReader函数实现的。
关键代码：
```
var vm = {
  base64:'',
  imageType:'',
  uploadHeadImage:function(){
      if(typeof FileReader !== "function"){
          layer.msg("你的浏览器不支持此功能，请更新浏览器，建议使用谷歌浏览器",{icon:2});
      }else{
          $("#head-image-upload").trigger("click");
      }
  },
  isImage:function(file){
      var name = file.name.toLowerCase();
      var type = file.type.toLowerCase();
      if(/.+\.(gif|png|jpg|jpeg)/.test(name) &&
          (type == "image/gif" ||
           type == "image/png" ||
           type == "image/jpg" ||
           type == "image/jpeg"
          )
      ){
          vm.imageType = type.replace("image/","");
          return true;
      }
      return false;
  },
  sizeFit:function(file){
      return file.size <= 2*1024*1024;//2M
  },
  previewImage:function(file){
      var reader = new FileReader();
      var stream = reader.readAsDataURL(file);
      reader.onload = function(streaming){
          vm.base64 = streaming.target.result;
      };
  },
  selectImageDone:function(){
      var file = $("#head-image-upload").get(0).files[0];
      if(vm.isImage(file)){
          if(vm.sizeFit(file)){
              vm.previewImage(file);
          }else{
              layer.msg('图片大小不能超过2M',{icon:2});
          }
      }else{
          layer.msg('请上传正确格式的图片文件',{icon:2});
      }
  },
  submit:funciton(){
    $.post("uri",{
      base64:vm.base64,
      type:vm.imageType
    },function(r){
      console.log(r);
    });
  },
};  
```
后端接受文件是把base64字符串过滤掉文件头后写入文本文件，这里用php举例：
```
private function isImage($base64,$type){
    return $base64 != '' && $type != '';
}

private function checkCompanyLogo($base64,$type){
    $lowerType = strtolower($type);
    if(in_array($lowerType,['png','jpg','jpeg','gif'])){
        if(strlen($base64) > 2*1024*1024){//2M
            return '图片尺寸不能超过2M';
        }else{
            return true;
        }
    }else{
        return "不是图片格式";
    }
}

private function saveCompanyLogo($base64,$type){
    $startIndex = strpos($base64,'base64,') + strlen('base64,');
    $fileContent = base64_decode(substr($base64,$startIndex));
    $path = PUBLIC_DIR.'/images/logo/';
    $filename = $this->com_create_guid().'.'.$type;
    $logo = fopen($path.$filename,'w');

    return fwrite($logo,$fileContent) === false ? false : $filename;
}

public funciton save(Request $request){
  $base64 = $request->get("base64");
  $type = $request->get("type");
  if($this->isImage() === true && $this->checkCompanyLogo($base,$type) === true){
    $filename = $this->saveCompanyLogo($base,$type);
    echo  $filename === false ? 'save fail':'success';
  }
}
```
