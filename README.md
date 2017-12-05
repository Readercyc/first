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
