# ec2 서버 mysql 연동

## mysql 설치
```
//nodejs 설치 > node -v 로 버전나오면 설치된 것
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -

//npm 설치 > npm -v 로 버전나오면 설치된 것
sudo apt-get install -y nodejs

//ec2에 node_modules 생략하고 파일 올린 후 인스톨!
npm install
```

## mySQL 세팅

### ubuntu > 해당 프로젝트 디렉토리에서 작업
```
sudo apt update //패키지 정보 업데이트
sudo apt install mysql-server //mysql설치. y/n 나오면 y
dpkg -l | grep mysql-server //설치확인 (mysql-server가 리스트에 나오는지)

//--외부 접속 허용 (안하면 세팅 다해도 로컬에서 원격 db계정접속 불가)--
cd /etc/mysql/mysql.conf.d //해당 디렉토리로 이동
sudo vi mysqld.cnf //mysqld.cnf 파일 실행 i 누르면 편집모드. 돌아갈 땐 esc 나갈 땐 :wq
[ => bind-address 항목 수정 ( 127.0.0.1 -> 0.0.0.0 ) ]

//--DB 내 한글 사용을 위한 인코딩 설정 변경--
cd /etc/mysql //해당 디렉토로 이동
sudo vi my.cnf //my.cnf 파일 실행 i 누르면 편집모드.

//[내용 추가 - "!includedir" 아래부분 부터]
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mysql.conf.d/

#[mysqld]
#collation-server = utf8_general_ci
#character-set-server = utf8
#skip-character-set-client-handshake

[client]
default-character-set = utf8

[mysqld] 
character-set-client-handshake=FALSE 
init_connect="SET collation_connection = utf8_general_ci"
init_connect="SET NAMES utf8" 
character-set-server = utf8 
collation-server = utf8_general_ci 
lower_case_table_names = 1
max_allowed_packet = 1024M

[mysqldump] 
default-character-set = utf8

[mysql] 
default-character-set = utf8

//[내용 끝]
```

### ubuntu > 해당 프로젝트 디렉토리 > mysql 실행 후 작업
```
//아래 코드들은 우선 실행하고 mysql 내에서 작업
//SQL 예약어는 대문자로 쓰는것이 관례

$ sudo systemctl start mysql //mysql 서버 실행

$ sudo systemctl enable mysql //우분투 재실행되는 경우 또는 sql종료돼도 재실행(직접스탑한 경우 제외)

sudo mysql //mysql 터미널 키워드 실행 (관리권한 실행)

//--mysql 외부 접속 계정 생성 및 권한설정--
//계정이름@ 이후 %를 입력하면 전제 ip에 대해 접근가능한 계정.
//localhost 또는 특정 ip입력하면 해당 ip에서만 접속가능 (ec2올려두고 사용하므로 % 사용)
CREATE user [계정이름]@'%' identified by [패스워드]; //계정 생성

//--권한부여 1 (모든 db에 대해 권한 부여)--
GRANT ALL PRIVILEGES ON *.* to '계정이름'@'%' with grant option; //모든 권한 부여

//--권한부여 2 (특정 db에 대한 권한 부여)--
GRANT ALL PRIVILEGES ON 데이터베이스이름.* to 생성한계정@localhost;

//--부여된 권한 조회--
SHOW GRANTS FOR '계정이름'@'localhost';


//user테이블(mysql 계정테이블)에 계정을 추가하거나 변경사항이 있을 경우 flush privileges 쿼리를 실행
// => ! 계정 추가 또는 계정의 권한을 변경했다면 한 번씩 실행해주면 됨
FLUSH PRIVILEGES;

//user 정보 확인
SELECT User, Host, authentication_string FROM mysql.user;

//--사용자 계정 삭제--
DROP USER [user명]@[server명];
ex) DROP USER root@localhost;

//--mysql db생성 ( 생성  후 sequelize migrate 실행해도 됨 )-- 
CREATE DATABASE [데이터베이스이름];

//--mysql db제거-- 
DROP DATABASE [데이터베이스이름];

//--mysql db리스트 출력-
SHOW DATABASES;


//--종료 후 mysql 계정  접속--
mysql -u 계정 -p 패스워드 // [패스워드]생략 시 엔터치면 입력하라고 나오는데 그 때 입력해도됨
```
  
### ++ Ubuntu에서 mysql의 root계정 로그인이 안되는 경우 해결방법 !
ubuntu같은 일부 리눅스 시스템에서 mysql을 설치하고  
$ mysql -u root -p 으로 로그인 시도를하면   
'ERROR 1698 (28000): Access denied for user 'root'@'localhost'이라는 에러를 발생할때가 있다.  

이는 기본적으로 초기설정되어있는 mysql의 root 계정의 패스워드 타입때문인데 
이 타입을 변경해주면된다.  
```
$ sudo mysql -u root # sudo를 사용하여 root계정으로 mysql에 접속한다. 

mysql> USE mysql;
mysql> SELECT User, Host, plugin FROM mysql.user;

+------------------+-----------------------+
| User             | plugin                |
+------------------+-----------------------+
| root             | auth_socket           |
| mysql.sys        | mysql_native_password |
| debian-sys-maint | mysql_native_password |
+------------------+-----------------------+
```  

위처럼 root의 plugin이 auth_socket으로 설정되어있는것을 확인할 수 있다.  
이 값을 mysql_native_password로 변경해주면 일반적인 로그인이 가능하다.  

```
mysql> update user set plugin='mysql_native_password' where user='root';
mysql> flush privileges;
mysql> select user, host, plugin from user;

+------------------+-----------------------+
| User             | plugin                |
+------------------+-----------------------+
| root             | mysql_native_password |
| mysql.sys        | mysql_native_password |
| debian-sys-maint | mysql_native_password |
+------------------+-----------------------+
mysql> exit;
Bye
```
> 출처:   
> https://aboutcoding.tistory.com/entry/AWS-EC2%EC%97%90-MySQL-%EC%84%B8%ED%8C%85%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-%EA%B8%B0%EB%A1%9D  
> https://oziguyo.tistory.com/36