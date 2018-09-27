# 一、LOG4J日志框架的整理
    
   1、首先要添加log4j.jar包   
   [http://mvnrepository.com/artifact/log4j/log4j] 
     
   2、要在resources资源文件中创建两个文件log4j.properties和mybatis.xml
      
   * log4j.properties
    
      
          # 全局配置: 只显示错误级别的日志，输出为名字为 stdou 的日志
          # error实在有错误信息时才显示。
          log4j.rootLogger=error, stdout

          # MyBatis 的日志配置，只输出 com.wgc.bookstore_ssm.dao 包下产生 INFO 以及以上级别的日志
          # TRACE当程序执行时，它会输出执行过的sql信息
          log4j.logger.com.wgc.bookstore_ssm.dao=TRACE

          # 定义名字为 stdout 的日志，将日志输出到控制台
          # ConsoleAppender的意思的输出到控制台附加的信息
          log4j.appender.stdout=org.apache.log4j.ConsoleAppender
          # PatternLayout的意思是要以什么样的形式输出到控制台
          log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
          log4j.appender.stdout.layout.ConversionPattern=%5p [%t] - %m%n
     
   * mybatis.xml
   

          <?xml version="1.0" encoding="UTF-8" ?>
          <!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
          <configuration>
              <settings>
                  <setting name="logImpl" value="LOG4J"/>
              </settings>
          </configuration>

   
   * 还要在spring-root.xml进行一个配置
   
       
         <!--配置 mybatis-->
           <bean class="org.mybatis.spring.SqlSessionFactoryBean" id="sqlSessionFactory">
       
               <property name="dataSource" ref="dataSource"/>
               
               <!--要启用配置的日志，就要在这里写一句mybatis的配置写入，要执行那个文件的 mybatis.xml就是执行日志文件的-->
               <property name="configLocation" value="classpath:mybatis.xml"/>
       
               <property value="classpath:mapper/BookDao.xml" name="mapperLocations"/>
       
           </bean>
