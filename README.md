# PermissionSix
安卓6.0权限设置

![](https://github.com/gdmec07120731/PermissionSix/blob/master/pic/O6CBZNJP%40U4K7%5BKDW%7D7%7DN%24Q.png)

先判断当前应用也没有获取打电话权限，再执行打电话操作。需要用到的参数有Context,Manifest.permission.CALL_PHONE,自定义常量
CALL_PHONE

```java
 private void Call(){
      if(ContextCompat.checkSelfPermission(this, Manifest.permission.CALL_PHONE)!= PackageManager.PERMISSION_GRANTED){
          ActivityCompat.requestPermissions(this,new String[]{Manifest.permission.CALL_PHONE},CALL_PHONE);

      }else{
          Intent intent=new Intent(Intent.ACTION_CALL);
          intent.setData(Uri.parse("tel:"+"10086"));
          startActivity(intent);
      }
 }
```


接着重写onRequestPermissionsResult方法，先判断常量是不是CALL_PHONE,再判断有没有拒绝权限请求，再执行打电话操作。
```java
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        if(requestCode==CALL_PHONE){

            if(grantResults[0]==PackageManager.PERMISSION_GRANTED){

                Call();
            }
            else{
                Toast.makeText(this,"授权拒绝",Toast.LENGTH_SHORT).show();
            }
        }

        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
    }
```