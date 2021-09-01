## TCP/UDP ���

### TCP ���
![TCP](https://user-images.githubusercontent.com/64240637/131625126-1773b733-3985-46e6-969a-6daf373ac082.png)

source port : ����� ��Ʈ��ȣ    
destination port : ������ ��Ʈ��ȣ     
checksum : ����� �������� ������ Ȯ���ϱ� ���� �ʵ�   
flags(NS ~ FIN) : ȥ�� ���� ����� ����� ���� �ش� �÷��׵��� ���ȴ�   
ACK : ���ι�ȣ �ʵ忡 ���� ä���� ������ �˸��� �÷���, �ش� ���� 0�̸� ������ ���õȴ� (������ ��� ������ ��Ÿ����)  
SYN : ����� ������ �����Ҷ� ������ ��ȣ�� ����ȭ�� ���߱� ���� ���׸�Ʈ�̴� (��뿡 ���� ���� ��û�� ��Ÿ����)
FIN : ������� ������ �����ϰ� �ʹٴ� ��û�� ���׸�Ʈ�̴� (������ �����ϴ� ���� ��Ÿ����)    

<br>

### UDP ���

![udp-header](https://user-images.githubusercontent.com/64240637/131624293-739ceb3d-80de-447d-aeb7-22056265b38e.png)

source port : ����� ��Ʈ��ȣ
destination port : ������ ��Ʈ��ȣ
checksum : �����׸�, ����� �������� ������ Ȯ���ϱ� ���� �ʵ�

<br>

## TCP 3-Way-HandShake
TCP 3 Way-HandShake�� tcp/ip ���������� �̿��ؼ� ����� �ϴ� �������α׷��� �����͸� �����ϱ� ���� ���� __��Ȯ�� ������ �����ϱ� ���ؼ� ���� ��ǻ�Ϳ� ������ ������ �����ϴ� ������ ���Ѵ�__     
- ���� ��� �����͸� ������ �غ� �Ǿ��ٴ� ���� �����Ѵ�.    

#### TCP 3-Way-HandShake ����
![SYN](https://user-images.githubusercontent.com/64240637/131626291-51fde236-016b-4bb1-943f-e086c5396628.png)

1. Ŭ���̾�Ʈ�� ������ ������ ��û�ϱ� ���� SYN��Ŷ�� ������. �̶� Ŭ���̾�Ʈ�� SYN/ACK������ ��ٸ��� SYN_SENT���°� �ȴ�
2. ������ SYN��û�� ���� �� Ŭ���̾�Ʈ���� ��û�� �����Ѵٴ� ACK�� SYN flog�� ������ ��Ŷ�� �����Ѵ�. ���� ACK�� ���� ������ ��ٸ���. �̶� ������ SYN_RECEIVED ���°� �ȴ�
3. SYN+ACK�� ���� Ŭ���̾�Ʈ�� �������� ACK�� ������ ���� ������ �����Ǿ� �����͸� �ְ��ް� �ȴ�. �̶� ������ ���´� ESTABLISHED�̴�   
 
#### TCP 4-Way-HandShake ����
TCP 3-Way-HandShake�� tcp�� ������ �ʱ�ȭ �Ҷ� ����ϰ� TCP 4-Way-HandShake�� ������ �����ϱ� ���� ����ȴ�(��, ��� ����)
![4HAND](https://user-images.githubusercontent.com/64240637/131627793-aa40532c-ef27-4264-a11f-8909d69c3dfc.png)

1. Ŭ���̾�Ʈ�� ������ �����ϰڴٴ� FIN�÷��׸� ������ ������
2. ������ �ϴ� Ȯ�� �޽����� ������ ����� ������ ���������� TIME_WAIT ���¸� �����Ѵ�
3. ���� ������ ����� �������� ������ ����Ǿ��ٰ� Ŭ���̾�Ʈ���� FIN�÷��׸� �����Ѵ�
4. Ŭ���̾�Ʈ�� Ȯ���ߴٴ� ACK�� ������
5. ���� Ŭ���̾�Ʈ�� ������ ����� CLOSED�ȴ�


#### Q1. �������� FIN�� �����ϱ� ���� Ŭ���̾�Ʈ �ʿ��� ������ ��Ŷ�� ����� �����̳� ��Ŷ ���Ƿ� ���� ���������� ���� FIN��Ŷ���� �ʰ� �����ϴ� ��Ȳ�� �߻��ϸ� ��� �ϴ°�?
A1. Ŭ���̾�Ʈ�ʿ��� ������ �����Ų�� �ڴʰ� ��Ŷ�� �����ϸ� �ش� ��Ŷ�� DROP�ǰ� �����ʹ� ���ǵȴ�. �̷��� ��Ȳ�� ����Ͽ� Ŭ���̾�Ʈ�� �����κ��� FIN�� �����ϴ��� �����ð�����(����Ʈ 240��) ������ ���ܳ��� ��Ŷ�� ��ٸ��� ������ ��ģ�� == __TIME_WAIT__   

#### Q2. TCP�� ���� ���� ������ ���� ���� ���� �ܰ谡 ���̳��� ������ �����ΰ� ?
A2. Ŭ���̾�Ʈ�� ������ �����Ͱ� ���ٰ� �ص� �������� ������ �ϴ� �����Ͱ� ���� ���� �� �ֱ� ������ �켱 FIN�� ���� ACK�� ���� ������ ���� �����͸� ���� ���� �Ŀ� FIN�� ������

#### Q3. �ʱ� Sequence Number�� ISN�� 0���� �������� �ʰ� ������ �����ؼ� �����ϴ� ������ �����ΰ� ?
A3. �������� SYN�� ���� ��Ŷ�� �����ϴµ� ������ �ƴ� �������� NUMBER�� ���۵Ǹ� ���� Connection���κ��� ���� ��Ŷ���� �ν��� �� �ֱ� ������ �̷��� ���ɼ��� ���̱� ���� ������ �����Ѵ�. 0���� �����ϴ� ISN�� �̾����� Seq�� ���� �����ϰ� ����� ���ݿ� ���������