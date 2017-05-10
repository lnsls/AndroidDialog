# AndroidDialog
Android Dialog 安卓对话框

<img src="http://ww2.sinaimg.cn/large/006tNbRwgy1ffg43248mfj30u00sy0t2.jpg" width="400px"/>

Android Dialog 即 Android对话框，在Android开发中，我们经常会需要在Android界面上弹出一些对话框，以询问用户或者让用户选择。Android Dialog 一般有五种，分别是：一般对话框，列表对话框，单选按钮对话框，多选对话框，自定义对话框。

<!-- more -->

## 一般对话框
<img src="http://ww4.sinaimg.cn/large/006tNbRwgy1ffg2gl99ipj30u01hcabj.jpg" width="300px"/>

```java
AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setIcon(R.mipmap.ic_launcher);   //设置图标
builder.setTitle("一般对话框");                    //设置标题
builder.setMessage("这是对话框要显示的内容");       //设置内容
builder.setCancelable(false);           //将对话框以外的区域设置成无法点击

//确认按钮监听事件
builder.setPositiveButton("确认", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

        Toast.makeText(MainActivity.this, "点击了 确定", Toast.LENGTH_SHORT).show();
        dialog.dismiss();      //取消显示(关闭)对话框
    }
});

//忽略按钮监听事件
builder.setNegativeButton("取消", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

        Toast.makeText(MainActivity.this, "点击了 取消", Toast.LENGTH_SHORT).show();
        dialog.dismiss();      //取消显示(关闭)对话框
    }
});

builder.create().show();         //创建并显示对话框
```

## 列表对话框
<img src="http://ww1.sinaimg.cn/large/006tNbRwgy1ffg2oug9x4j30u01hcabb.jpg" width="300px"/>

```java
final String item[] = {"第一项", "第二项", "第三项"};     //设置列表内容

AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setIcon(R.mipmap.ic_launcher);   //设置图标
builder.setTitle("列表对话框");           //设置标题
builder.setCancelable(false);           //将对话框以外的区域设置成无法点击

//列表项监听事件
builder.setItems(item, new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

        Toast.makeText(MainActivity.this, "点击了 " + item[which], Toast.LENGTH_SHORT).show();

    }
});

builder.create().show();         //创建并显示对话框
```

## 单选按钮对话框
<img src="http://ww3.sinaimg.cn/large/006tNbRwgy1ffg2pywg99j30u01hc75t.jpg" width="300px"/>

```java
final String item[] = {"第一项", "第二项", "第三项"};     //设置列表内容

AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setIcon(R.mipmap.ic_launcher);   //设置图标
builder.setTitle("单选按钮对话框");           //设置标题
builder.setCancelable(false);           //将对话框以外的区域设置成无法点击

//单选按钮监听事件,item列表内容,select为默认选中的数组编号
builder.setSingleChoiceItems(item, select, new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

        Toast.makeText(MainActivity.this, "选择了 " + item[which], Toast.LENGTH_SHORT).show();
        select = which;        //更新默认选中
    }
});

// 设置确认按钮
builder.setPositiveButton("确定", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

        Toast.makeText(MainActivity.this, "确定", Toast.LENGTH_SHORT).show();
        dialog.dismiss();      //取消显示(关闭)对话框
    }
});

builder.create().show();         //创建并显示对话框
```

## 多选对话框
<img src="http://ww1.sinaimg.cn/large/006tNbRwgy1ffg2rk4ei1j30u01hcgn5.jpg" width="300px"/>

```java
final String item[] = {"第一项", "第二项", "第三项"};     //设置列表内容

AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setIcon(R.mipmap.ic_launcher);   //设置图标
builder.setTitle("多选对话框");           //设置标题
builder.setCancelable(false);           //将对话框以外的区域设置成无法点击

//多选对话监听事件,item列表内容,selected设置默认选中
builder.setMultiChoiceItems(item, selected, new DialogInterface.OnMultiChoiceClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which, boolean isChecked) {

        Toast.makeText(MainActivity.this, item[which] + isChecked, Toast.LENGTH_SHORT).show();
        selected[which] = isChecked;
    }
});

// 设置确认按钮
builder.setPositiveButton("确定", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

        Toast.makeText(MainActivity.this, "确定", Toast.LENGTH_SHORT).show();
        dialog.dismiss();      //取消显示(关闭)对话框
    }
});

builder.create().show();         //创建并显示对话框
```

## 自定义对话框
<img src="http://ww4.sinaimg.cn/large/006tNbRwgy1ffg2uavcctj30u01hcmyf.jpg" width="300px"/>

```java
AlertDialog.Builder builder = new AlertDialog.Builder(this);  //先得到构造器
builder.setIcon(R.mipmap.ic_launcher);   //设置图标
builder.setTitle("自定义对话框");           //设置标题
builder.setCancelable(false);           //将对话框以外的区域设置成无法点击

// 载入自定义布局
LayoutInflater inflater = getLayoutInflater();
View layout = inflater.inflate(R.layout.dialog, null);
builder.setView(layout);

// 对布局中的控件监听
final EditText editText_name = (EditText) layout.findViewById(R.id.editText_name);
final EditText editText_password = (EditText) layout.findViewById(R.id.editText_password);

// 输入框监听事件
editText_name.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

        Toast.makeText(MainActivity.this, "点击了账号输入框", Toast.LENGTH_SHORT).show();
    }
});

// 输入框监听事件
editText_password.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

        Toast.makeText(MainActivity.this, "点击了密码输入框", Toast.LENGTH_SHORT).show();
    }
});

// 设置确认按钮
builder.setPositiveButton("确定", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {

        Toast.makeText(MainActivity.this, "账号" + editText_name.getText().toString() + "\n密码" + editText_password.getText().toString(), Toast.LENGTH_SHORT).show();
        dialog.dismiss();      //取消显示(关闭)对话框
    }
});

builder.create().show();         //创建并显示对话框
```
