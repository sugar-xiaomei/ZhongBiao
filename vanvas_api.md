#  canvas 常用api
####特点：绘制上的元素无法更改
  ##形状
    >
     *cts.fillRect()   填充矩形
     *cts.strokeRect()   框线矩形
   >圆
     *cts.arc();     画圆
     *cts.arcTO()   画圆弧
  >线
    *ctx.beginPath();  开始一条路径
    *ctx.moveTo();    移动画笔到某点
    *ctx.lineTo();   让路径拥有一条 到某点的线(并不会直接就画上线 去填充或描边)
    *cts.rect()   让路径拥有（并不会直接绘制）一个矩形
    *ctx.fill();    填充当前路径
    *ctx.stroke();  描边当前路径
    *ctx.closePath();   结束一个路径
    *ctx.clearRect()     从画布中清楚某些区域
    *ctx.quadraticCurveTo(cp1x.cp2y,x,y)   二次贝塞尔曲线
    *ctx.bezierCurveTo(cp1x.cp2y,cp2x,cp2y,x,y)   三次贝塞尔曲线
#位移    
   *ctx.save();        //保存原来的样式  只保存画布的状态
   *ctx.restore();     //恢复到上次保存的状态 不保存任何图像
   *ctx.translate(x，y);   //移动画布到当前位置
   *ctx.rotate(Math.PI/180*360)  //旋转
   *ctx.scale()     //缩放

###清理画布的两种方式
   document.onclick=function(){
   canvas.width=carvas.height=600;  //直接设置宽高
   ctx.clearRect(0,0,600,600);   //调用该方法
 }
