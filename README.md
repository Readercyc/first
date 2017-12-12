#include<cstdio>
#include<iostream>
#include<stack>
#include<queue>
using namespace std;
struct car{
	char car_state;
	int car_num;
	int car_time;
} Car;
int main(){
	int total_car;
	cout<<"请输入停车场容量"<<endl;
	cin>>total_car;
	car all_car;
	car temp_car;
	car queue_car;
	stack <struct car> parking_lot;
	stack <struct car> temp_parking_lot;
	queue <struct car> outside_park;
	cout<<"请输入车的状态（进入或离开）以及车牌号（整数）以及时间（整数）"<<endl;
	while(1)
	{

        
        scanf("%c %d %d",&all_car.car_state,&all_car.car_num,&all_car.car_time);
		if(all_car.car_state == 'E')
			break;

		if(all_car.car_state == 'A')
		{


			if(parking_lot.size()+1<=total_car)
			{
				parking_lot.push(all_car);
				cout<<"成功停入停车场!"<<endl;
                cout<<"现在停车场里有"<<parking_lot.size()<<"辆车"<<endl;
				cout<<"您现在在停车场里的位置为"<<parking_lot.size()<<endl;
			}
			else
			{
				outside_park.push(all_car);
				cout<<"现在停车场里有"<<parking_lot.size()<<"辆车"<<endl;
				cout<<"停车场已满，暂时停入过道"<<endl;
			}
		}
		if(all_car.car_state == 'D')
		{
            while(1)
            {

                temp_car = parking_lot.top();
                if(temp_car.car_num == all_car.car_num)
                {
                    cout<<"已找到您的车辆"<<endl;
                    cout<<"您的停车时间为"<<all_car.car_time - temp_car.car_time<<"分钟"<<endl;
                    cout<<"您应付的金额为"<<all_car.car_time - temp_car.car_time<<"元"<<endl;
                    parking_lot.pop();
                    while(!temp_parking_lot.empty())
                    {
                        parking_lot.push(temp_parking_lot.top());
                        temp_parking_lot.pop();
                    }
                    if(!outside_park.empty())
                    {
                        queue_car = outside_park.front();
                        cout<<"过道的车辆:"<<queue_car.car_num<<" 可停入停车场"<<endl;
                        parking_lot.push(queue_car);
                        outside_park.pop();
                    }
                    else{

                        cout<<"过道上没有车辆"<<endl;
                    }
                    break;

                }
                else
                {
                    temp_parking_lot.push(temp_car);
                    parking_lot.pop();
                }

            }

		}
	}

	return 0;
}

#include <iostream>  
#include <string>  
#include <vector>  
using namespace std;  
  
void Min(string t,vector<int>& key)  
{  
    string temp1; //子串前缀  
    string temp2; //子串后缀  
    int i=2,j=1,k,len=t.length();  
    //vector<int> key;  
    while(i<len) //长度为i的子串  
    {  
        //if(i==1)  
            //key[j]=0;  
        k=1;  
        while(k<i) //长度为i的子串有i-1个前/后缀，同级相比较  
        {  
            temp1=t.substr(0,k);  
            temp2=t.substr(i-k,k);  
            if(temp1==temp2)  
                key[j]=temp1.length();  
            ++k;  
        }  
        ++j;  
        ++i;  
    }  
}  
  
int Index(string s,string t,int pos)  
{  
    int i=pos-1,slen=s.length(),tlen=t.length();  
    vector<int> key;  
    for(int a=0;a<tlen;++a)  
        key.push_back(0);  
    Min(t,key);  
    int j=0;  
    int k=0;  
    int ppos=0;  
    while(1)  
    {  
        if(s[j]!=t[k])  
        {  
            if(k==0)  
            {  
                ++j;  
                ++ppos;  
                continue;  
            }  
            else  
            {  
                ppos+=k-key[k-1];  
                j=ppos;  
                k=0;  
            }  
        }  
        else if(s[j]==t[k])  
        {  
            if(k==tlen-1)  
                return ppos+1;  
            else  
            {  
                ++k;  
                ++j;  
            }  
        }  
        if(j==slen)  
            return -1;  
    }  
}  
  
int main()  
{  
	cout<<"请输入需要进行匹配的字符串"<<endl; 
    string S;
    string model;
	cin>>S;  
    cout<<"请输入模式串"<<endl;
    cin>>model; 
    int v=Index(S,model,1);  
    if(v>=0)
        cout<<"串T在串S中首次出现的位置是："<<Index(S,model,1)<<endl;  
    else  
        cout<<"串T不是串S的子串."<<endl;
	return 0;  
}  

