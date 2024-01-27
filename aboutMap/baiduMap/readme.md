### 简介
    当前项目是可以实现离线百度地图，将下载好的地图瓦片放在maptitle文件夹中，然后设置好显示层级和一个中心点，就可以了！主要js代码在map.html中
### 项目说明:  
- 在IP网管页面的选择某一个设备进入到详情页面，点击详情页面中的设备的位置图标进入到地图页面;  
- 地图页面的显示：
- level:13-16;一开始显示设备在地图的位置(level:12);鼠标滑动加大level,直到16不在变化;鼠标可以滑动,拖动地图;鼠标放在设备上可以有弹框显示设备的具体信息;
### 项目开发:  
- C#下载地图瓦片的12-16的全国地图;调用百度地图API;地图瓦片大小：(12-13 40万张图片 1.22G;14    200万 2166345   15    800万    占用空间：19.4G )
### 文档：
- 百度地图api:http://lbsyun.baidu.com/jsdemo.htm#a1_2
- http://d0.map.baidu.com/resource/mappic/
- http://or2.map.bdimg.com:8080/tile/?qt=tile&x=6536&y=1797&z=15&styles=pl&udt=20130822
### 资料：
#### 地图的计算
kc.getTilesUrl=function(a,b){var c=a.x,d=a.y,e=256*Math.pow(2,20-b),d=Math.round((9998336-e*d)/e)-1;return url=this.yA[Math.abs(c+d)%this.yA.length]+this.map.zb+"/"+this.map.Yr+"/3/lv"+(21-b)+"/"+c+","+d+".jpg"};

kc.getTilesUrl = function(a, b) {
    var c = a.x,
    d = a.y,
    e = 256 * Math.pow(2, 20 - b),
    d = Math.round((9998336 - e * d) / e) - 1;
    return url = this.yA[Math.abs(c + d) % this.yA.length] + this.map.zb + "/" + this.map.Yr + "/3/lv" + (21 - b) + "/" + c + "," + d + ".jpg"
};  

a: x = 6536  y = 1797
b: 15
c: "normal"  