# 样式
  *ctx.fillStyle ='rgba(0,0,0)';
  *ctx.strokeStyle='#000';
  *ctx.globalAlpha=0.2;  全局的透明度
  >>>>>线性
   ctx.lineWidth = value  边框的宽度   相对中心两边拓展   
   ctx.lineHeight = value
   ctx.lineCap = type   末端样式  
                       butt默认  round  圆角    square 会伸出半个小方块
   ctx.lineJoin = type  线条与线条接洽的样式  round;
   ctx.Join='inherit'  两条线的节点


  *ctx.creatPattern(image,type);  dom对象的image   no-repeat
  *ctx.creatLinearGradient(x,y,x,y)
    ctx.shadowOffsetX=10;
    ctx.shadowOffsetX=10;    
    ctx.shadowOffsetBlur=10;   
    ctx.shadowOffsetColor=10;



    ctx.fillText('jjj',0,0,300);
    ctx.strokefillText('jjj',0,0,300);
    ctx.font(10px,song)






    var  canvasS = 600;
      var  row = 15;
      var  blockS = canvasS/row;
      ctx = $('#canvas').get(0).getContext('2d');
      var  starRadius = 3;


      $('#canvas').get(0).height = canvasS;
      $('#canvas').get(0).width = canvasS;

      var draw = function(){
        var off = blockS/2 + 0.5;
        var lineWidth = canvasS - blockS;

        ctx.save();
        ctx.beginPath();
        ctx.translate(off,off);
        for(var i = 0; i<row; i++){
          ctx.moveTo(0,0)
          ctx.lineTo(lineWidth,0);
          ctx.translate(0,blockS);
        }
        ctx.stroke();
        ctx.closePath();
        ctx.restore();

        ctx.save();
        ctx.beginPath();
        ctx.translate(off,off);
        for(var i = 0; i<row; i++){
          ctx.moveTo(0,0)
          ctx.lineTo(0,lineWidth);
          ctx.translate(blockS,0);
        }
        ctx.stroke();
        ctx.closePath();
        ctx.restore();

        var points = [3.5*blockS+0.5 , 11.5*blockS + 0.5];
        for(var i = 0; i< 2; i++){
          for( var j=0; j<2; j++){
            var x = points[i];
            var y = points[j];
            ctx.save();
            ctx.beginPath();
            ctx.translate(x, y);
            ctx.arc(0,0,starRadius,0,(Math.PI/180)*360);
            ctx.fill();
            ctx.closePath();
            ctx.restore();
          }
        }
        ctx.save();
        ctx.beginPath();
        ctx.translate(7.5*blockS+0.5, 7.5*blockS + 0.5);
        ctx.arc(0,0,starRadius,0,(Math.PI/180)*360);
        ctx.fill();
        ctx.closePath();
        ctx.restore();
      }
      draw();

      var qiziRadius = blockS/2*0.8;

      var drop = function(qizi){
        ctx.save();
        ctx.beginPath();
        ctx.translate((qizi.x+0.5)*blockS + 0.5, (qizi.y+0.5)*blockS + 0.5);
        ctx.arc(0,0,qiziRadius,0,Math.PI/180*360);
        if( qizi.color === 1){
          ctx.fill();
        }else{
          ctx.fillStyle = '#fff';
          ctx.strokeStyle = 'black';
          ctx.fill();
          ctx.stroke();
        }
        ctx.closePath();
        ctx.restore();
      }

      var kaiguan = true;
      all = {};
      var step = 1;

      panduan = function(qizi){
        var shuju = {};
        $.each(all,function(k,v){
          if( v.color === qizi.color ){
            shuju[k] = v;
          }
        })
        var shu = 1,hang=1,zuoxie=1,youxie=1;
        var tx,ty;

        /*|*/
        tx = qizi.x; ty = qizi.y;
        while ( shuju [ tx + '-' + (ty + 1) ]){
          shu ++;ty++;
        }
        tx = qizi.x; ty = qizi.y;
        while ( shuju [ tx + '-' + (ty - 1) ]){
          shu ++; ty--;
        }

        /*-*/
        tx = qizi.x ; ty = qizi.y;
        while( shuju[ (tx+1) + '-' + ty ] ){
          hang++;tx++;
        }
        tx = qizi.x ; ty = qizi.y;
        while( shuju[ (tx-1) + '-' + ty ] ){
          hang++;tx--;
        }

        tx = qizi.x; ty = qizi.y;
        while( shuju[ (tx-1) + '-' + (ty-1) ] ){
          zuoxie++;tx--;ty--;
        }
        tx = qizi.x ; ty = qizi.y;
        while( shuju[ (tx+1) + '-' + (ty+1) ] ){
          zuoxie++;tx++;ty++;
        }

        tx = qizi.x ; ty = qizi.y;
        while( shuju[ (tx+1) + '-' + (ty-1) ] ){
          youxie++;tx++;ty--;
        }
        tx = qizi.x ; ty = qizi.y;
        while( shuju[ (tx-1) + '-' + (ty+1) ] ){
          youxie++;tx--;ty++;
        }

        if( shu >=5  || hang>=5 || zuoxie>=5 || youxie>=5){
          return true;
        }
      }

      $('#canvas').on('click',function(e){
        var x = Math.floor(e.offsetX/blockS);
        var y = Math.floor(e.offsetY/blockS);

        if( all[ x + '-' + y ]){
          return;
        }

        var qizi;

        if(kaiguan){
          qizi = {x:x,y:y,color:1,step:step};
          drop(qizi);
          if( panduan(qizi) ){
            $('.cartel').show().find('#tishi').text('黑棋赢');
          };
        }else{
          qizi = {x:x,y:y,color:0,step:step};
          drop(qizi);
          if( panduan(qizi) ){
            $('.cartel').show().find('#tishi').text('白棋赢');
          };
        }
        step += 1;
        kaiguan = !kaiguan;
        all[ x + '-' + y ] = qizi;

      });

      $("#restart").on('click',function(){
        $('.cartel').hide();
        ctx.clearRect(0,0,600,600);
        draw();
        kaiguan = true;
        all = {};
        step = 1;
      })

      $('#qipu').on('click',function(){
        $('.cartel').hide();
        $('#save').show();
        ctx.save();
        ctx.font = "20px consolas";
        for( var i in all){
          if( all[i].color === 1){
              ctx.fillStyle = '#fff';
          }else{
            ctx.fillStyle = 'black';
          }
          ctx.textAlign = 'center';
          ctx.textBaseline = 'middle';

          ctx.fillText(all[i].step,
            (all[i].x+0.5)*blockS,
            (all[i].y+0.5)*blockS);
        }
        ctx.restore();
        var image = $('#canvas').get(0).toDataURL('image/jpg',1);
        $('#save').attr('href',image);
        $('#save').attr('download','qipu.png');
      })

      $('.tips').on('click',false);
      $('#close').on('click',function(){
          $('.cartel').hide();
      })
      $('.cartel').on('click',function(){
        $(this).hide();
      })
    })
