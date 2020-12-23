하이버네이트 방언 설정
===================

### 각 방언 후속 버전은 이전 방언 버전의 설정을 상속한다. 따라서 MariaDB의 상속 계층은 다음과 같다.
```
> MariaDB103Dialect 
>   > MariaDB102Dialect 
>   >   > MariaDB10Dialect 
>   >   >   > MariaDB53Dialect 
>   >   >   > MariaDBDialect 
>   >   >   >   > MySQL5Dialect 
>   >   >   >   >   > MySQLDialect 
>   >   >   >   >   >   > Dialect
```
***
### 버전별 방언
* MariaDB102Dialect for   : MariaDB server 10.2
* MariaDB103Dialect for   : MariaDB server 10.3 이상은 시퀀스 지원을 제공합니다.
* MariaDB10Dialect for    : MariaDB server 10.0 및 10.1 용 
* MariaDB53Dialect for    : MariaDB server 5.3 및 이후 5.x 버전.
* MariaDBDialect for      : MariaDB server 5.1 및 5.2.
