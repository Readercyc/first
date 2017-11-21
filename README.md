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

