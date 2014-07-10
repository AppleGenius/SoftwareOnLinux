一：概述：
    DBLocator_Service 提供了一套查询后台数据库连接地址的服务，该服务同时提供了对Redis和MySQL数据库操作的接口。

二：接口描述：
    （一） Redis部分：
        ···java
        /**
	    * 添加一条记录在Redis数据库中
	    * @param key the String 一条记录的key
	    * 		  value the String 一条记录的value
	    * @return <code>1</code> 执行成功
	    *		   <code>0</code> 执行失败
	    */
        public int add(String key, String value);
        ···
