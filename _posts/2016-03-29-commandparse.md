---
layout: post
title:  "OpenCV CommandLineParser用法"
date:   2016-03-24
categories: Code
---

## OpenCV CommandLineParsed类用法

本文章参考[CommandLineParser Class](http://docs.opencv.org/3.0.0/d0/d2e/classcv_1_1CommandLineParser.html#a3136cd8a4da764026bebd67b4d70d270)和[tornadomeet的CommandLineParser类的简单理解](http://www.cnblogs.com/tornadomeet/archive/2012/04/15/2450505.html)

## 例子介绍
        const String keys =
            "{help h usage ? |      | print this message   }"
            "{@image1        |      | image1 for compare   }"
            "{@image2        |      | image2 for compare   }"
            "{@repeat        |1     | number               }"
            "{path           |.     | path to file         }"       
            "{fps            | -1.0 | fps for output video }"
            "{N count        |100   | count of objects     }"
            "{ts timestamp   |      | use time stamp       }";}

        CommandLineParser parser(argc, argv, keys);
        parser.about("Application name v1.0.0");
        

        if (parser.has("help"))
        {
             parser.printMessage();
             return 0;
        }
        int N = parser.get<int>("N");
        double fps = parser.get<double>("fps");
        String path = parser.get<String>("path");
        use_time_stamp = parser.has("timestamp");
        String img1 = parser.get<String>(0);
        String img2 = parser.get<String>(1);
        int repeat = parser.get<int>(2);
        if (!parser.check())
        {
            parser.printErrors();
             return 0;
        }
        
        $ ./app -N=200 1.png 2.jpg 19 -ts
        
1. {help h usage ? | | }
    
    分为三个字段，第一字段为参数名称，第二个字段为默认值，第三个字段为说明。只使用参数名称，不赋值。由于存在多个参数名称，可通过下列多种方式使用：
    
            ./code -h
            ./code -help
            ./code -usage
            ./code -?               //由于已经使用了参数名称help等，通过has("help")判断则返回true
               
2. {@image1 |   white.jpg   | image1 for compare  }

    第一个字段为参数名称，直接赋值给@image，第二个字段为默认值，第三个字段为说明。使用方式：
    
            string filename=parser.get<string>("@string");
             $ ./app white.jpg
    
3. {path | . | path to file}

    第一字段为参数名称，第二个字段为默认值，第三个字段为说明。要想对其赋值，则必须指定具体参数复制：
    
            ./code -path=../
            ./code /home/tmp        //无效，无法赋值，如果要使用该种方式，必须使用@path
            
4. 多个函数：
    
    - CommandLineParser::has(const String &name) const      判断参数名称是否在命令行中出现
    - CommandLineParser::<typename T >get(const String name)        返回命令行给参数名称赋的值，通过相应类型返回，不能转换则返回错误
    - CommandLineParser::check()    检测parsing的错误
    
    