jc.getTilesUrl = function(a, b, c) {
    var d = a.x,         //d = 6536  
    a = a.y,             //a = 1797
    e = "pl";            //e = "pl"
    this.map.$g();       //
    e = ic[c];
    var yyy=(hc[Math.abs(d + a) % hc.length] + "?qt=tile&x=" + (d + "").replace(/-/gi, "M") + "&y=" + (a + "").replace(/-/gi, "M") + "&z=" + b + "&styles=" + e + (6 == t.M.S ? "&color_dep=32&colors=50": "") + "&udt=20130822").replace(/-(\d+)/gi, "M$1");  

图块坐标
1,3  2,3  3,3
1,2  2,2  3,2
1,1  2,1  3,1  

###### 地图(最低是第4级)
- http://online0.map.bdimg.com/tile/?qt=tile&x=6536&y=1797&z=15&styles=pl
- http://or2.map.bdimg.com:8080/tile/?qt=tile&x=6536&y=1797&z=15&styles=pl&udt=20130822  

###### 路网
- http://or2.map.bdimg.com:8080/tile/?qt=tile&x=52294&y=14384&z=18&styles=sl
- http://or2.map.bdimg.com:8080/tile/?qt=tile&x=52295&y=14383&z=18&styles=sl&udt=20130712  

###### 全景图
- http://pcsv0.map.bdimg.com/tile/?udt=v&qt=tile&styles=pl&x=52294&y=14384&z=18  

###### 卫星图(最低是第1级)
- http://shangetu3.map.bdimg.com/it/u=x=52295;y=14383;z=18;v=009;type=sate&fm=46  

###### 将瓦片地址改为本地图片
jc.getTilesUrl = function(a, b, c) {
    var d = a.x,
        a = a.y,
        e = "pl";
    this.map.$g();
    e = ic[c];
    //return (hc[Math.abs(d + a) % hc.length] + "?qt=tile&x=" + (d + "").replace(/-/gi, "M") + "&y=" + (a + "").replace(/-/gi, "M") + "&z=" + b + "&styles=" + e + (6 == t.M.S ? "&color_dep=32&colors=50" : "") + "&udt=20130822").replace(/-(\d+)/gi, "M$1")
    return "maptile/" + b + "/" + d + "/" + a + ".jpg"
};  

###### 禁用canvas（IE8本来就不支持，对于Chrome、Firefox、IE9以上要通过源代码来禁用）
- 如果使用canvas，就不会使用瓦片图，所以这个函数改为直接返回false
Dc: function() {
    var a = this.U() >= this.F.Ou && this.ha() == ra && 18 >= this.U(),
        b = o;
    try {
        document.createElement("canvas").getContext("2d"), b = i
    } catch (c) {
        b = o
    }
    //return a && b
    return false
},
        
###### 修改相关图片地址：(file:///D:/images/openhand.cur)//ca: "http://api0.map.bdimg.com/images/",ca: "./images/",
        
###### 修改blank.gif地址（不知道这个图片是干什么用的）        
//Sa.src = "http://api.map.baidu.com/images/blank.gif?" + a.src
Sa.src = "./images/blank.gif"



####地图需要的模块
###### 打开Fildder2，查看所有getmodules的网址
- http://api0.map.bdimg.com/getmodules?v=2.0&mod=marker_ptbbkx,panorama_h4nqoe,map_iud0mt,scommon_x0ooro,mapclick_llwkfr,oppc_cujud4,tile_co4sly,navictrl_fhkk1i
- http://api0.map.bdimg.com/getmodules?v=2.0&mod=copyrightctrl_rtz3dy
- http://api0.map.bdimg.com/getmodules?v=2.0&mod=hotspot_htf5xw
- http://api0.map.bdimg.com/getmodules?v=2.0&mod=draw_1uiavz,drawbysvg_bwklsk,drawbyvml_51f0oc,drawbycanvas_gpvidg,poly_0pzfca
- http://api0.map.bdimg.com/getmodules?v=2.0&mod=common_bmjtcd,infowindow_53rvc4

###### 汇总成一个网址，并保存该结果为getmodules。注意顺序，不同的模块有依赖关系，如果顺序错误，就会导致无法运行！！！！
- http://api0.map.bdimg.com/getmodules?v=2.0&mod=marker_ptbbkx,panorama_h4nqoe,map_iud0mt,scommon_x0ooro,mapclick_llwkfr,oppc_cujud4,tile_co4sly,navictrl_fhkk1i,copyrightctrl_rtz3dy,hotspot_htf5xw,draw_1uiavz,drawbysvg_bwklsk,drawbyvml_51f0oc,drawbycanvas_gpvidg,poly_0pzfca,common_bmjtcd,infowindow_53rvc4

- 也可用这个最全的网址，但是生成的文件较大，有700多K，可以考虑通过解析参数来动态生成这个文件.注意顺序，不同的模块有依赖关系，如果顺序错误，就会导致无法运行！！！！
- http://api0.map.bdimg.com/getmodules?v=2.0&mod=marker_ptbbkx,panoramaservice_qeojoi,panorama_h4nqoe,panoramaflash_ovaxkh,map_iud0mt,scommon_x0ooro,mapclick_llwkfr,oppc_cujud4,tile_co4sly,navictrl_fhkk1i,copyrightctrl_rtz3dy,hotspot_htf5xw,menu_afolxc,opmb_qhltj4,common_bmjtcd,draw_1uiavz,coordtrans_ifnwg5,local_kq2o2m,route_mmq15s,othersearch_o2m2t1,autocomplete_l3nwcm,infowindow_53rvc4,drawbysvg_bwklsk,drawbyvml_51f0oc,drawbycanvas_gpvidg,poly_0pzfca,coordtransutils_cohv5l,clayer_cgg5rd,buslinesearch_24c22h,geoctrl_hvlbja,markeranimation_vgemto,vector_fj1lpf,control_akds3z
- 最新的：
http://api0.map.bdimg.com/getmodules?v=2.0&mod=marker_sibaye,panoramaservice_qeojoi,panorama_im2d2t,panoramaflash_ovaxkh,map_t5jg4o,scommon_0w53w5,mapclick_i0dlab,oppc_0ivujw,tile_q2mnnx,navictrl_arfxo2,copyrightctrl_hc1pfy,hotspot_bqyvao,menu_owoyra,opmb_j10oke,common_e3srsg,draw_ojumfh,coordtrans_ace4nl,local_2oujkj,route_35rb03,othersearch_evpsqr,autocomplete_bufwgb,infowindow_io0n23,drawbysvg_p5mxj4,drawbyvml_u0rhxm,drawbycanvas_dz004b,poly_4djeai,coordtransutils_xib5tn,clayer_0zplsz,buslinesearch_eyhblc,geoctrl_dftw2h,markeranimation_2fzw23,vector_0uvhvq,control_0kgcrt        
    
通过以下数组和nb() ? a = "drawbysvg": mb() ? a = "drawbyvml": ob() && (a = "drawbycanvas");可以生成这个网址：
    var pb = {
        map: "iud0mt",
        common: "bmjtcd",
        tile: "co4sly",
        marker: "ptbbkx",
.........
        vector: "fj1lpf"
    };

修改getmodules，将远程图片改为本地图片
http://api0.map.bdimg.com/images/
./images/

修改apiv2.0.js：
将
            //tB: "http://api0.map.bdimg.com/getmodules?v=2.0",
修改为：
            tB: "./js/getmodules",

将
                        //0 == a.length ? e.ny() : La(e.Vu.tB + "&mod=" + a.join(","))
修改为：
                        0 == a.length ? e.ny() : La(e.Vu.tB)

- !!!全景图!!!全景图模式必须在服务器环境下才能使用（即必须启动Apache）swfSrc:"http://api.map.baidu.com/res/swf/APILoader.swf"


#### 瓦片图
http://pcsv2.map.bdimg.com/scape/?qt=pdata&sid=0100010000130501111158026Z5&pos=4_1&z=5

pos=4_1： 例如，z=4时，第一个数字范围0-7（垂直方向的从上到下）， 第二个数字范围0-15（表示水平360度，从北开始顺时针方向）
z=1：放大级别1，1张图，垂直=0，水平=0
z=2：放大级别2，2张图，垂直=0，水平0-1
z=3：放大级别3，4张图，垂直0-1，水平0-3,
z=4：放大级别4，32张图，垂直0-3，水平0-7,
z=5：放大级别5，128张图，垂直0-7，水平0-15

平面坐标： x=13392993.66&y=3685722.2

根据坐标获取信息
http://pcsv0.map.bdimg.com/scape/?qt=qscb&l=17&x=13392993.66&y=3685722.2&action=1&fn=BMap._rd._cbk81366
根据id获取信息
http://pcsv0.map.bdimg.com/scape/?qt=scb&l=17&sid=0100010000130501092341622Z2&action=1&fn=BMap._rd._cbk81366


BMap._rd._cbk81366({"content":[{"Admission":"GS(2013)6021","Date":"20130501","DeviceHeight":2.15,"FileTag":"pano_cfg","ID":"0100010000130501092341622Z2","ImgLayer":[{"BlockX":2,"BlockY":1,"ImgFormat":"jpg","ImgLevel":1},{"BlockX":4,"BlockY":2,"ImgFormat":"jpg","ImgLevel":2},{"BlockX":8,"BlockY":4,"ImgFormat":"jpg","ImgLevel":3},{"BlockX":16,"BlockY":8,"ImgFormat":"jpg","ImgLevel":4}],"LayerCount":4,"Links":[],"Mode":"day","MoveDir":-88.775,"NorthDir":358.78,"Pitch":1.309,"Provider":1,"RX":1339298925,"RY":368567874,"Rname":"崇宁路","Roads":[{"ID":"3dda98-cfa3-5f3b-a55c-0d02de","IsCurrent":1,"Name":"崇宁路","Panos":[{"DIR":89,"Order":0,"PID":"0100010000130501092418039Z2","X":1339289695,"Y":368568933},{"DIR":89,"Order":1,"PID":"0100010000130501092415856Z2","X":1339290276,"Y":368568937},{"DIR":90,"Order":2,"PID":"0100010000130501092413867Z2","X":1339290878,"Y":368568938},{"DIR":90,"Order":3,"PID":"0100010000130501092412011Z2","X":1339291477,"Y":368568934},{"DIR":91,"Order":4,"PID":"0100010000130501092410333Z2","X":1339292097,"Y":368568927},{"DIR":91,"Order":5,"PID":"0100010000130501092408633Z2","X":1339292751,"Y":368568911},{"DIR":91,"Order":6,"PID":"0100010000130501092407074Z2","X":1339293348,"Y":368568892},{"DIR":91,"Order":7,"PID":"0100010000130501092405337Z2","X":1339293952,"Y":368568875},{"DIR":92,"Order":8,"PID":"0100010000130501092403538Z2","X":1339294574,"Y":368568854},{"DIR":93,"Order":9,"PID":"0100010000130501092401479Z2","X":1339295158,"Y":368568827},{"DIR":93,"Order":10,"PID":"0100010000130501092355423Z2","X":1339295589,"Y":368568804},{"DIR":92,"Order":11,"PID":"0100010000130501092351537Z2","X":1339295990,"Y":368568779},{"DIR":93,"Order":12,"PID":"0100010000130501092349838Z2","X":1339296532,"Y":368568754},{"DIR":91,"Order":13,"PID":"0100010000130501092347947Z2","X":1339297109,"Y":368568723},{"DIR":91,"Order":14,"PID":"0100010000130501092345759Z2","X":1339297719,"Y":368568702},{"DIR":91,"Order":15,"PID":"0100010000130501092343623Z2","X":1339298315,"Y":368568684},{"DIR":92,"Order":16,"PID":"0100010000130501092341622Z2","X":1339298915,"Y":368568665},{"DIR":97,"Order":17,"PID":"0100010000130501092321200Z2","X":1339299712,"Y":368568634},{"DIR":95,"Order":18,"PID":"0100010000130501092319036Z2","X":1339300261,"Y":368568562},{"DIR":89,"Order":19,"PID":"0100010000130501092317539Z2","X":1339300930,"Y":368568497},{"DIR":0,"Order":20,"PID":"0100010000130501092316249Z2","X":1339301537,"Y":368568471}],"Width":550}],"Roll":0.957,"SwitchID":[],"Time":"2013","Type":"street","Version":"0","X":1339298915,"Y":368568665,"Z":13,"plane":"","pois":[{"bus":"","catalog":"010501","dir":1,"id":"4ea3f2f189d254b3afcb6692","importance":0,"ismodified":1,"name":"文渊坊","pid":"0100010000130501092442051Z2","pitch":6,"rank":380,"x":1339281800,"y":368570101,"zoom":"1.3000000000000000444"},{"bus":"","catalog":"01010109","dir":345,"id":"50f7d1469fad88dd73210bb2","importance":0,"ismodified":1,"name":"兰州正宗牛肉拉面(无锡锦江大酒店东)","pid":"0100010000130501092321200Z2","pitch":1,"rank":-15,"x":1339299300,"y":368569700,"zoom":"1.3100000000000000533"},{"bus":"","catalog":"010301","dir":329,"id":"4dec1e19d63a09212ee67bf6","importance":0,"ismodified":1,"name":"东方巴黎东门","pid":"0100010000130501090429115Z2","pitch":358,"rank":107,"x":1339286601,"y":368561150,"zoom":"1.1000000000000000888"}]}],"result":{"action":1,"error":0}});

{
    "content": [
        {
            "Admission": "GS(2013)6021",
            "Date": "20130501",
            "DeviceHeight": 2.15,
            "FileTag": "pano_cfg",
            "ID": "0100010000130501092341622Z2",
            "ImgLayer": [
                {
                    "BlockX": 2,
                    "BlockY": 1,
                    "ImgFormat": "jpg",
                    "ImgLevel": 1
                },
                {
                    "BlockX": 4,
                    "BlockY": 2,
                    "ImgFormat": "jpg",
                    "ImgLevel": 2
                },
                {
                    "BlockX": 8,
                    "BlockY": 4,
                    "ImgFormat": "jpg",
                    "ImgLevel": 3
                },
                {
                    "BlockX": 16,
                    "BlockY": 8,
                    "ImgFormat": "jpg",
                    "ImgLevel": 4
                }
            ],
            "LayerCount": 4,
            "Links": [],
            "Mode": "day",
            "MoveDir": -88.775,
            "NorthDir": 358.78,
            "Pitch": 1.309,
            "Provider": 1,
            "RX": 1339298925,
            "RY": 368567874,
            "Rname": "崇宁路",
            "Roads": [
                {
                    "ID": "3dda98-cfa3-5f3b-a55c-0d02de",
                    "IsCurrent": 1,
                    "Name": "崇宁路",
                    "Panos": [
                        {
                            "DIR": 89,
                            "Order": 0,
                            "PID": "0100010000130501092418039Z2",
                            "X": 1339289695,
                            "Y": 368568933
                        },
                        {
                            "DIR": 89,
                            "Order": 1,
                            "PID": "0100010000130501092415856Z2",
                            "X": 1339290276,
                            "Y": 368568937
                        },
                        {
                            "DIR": 90,
                            "Order": 2,
                            "PID": "0100010000130501092413867Z2",
                            "X": 1339290878,
                            "Y": 368568938
                        },
                        {
                            "DIR": 90,
                            "Order": 3,
                            "PID": "0100010000130501092412011Z2",
                            "X": 1339291477,
                            "Y": 368568934
                        },
                        {
                            "DIR": 91,
                            "Order": 4,
                            "PID": "0100010000130501092410333Z2",
                            "X": 1339292097,
                            "Y": 368568927
                        },
                        {
                            "DIR": 91,
                            "Order": 5,
                            "PID": "0100010000130501092408633Z2",
                            "X": 1339292751,
                            "Y": 368568911
                        },
                        {
                            "DIR": 91,
                            "Order": 6,
                            "PID": "0100010000130501092407074Z2",
                            "X": 1339293348,
                            "Y": 368568892
                        },
                        {
                            "DIR": 91,
                            "Order": 7,
                            "PID": "0100010000130501092405337Z2",
                            "X": 1339293952,
                            "Y": 368568875
                        },
                        {
                            "DIR": 92,
                            "Order": 8,
                            "PID": "0100010000130501092403538Z2",
                            "X": 1339294574,
                            "Y": 368568854
                        },
                        {
                            "DIR": 93,
                            "Order": 9,
                            "PID": "0100010000130501092401479Z2",
                            "X": 1339295158,
                            "Y": 368568827
                        },
                        {
                            "DIR": 93,
                            "Order": 10,
                            "PID": "0100010000130501092355423Z2",
                            "X": 1339295589,
                            "Y": 368568804
                        },
                        {
                            "DIR": 92,
                            "Order": 11,
                            "PID": "0100010000130501092351537Z2",
                            "X": 1339295990,
                            "Y": 368568779
                        },
                        {
                            "DIR": 93,
                            "Order": 12,
                            "PID": "0100010000130501092349838Z2",
                            "X": 1339296532,
                            "Y": 368568754
                        },
                        {
                            "DIR": 91,
                            "Order": 13,
                            "PID": "0100010000130501092347947Z2",
                            "X": 1339297109,
                            "Y": 368568723
                        },
                        {
                            "DIR": 91,
                            "Order": 14,
                            "PID": "0100010000130501092345759Z2",
                            "X": 1339297719,
                            "Y": 368568702
                        },
                        {
                            "DIR": 91,
                            "Order": 15,
                            "PID": "0100010000130501092343623Z2",
                            "X": 1339298315,
                            "Y": 368568684
                        },
                        {
                            "DIR": 92,
                            "Order": 16,
                            "PID": "0100010000130501092341622Z2",
                            "X": 1339298915,
                            "Y": 368568665
                        },
                        {
                            "DIR": 97,
                            "Order": 17,
                            "PID": "0100010000130501092321200Z2",
                            "X": 1339299712,
                            "Y": 368568634
                        },
                        {
                            "DIR": 95,
                            "Order": 18,
                            "PID": "0100010000130501092319036Z2",
                            "X": 1339300261,
                            "Y": 368568562
                        },
                        {
                            "DIR": 89,
                            "Order": 19,
                            "PID": "0100010000130501092317539Z2",
                            "X": 1339300930,
                            "Y": 368568497
                        },
                        {
                            "DIR": 0,
                            "Order": 20,
                            "PID": "0100010000130501092316249Z2",
                            "X": 1339301537,
                            "Y": 368568471
                        }
                    ],
                    "Width": 550
                }
            ],
            "Roll": 0.957,
            "SwitchID": [],
            "Time": "2013",
            "Type": "street",
            "Version": "0",
            "X": 1339298915,
            "Y": 368568665,
            "Z": 13,
            "plane": "",
            "pois": [
                {
                    "bus": "",
                    "catalog": "010501",
                    "dir": 1,
                    "id": "4ea3f2f189d254b3afcb6692",
                    "importance": 0,
                    "ismodified": 1,
                    "name": "文渊坊",
                    "pid": "0100010000130501092442051Z2",
                    "pitch": 6,
                    "rank": 380,
                    "x": 1339281800,
                    "y": 368570101,
                    "zoom": "1.3000000000000000444"
                },
                {
                    "bus": "",
                    "catalog": "01010109",
                    "dir": 345,
                    "id": "50f7d1469fad88dd73210bb2",
                    "importance": 0,
                    "ismodified": 1,
                    "name": "兰州正宗牛肉拉面(无锡锦江大酒店东)",
                    "pid": "0100010000130501092321200Z2",
                    "pitch": 1,
                    "rank": -15,
                    "x": 1339299300,
                    "y": 368569700,
                    "zoom": "1.3100000000000000533"
                },
                {
                    "bus": "",
                    "catalog": "010301",
                    "dir": 329,
                    "id": "4dec1e19d63a09212ee67bf6",
                    "importance": 0,
                    "ismodified": 1,
                    "name": "东方巴黎东门",
                    "pid": "0100010000130501090429115Z2",
                    "pitch": 358,
                    "rank": 107,
                    "x": 1339286601,
                    "y": 368561150,
                    "zoom": "1.1000000000000000888"
                }
            ]
        }
    ],
    "result": {
        "action": 1,
        "error": 0
    }
}


#### 坐标纠偏
    纠偏查询：多个经纬度用逗号分隔
    http://api.map.baidu.com/ag/coord/convert?x=116.397428,116.397428&y=39.75923,39.75923&from=0&to=4&mode=1

    结果
    [{"error":0,"x":"MTE2LjQxMDA1NzAwODk3","y":"MzkuNzY2OTc4MTk2Nzc1"},{"error":0,"x":"MTE2LjQxMDA1NzAwODk3","y":"MzkuNzY2OTc4MTk2Nzc1"}]

    将 MTE2LjQxMDA1NzAwODk3 、 MzkuNzY2OTc4MTk2Nzc1 按base64解码后就是经纬度 116.41005700897， 39.766978196775

    将纠偏后的百度经纬度 - 输入的GPS经纬度 = 纠偏参数（保留小数点后6位即可）

    PS:apiv2.0.js中搜索"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789"可以找到base64解码的相关函数

#### 一些地理坐标 不用关心
中国
最左：73.500623,39.409692
最右：135.11087,48.430806

最上：123.276809,53.583169
最下：109.584459,18.16375

经度：73.50 - 135.11
纬度：18.16 - 53.58
（忽略南海）

SELECT (13511 - 7350) * (5358 - 1816) FROM dual

21822262 条记录
25273314 => 1.02G
=================================================
无锡
119.48 - 120.64
31.1  -  32.01

10-18级
=================================================
经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：13300597, 3741765
图块坐标：51955, 14616
可视区域坐标：-86425, -59177
覆盖物坐标：-86425, -59177
放大界别：18

右下角
经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：13429729, 3623469
图块坐标：52459, 14154
可视区域坐标：42707, 59120
覆盖物坐标：42707, 59120
放大界别：18

52459 - 51955 = 504
14616 - 14154 = 462
504 * 462 = 232848
232848 * 2353 = 547891344 byte = 535050 KB = 522 MB

=================================================
经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：6650298, 1870882
图块坐标：25977, 7308
可视区域坐标：-42962, -29438
覆盖物坐标：-42962, -29438
放大界别：17

经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：6714864, 1811734
图块坐标：26229, 7077
可视区域坐标：21604, 29710
覆盖物坐标：21604, 29710
放大界别：17

26229 - 25977 = 252
7308 - 7077 = 231
252 * 231 = 58212
58212 * 5237 = 304856244 byte = 297711 KB = 291 MB

=================================================
经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：3357432, 905867
图块坐标：13114, 3538
可视区域坐标：11052, 15005
覆盖物坐标：11052, 15005
放大界别：16

经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：3325149, 935441
图块坐标：12988, 3654
可视区域坐标：-21231, -14569
覆盖物坐标：-21231, -14569
放大界别：16

13114 - 12988 = 126
3654 - 3538 = 116
126 * 116 = 14616
14616 * 4942 = 72232272 byte = 70539 KB = 69 MB

=================================================

经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：1678716, 452933
图块坐标：6557, 1769
可视区域坐标：5776, 7651
覆盖物坐标：5776, 7652
放大界别：15


经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：1662574, 467720
图块坐标：6494, 1827
可视区域坐标：-10366, -7135
覆盖物坐标：-10366, -7135
放大界别：15
=================================================

经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：839358, 226466
图块坐标：3278, 884
可视区域坐标：3138, 3976
覆盖物坐标：3138, 3976
放大界别：14


经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：831287, 233860
图块坐标：3247, 913
可视区域坐标：-4933, -3417
覆盖物坐标：-4933, -3417
放大界别：14
=================================================

经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：419679, 113233
图块坐标：1639, 442
可视区域坐标：1819, 2138
覆盖物坐标：1819, 2138
放大界别：13

经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：415643, 116930
图块坐标：1623, 456
可视区域坐标：-2216, -1559
覆盖物坐标：-2216, -1559
放大界别：13
=================================================

经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：209839, 56616
图块坐标：819, 221
可视区域坐标：1159, 1219
覆盖物坐标：1159, 1219
放大界别：12


经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：207821, 58465
图块坐标：811, 228
可视区域坐标：-858, -629
覆盖物坐标：-858, -629
放大界别：12
=================================================

经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：104919, 28308
图块坐标：409, 110
可视区域坐标：830, 760
覆盖物坐标：830, 760
放大界别：11


经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：103910, 29232
图块坐标：405, 114
可视区域坐标：-179, -165
覆盖物坐标：-179, -165
放大界别：11
=================================================

经纬度：120.64, 31.1
平面坐标：13429729.49, 3623469.36
像素坐标：52459, 14154
图块坐标：204, 55
可视区域坐标：665, 530
覆盖物坐标：665, 530
放大界别：10


经纬度：119.48, 32.01
平面坐标：13300597.48, 3741765.79
像素坐标：51955, 14616
图块坐标：202, 57
可视区域坐标：160, 68
覆盖物坐标：160, 68
放大界别：10



