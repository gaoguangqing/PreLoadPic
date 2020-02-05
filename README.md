# PreLoadPic
图片预加载-无序加载

>核心内容

>实例化image对象

>监听load事件和error事件

>为src赋上正确的图片路径

```
            var image=new Image();
            $(image).on('load error',function () {
             
            });
            image.src=src;
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>图片预加载</title>
    <style>
        html,body{
            height: 100%;
        }
        a{
            text-decoration: none;
        }
        .box{
            text-align: center;
        }
        .btn{
            display: inline-block;
            height: 30px;
            line-height: 30px;
            border: 1px solid #ccc;
            background-color: #fff;
            padding: 0 15px;
            margin-right: 50px;
            color: #333;
        }
        .btn:hover{
            background-color: #eee;
        }
        .loading{
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #eee;
            text-align: center;
            font-size: 5em;
        }
        .progress{
            padding-top: 150px;
        }
    </style>
</head>
<body>
<div class="box">
    <img src="img/scene0.jpg" alt="pic" id="img" width="1000px" height="500px"/>
    <p>
        <a href="javascript:;" class="btn" data-control="prev">上一页</a>
        <a href="javascript:;" class="btn" data-control="next">下一页</a>
    </p>
</div>
<div class="loading">
    <p class="progress">0%</p>
</div>

<script src="js/jquery-1.9.1.min.js"></script>
<script>
    var imgs=[
        'img/scene0.jpg',
        'img/scene1.jpg',
        'img/scene3.jpg',
        'img/scene4.jpg',
        'img/scene5.jpg',
        'img/scene6.jpg',
        'img/scene7.jpg',
        'img/scene8.jpg'
    ];

    var index=0;
    var len=imgs.length;
    var count=0;
    $progress=$('.progress');

    $.each(imgs,function (i,src) {
        var image=new Image();

        $(image).on('load error',function () {
            $progress.html(Math.round((count+1)/len*100)+'%');
            if(count>=len-1){
                $('.loading').hide();
            }
            count++;
        });
        image.src=src;
    });
    $('.btn').on('click',function () {
       if("prev"===$(this).data('control')){
           //上一张
           index--;
           if(index<0) index=0;

       } else{
           //下一张
           index++;
           if(index>len-1) index=len-1;
       }
       $('#img').attr('src',imgs[index]);
    });
</script>
</body>
</html>
```