#include<cstdio>
#include<iostream>
using namespace std;
int main()
{
	int card[111111]={0,1};
	int n;
	//结论就是所有的平方数都一样 
	while(1)
	{	
		//方案1 
		cout<<"请输入任意牌数"<<endl;
		cin>>n;
		/*int m = 1;
		for(;m*m<=n;m++)
			cout<<"第"<<m*m<<"张纸牌是正面朝上的"<<endl; */
		//方案2 
		if(n==0)
			break;
		for(int i=2;i<=n;i++)
			for(int j=i;j<=n;j+=i)
			{
				if(card[j]==1)
					card[j] = 0;
				else
					card[j] = 1;
			}
		for(int i=1;i<=n;i++)
			if(card[i]==0)
				cout<<"第"<<i<<"张纸牌是正面朝上的"<<endl; 
		}
	
	return 0;
}
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" >
<head>
    <title>Untitled Page</title>
    <style>
        body
        {
            background-color:#333333;
        }
        
        .card
        {
            display:inline-block;
            height:140px;
            width:100px;
            margin-left:10px;
            background-image:url(./zhengmian.png);
            background-size:100% 100%;
        }
         .card_bg
        {
            display:inline-block;
            height:140px;
            width:100px;
            margin-left:10px;
            background-image:url(./beimian.jpg);
            background-size:100% 100%;
        }
       button
        {
            width:80px;
            margin:0 auto;
            display:block;
            background-color:#ddd;
        }
    </style>
    <script src="jquery.js"></script>
    <script>
        var i = 2;
        var card = document.getElementsByTagName("div");
        /*console.log(card);*/
        function start() {
            time = setInterval(change_card, 300);
        }
        function change_card() {
            if (i > 52)
                clearInterval(time);
            for (var j = i; j <= 52; j += i) {
                $(card[j]).toggleClass("card");
                $(card[j]).toggleClass("card_bg");
            }
            i++;
        }
    </script>
</head>
<body>
      <div class="card" style="width:0px;margin:0;display:none"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
       <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
       <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
       <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <div class="card"></div>
      <button onclick="start()">开始演示</button>
</body>
</html>

#include <iostream>
#include <string>
#include <time.h>
using namespace std;
#define MaxSize 34
#define N 4
int color[10]={0};
string name[34]={"广西","广东","云南","贵州","湖南","江西","福建",
              "浙江","安徽","湖北","重庆","四川","西藏","青海",
           "新疆","甘肃","陕西","宁夏","内蒙","北京","黑龙江",
     "吉林","辽宁","天津","河北","山西","河南","江苏",
              "山东","上海","海南","台湾","香港","澳门"};
