
记得之前在别的网站上看到这个喜庆的春节灯笼效果，觉得非常吸引人。虽然网上有一些现成的API可以直接实现，比如这个[春节灯笼API](https://api.vvhan.com/article/denglong.html)，但使用后我发现两个问题：一是手机端访问时灯笼没有自适应，二是灯笼上的“春节快乐”四个字不能自定义。



> 为了解决这些问题，我找到了[这篇文章](https://cloud.tencent.com/developer/article/2222081):[豆荚加速器](https://yirou.org)，并“借鉴”了其中的源代码，稍加修改后转换成JavaScript方式引入使用。下面有完整的JS代码。



> 原文可查看效果：[张苹果博客灯笼效果](https://github.com)


### 一，引入使用



> 距离春节还有不到90天，赶紧试试吧！将以下JS在您的页面直接引入即可。



```
   
   <script src="https://www.vae.zhangweicheng.xyz/web/denglong.js?text=好好学习"> script>

```

### 二，完整JS代码



```
 // 张苹果博客：https://zhangpingguo.com/
 // 创建并添加元素
function createDengContainer() {
    const container = document.createElement('div');
    container.className = 'deng-container';

    // 从当前脚本的 URL 获取参数
    const scriptSrc = document.currentScript.src;
    const urlParams = new URLSearchParams(scriptSrc.split('?')[1]); // 获取 '?'
    const customText = urlParams.get('text'); // 获取参数名为'text'的值

    // 将获取的文本分割为字符数组，如果没有提供文本，则使用默认的“新年快乐”
    const texts = customText ? customText.split('') : ['新', '年', '快', '乐'];

    texts.forEach((text, index) => {
        const box = document.createElement('div');
        box.className = `deng-box deng-box${index + 1}`;

        const deng = document.createElement('div');
        deng.className = 'deng';

        const xian = document.createElement('div');
        xian.className = 'xian';

        const dengA = document.createElement('div');
        dengA.className = 'deng-a';

        const dengB = document.createElement('div');
        dengB.className = 'deng-b';

        const dengT = document.createElement('div');
        dengT.className = 'deng-t';
        dengT.textContent = text;

        dengB.appendChild(dengT);
        dengA.appendChild(dengB);
        deng.appendChild(xian);
        deng.appendChild(dengA);

        const shuiA = document.createElement('div');
        shuiA.className = 'shui shui-a';

        const shuiC = document.createElement('div');
        shuiC.className = 'shui-c';
        const shuiB = document.createElement('div');
        shuiB.className = 'shui-b';

        shuiA.appendChild(shuiC);
        shuiA.appendChild(shuiB);
        deng.appendChild(shuiA);
        box.appendChild(deng);
        container.appendChild(box);
    });

    document.body.appendChild(container);
}

// 添加CSS样式
function addStyles() {
    const style = document.createElement('style');
    style.type = 'text/css';
    style.textContent = `
        .deng-container {
            position: relative;
            top: 10px;
            opacity: 0.9;
            z-index: 9999;
            pointer-events: none;
        }
        .deng-box {
            position: fixed;
            right: 10px;
        }
        .deng-box1 { position: fixed; top: 15px; left: 20px; }
        .deng-box2 { position: fixed; top: 12px; left: 130px; }
        .deng-box3 { position: fixed; top: 10px; right: 110px; }
        .deng {
            position: relative;
            width: 120px;
            height: 90px;
            background: rgba(216, 0, 15, .8);
            border-radius: 50% 50%;
            animation: swing 3s infinite ease-in-out;
            box-shadow: -5px 5px 50px 4px #fa6c00;
        }
        .deng-a { 
            width: 100px; 
            height: 90px; 
            background: rgba(216, 0, 15, .1); 
            border-radius: 50%;  
            border: 2px solid #dc8f03; 
            margin-left: 7px; 
            display: flex; 
            justify-content: center; 
        }
        .deng-b { 
            width: 65px; 
            height: 83px; 
            background: rgba(216, 0, 15, .1); 
            border-radius: 60%; 
            border: 2px solid #dc8f03; 
        }
        .xian { 
            position: absolute; 
            top: -20px; 
            left: 60px; 
            width: 2px; 
            height: 20px; 
            background: #dc8f03; 
        }
        .shui-a { 
            position: relative; 
            width: 5px; 
            height: 20px; 
            margin: -5px 0 0 59px; 
            animation: swing 4s infinite ease-in-out; 
            transform-origin: 50% -45px; 
            background: orange; 
            border-radius: 0 0 5px 5px; 
        }
        .shui-b { 
            position: absolute; 
            top: 14px; 
            left: -2px; 
            width: 10px; 
            height: 10px; 
            background: #dc8f03; 
            border-radius: 50%; 
        }
        .shui-c { 
            position: absolute; 
            top: 18px; 
            left: -2px; 
            width: 10px; 
            height: 35px; 
            background: orange; 
            border-radius: 0 0 0 5px; 
        }
        .deng:before, .deng:after { 
            content: " "; 
            display: block; 
            position: absolute; 
            border-radius: 5px; 
            border: solid 1px #dc8f03; 
            background: linear-gradient(to right, #dc8f03, orange, #dc8f03, orange, #dc8f03); 
        }
        .deng:before { 
            top: -7px; left: 29px; height: 12px; width: 60px; z-index: 999; 
        }
        .deng:after { 
            bottom: -7px; left: 10px; height: 12px; width: 60px; margin-left: 20px; 
        }
        .deng-t { 
            font-family: '华文行楷', Arial, Lucida Grande, Tahoma, sans-serif; 
            font-size: 3.2rem; 
            color: #dc8f03; 
            font-weight: 700; 
            line-height: 85px; 
            text-align: center; 
        }
        @media (max-width: 768px) { 
            .deng-t { font-size: 2.5rem; }  
            .deng-box { transform: scale(0.5); top: -15px; }  
            .deng-box1 { left: -22%; }  
            .deng-box2 { left: 0px; }  
            .deng-box3 { right: 50px; }  
            .deng-box4 { right: -10px; }  
        }
        @keyframes swing { 
            0% { transform: rotate(-10deg); }  
            50% { transform: rotate(10deg); }  
            100% { transform: rotate(-10deg); }  
        }
    `;
    document.head.appendChild(style);
}

// 引入时调用
function init() {
    addStyles();
    createDengContainer();
}

// 调用初始化函数
init();

```

### 三，页面使用



```
html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>春节灯笼title>
head>
<body>
    
   <script src="./denglong.js?text=等着下班"> script>
 body>html>

```

### 四，效果图


![](https://img2024.cnblogs.com/blog/3395189/202411/3395189-20241101162212813-60579206.png)


