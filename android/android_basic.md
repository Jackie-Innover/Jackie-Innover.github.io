- **添加菜单**
- **构建URL**





### 添加菜单

------

1. 创建 menu folder. 

   ![create menu](/images/create_menu.jpg)
   ![menu res type](./images/menu_res_type.jpg)

2. add item node, set id, title, orderInCategory, showAsAction and others.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <menu xmlns:android="http://schemas.android.com/apk/res/android"
         xmlns:app="http://schemas.android.com/apk/res-auto">
       <item
           android:id="@+id/action_search"
           android:title="Jackie"
           android:orderInCategory="1"
           app:showAsAction="ifRoom">

       </item>
   </menu>
   ```

   ​

3. override **onCreateOptionsMenu** and **onOptionsItemSelected** methods

   ```java
       @Override
       public boolean onCreateOptionsMenu(Menu menu) {
           getMenuInflater().inflate(R.menu.main, menu);
           return  true;
       }
   ```

   ```java
       public boolean onOptionsItemSelected(MenuItem item) {
           if (item.getItemId()==R.id.action_search){
               Toast.makeText(this, "search clicked", Toast.LENGTH_SHORT).show();
           }

           return super.onOptionsItemSelected(item);
       }
   ```

   ​


### 构建URL

------

1. Uri.parse().buildUpon()
2. appendQueryParameter(key, value)
3. build
4. new URL(uri.toString())