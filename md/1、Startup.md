

Aplication�г�ʼ����������������ң�Ӱ�쿪���ٶȡ�

���ܣ��������ڼ���App�����ٶȵ�һ���⡣���Խ��������ڳ�ʼ����ContentProvider�ϲ���һ�����Ӷ�ʹApp�������ٶȱ�ø��졣

ʹ��ContextProviderԭ��������ʾ�ص��ó�ʼ���ӿڣ����ǿ����Զ����ó�ʼ���ӿڣ����ְ취���ǽ���ContentProvider��

ԭ��ContentProvider onCreate����ִ���� Application onCreate֮ǰ�����̿���ʱ�Զ����á�


ʹ��ContextProvider�׶ˣ�һ���յ�ContentProvider��Լ��ռ��2ms�ĺ�ʱ������ContentProvider�����ӣ���ʱҲ�����һ�����ӡ�


��������˳��

Application#attachBaseContext->ContentProvider#onCreate->Application#onCreate



�����⣺   

     // jetPack Component
    implementation "androidx.startup:startup-runtime:1.0.0" // startup


�ο���https://blog.csdn.net/guolin_blog/article/details/108026357