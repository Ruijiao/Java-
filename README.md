# 反射
### 最近用Android对接广告的时候，因为多个渠道，每个渠道要求的广告平台不同，但每次打包都改代码，删代码的也太麻烦，就想到了用反射，这样删除jar包代码也不至于报错，以前只是学过反射，但真正用的时候很少，这次用到了，做个总结，方便以后查看，
##一。调用静态方法
<pre>
  <code>
  </code>
</pre>
<pre>
  <code>
    LestoreAD.init(act);
  </code>
</pre>
### 用反射：
<pre>
  <code>
   try{
			//拿到类
			Class<?> aDSize = Class.forName("com.lestore.ad.sdk.LestoreAD");
			//拿到类中的方法，参数一：方法名，参数二：参数类型
			Method methodSetKey = aDSize.getMethod("init", new Class[]{Activity.class});
			//方法调用，参数一：类对象，静态方法穿null，参数二：方法中需要的参数
			methodSetKey.invoke(null, new Object[]{act});
		}catch(Exception e){
		}
  </code>
</pre>
## 二。拿到属性
<pre>
  <code>
  BannerSize.BANNER_SIZE_728_90_DIP
  </code>
</pre>
###用反射
<pre>
  <code>
  Class aDSize = Class.forName("com.lestore.ad.sdk.BannerSize");
	//拿到他的属性
	Field[] fields = aDSize.getFields();
	Object adSizeDip = null;
	
	for(Field field : fields){
		if("BANNER_SIZE_728_90_DIP".equals(field.getName()))
		{
    		adSizeDip = field.get(aDSize);
    		break;
  		}
	}
  </code>
</pre>