// 1、广西; 2、广东; 3、云南; 4、贵州; 5、湖南; 6、江西; 7、福建;
// 8、浙江; 9、安徽;10、湖北;11、重庆;12、四川;13、西藏;14、青海;
//15、新疆;16、甘肃;17、陕西;18、宁夏;19、内蒙;20、北京;21、黑龙江;
//22、吉林;23、辽宁;24、天津;25、河北;26、山西;27、河南;28、江苏;
//29、山东;30、上海;31、海南;32、台湾;33、香港;34、澳门;
int shengguanxi[35][35]={{0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//0
 {0,0,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//1
 {0,1,0,0,0,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1},//2
 {0,1,0,0,1,0,0,0,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//3
 {0,1,0,1,0,1,0,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//4
 {0,1,1,0,1,0,1,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//5
 {0,0,1,0,0,1,0,1,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//6
 {0,0,1,0,0,0,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//7
 {0,0,0,0,0,0,1,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,0,0,0},//8
 {0,0,0,0,0,0,1,0,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,0,0,0,0,0},//9
 {0,0,0,0,0,1,1,0,0,1,0,1,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0},//10
 {0,0,0,0,1,1,0,0,0,0,1,0,1,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//11
 {0,0,0,1,1,0,0,0,0,0,0,1,0,1,1,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//12
 {0,0,0,1,0,0,0,0,0,0,0,0,1,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//13
 {0,0,0,0,0,0,0,0,0,0,0,0,1,1,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//14
 {0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//15
 {0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,1,0,1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//16
 {0,0,0,0,0,0,0,0,0,0,1,1,1,0,0,0,1,0,1,1,0,0,0,0,0,0,1,1,0,0,0,0,0,0,0},//17
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//18
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,0,0,1,1,1,0,1,1,0,0,0,0,0,0,0,0},//19
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0},//20

{0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0},//21
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,1,0,0,0,0,0,0,0,0,0,0,0},//22
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,1,0,0,0,0,0,0,0,0,0},//23
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,1,0,0,0,0,0,0,0,0,0},//24
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,1,1,0,1,1,0,1,0,0,0,0,0},//25
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,0,0,0,0,0,1,0,1,0,0,0,0,0,0,0},//26
 {0,0,0,0,0,0,0,0,0,1,1,0,0,0,0,0,0,1,0,0,0,0,0,0,0,1,1,0,0,1,0,0,0,0,0},//27
 {0,0,0,0,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,0},//28
 {0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,1,1,0,0,0,0,0,0},//29
 {0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0},//30
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//31
 {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//32
 {0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//33
 {0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0},//34
};

class ChinaMap
{
public:
 ChinaMap(){}
 ChinaMap(string SM[],int t,int b);
 ~ChinaMap(){}
    void ShowCM();
    int IsColorSame(int n);
 void ColorZL();
 void ShowColor();
 void ShangSe(int n);
private:
 string ShengMing[MaxSize+1];
    int ShengGX[MaxSize+1][MaxSize+1];
 int tNum,bNum;
};

ChinaMap::ChinaMap(string SM[],int t,int b)
{
 int i,j;
 tNum=t;
 bNum=b;
 for (i=1;i<=tNum;i++)
 {
  ShengMing[i]=SM[i-1];
 }
 for(i=0;i<=tNum;i++)
  for (j=0;j<=tNum;j++)
     ShengGX[i][j]=shengguanxi[i][j];
}
void ChinaMap::ShowCM()
{
 int i;
 cout<<"图的各顶点:"<<endl;
 for(i=1;i<=tNum;i++)
 { 
  cout<<ShengMing[i]<<"  ";
  if(i%7==0)
   cout<<endl;
 }
 cout<<endl;
/* cout<<"图的邻接矩阵:"<<endl;
 for (i=1;i<=tNum;i++)
 {
  for (j=1;j<=tNum;j++)
     cout<<ShengGX[i][j]<<"  ";
  cout<<endl;
 }*/
}

int ChinaMap::IsColorSame(int n)
{
 int i,flag=0;
 for (i=1;i<=n-1;i++)
 {
  if (ShengGX[i][n]==1&&color[i]==color[n])
  {
   flag=1;
   break;
  }
 }
 return flag;
}
void ChinaMap::ColorZL()
{
 int i;
    for (i=1;i<=tNum;i++)
    {
  cout<<ShengMing[i]<<":";
  switch (color[i])
  {
  case 1:cout<<"红色"<<"  ";
   break;
  case 2:cout<<"蓝色"<<"  ";
   break;
  case 3:cout<<"黄色"<<"  ";
   break;
  case 4:cout<<"绿色"<<"  ";
   break;
  case 5:cout<<"白色"<<"  ";
   break;
  case 6:cout<<"黑色"<<"  ";
   break;
  case 7:cout<<"橙色"<<"  ";
   break;
  default:
   break;
  }

if(i%7==0)
   cout<<endl;
    }
}
void ChinaMap::ShowColor()
{
// int i;
// for(i=1;i<=tNum;i++)
//  cout<<color[i]<<"  ";
 ColorZL();
 cout<<endl;
}
void ChinaMap::ShangSe(int n)
{
 int i;
 if (n>tNum)
 {
  ShowColor();
  exit(1);
 }
 else
 {
  for (i=1;i<=N;i++)
  {
   color[n]=rand()%N+1;
   if (IsColorSame(n)==0)
   {
    ShangSe(n+1);
   }
  }
 }
}
int main()

{
 srand((unsigned)time(NULL));
 
 ChinaMap cm(name,34,70); 
 cm.ShowCM();
 cout<<"着色方案:"<<endl;
 cm.ShangSe(1);
 return 0;
}

#include<stdio.h>
  
int color[100];
bool ok(int k,int c[][100])//判断顶点k的着色是否发生冲突
{
  int i,j;
  for(i=1;i<k;i++)
  {
    if(c[k][i]==1&&color[i]==color[k])
      return false;
  }
  return true;
}
  
void graphcolor(int n,int m,int c[][100])
{
  int i,k;
  for(i=1;i<=n;i++)
  color[i]=0;
  k=1;
  while(k>=1)
  {
    color[k]=color[k]+1;
    while(color[k]<=m)
      if(ok(k,c))
        break;
      else 
        color[k]=color[k]+1;//搜索下一个颜色
      if(color[k]<=m&&k==n)
      {
        for(i=1;i<=n;i++) 
          printf("%d",color[i]);
        printf("\n");
      }
      else if(color[k]<=m&&k<n)
        k=k+1;//处理下一个顶点
      else
      {
        color[k]=0;
        k=k-1;//回溯
      }
  }
}
void main()
{
    int i,j,n,m;
    int c[100][100];//存储n个顶点的无向图的数组
    printf("输入顶点数n和着色数m:\n");
    scanf("%d%d",&n,&m);
    printf("输入无向图的邻接矩阵:\n");
    for(i=1;i<=n;i++)
      for(j=1;j<=n;j++)
        scanf("%d",&c[i][j]);
    printf("着色所有可能的解:\n");
    graphcolor(n,m,c);
}
