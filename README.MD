## �������� ������� � ����� 4. GOF: �������� �������������� � .Net ����������:

�������������� ��� ������� � ������� ����, ��������� ������ � ��������.

---
## �������:

��� ������� ������  ��� ������� ������� ��� ������� � ��������� ����� Server �  ����������� ������������ �������� Singleton.
����������� ������� Sinleton ���������� �  ������ Server ��������� �������:

1. ��������� ��������� ����������� ����������-��������� ������ ������ instance (���. 10);
```
private static Server instance;
```
2. �������� ��������� ������ lockObject (���. 11), ������� ����� �������������� ��� ���������� ������� ����, �������������� �� �������� ���������� instance;
```
private static readonly object lockObject = new object();
```
3. �������� ��������� ����������� ������ (���. 17). ��� ��� ����������� ���������, ����� �� ������ ������� ��� ���������.
```
private Server() { }
```
4. ��������� ��������� �������� Instance (���. 19 - 36), ����� ������� ����� ��������� ������ � ���������� ������ Server. ���� ��������� �� ����������, �� �� ����� ������.
```
public static Server Instance
{
       get
       {
           if (instance == null)
           {
               lock (lockObject)
               {
                   if (instance == null)
                   {
                       instance = new Server();
                   }
               }
           }
            return instance;
       }
}
```
5. � ������ StartServer() ���������� ����� ���� ������ �������(���.38).
6. ������ ������� ���������� �� ������ Main()  (���. 67)
```
await Task.Run(() => Server.Instance.StartServer());
```

����� ������� ��� ���������� ����������� ������� Singleton.
