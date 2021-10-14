# Sequelize

> 이번 프로젝트에서 MYSQL을 노드에서 쓰려고 한다...  
> = 알아야 한다.

- Nodejs에서 mysql을 다루는 orm이다.
- mongoose와 다르게 관계형이니까 orm이다.

## 매우 편리한 이니셜라이즈
```
$ npm i sequelize mysql2
$ npm i -g sequelize-cli
$ npx sequelize init
```
- 필요한 파일과 폴더들이 알아서 설치된다.
- 근데 -g는 안붙여도 될 것 같은데 왜 붙였을까
> - 찾아보니 역시 필요없었다. 오히려 -D를 붙이는게 (개인적으로) 낫다.  


sequelize init을 하게 되면 새 폴더와 파일들이 생성된다.  
![image1](/public/JS/sequelize1_1.png)  
(프로젝트에 실시간 적용중..)
- config : sequelize를 사용하기 위해 환경을 설정하는 부분이다.
- models/index.js : Model을 정의하고 관계를 설정하는 부분이다.

## models/index.js
> index.js파일이 생겨났다.
> 각각 기능을 알아보자
```
'use strict';

const fs = require('fs');
const path = require('path');
const Sequelize = require('sequelize');
const basename = path.basename(__filename);
// 환경변수, 실제 배포할 때는 'production'으로 바꿔야한다.
const env = process.env.NODE_ENV || 'development';
const config = require(__dirname + '/../config/config.json')[env];
// db 객체 생성
const db = {};

let sequelize;
//환경변수에 따라 다르게 작용한다.
if (config.use_env_variable) {
  sequelize = new Sequelize(process.env[config.use_env_variable], config);
} else {
  sequelize = new Sequelize(config.database, config.username, config.password, config);
}

fs
  .readdirSync(__dirname)
  .filter(file => {
    return (file.indexOf('.') !== 0) && (file !== basename) && (file.slice(-3) === '.js');
  })
  .forEach(file => {
    const model = require(path.join(__dirname, file))(sequelize, Sequelize.DataTypes);
    db[model.name] = model;
  });

Object.keys(db).forEach(modelName => {
  if (db[modelName].associate) {
    db[modelName].associate(db);
  }
});

//시퀄라이즈 객체에 config 파일에 있는 설정들을 넣어준다.
db.sequelize = sequelize;
db.Sequelize = Sequelize;

//db 객체에 시퀄라이즈 패키지와 객체를 넣고 모듈로 사용한다.
module.exports = db;
```

## config.json
```
{
  "development": {
    "username": "root",
    "password": null,
    "database": "database_development",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "test": {
    "username": "root",
    "password": null,
    "database": "database_test",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "production": {
    "username": "root",
    "password": null,
    "database": "database_production",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }
}
```
역시 환경변수에 따라 다르게 작동한다.

## 데이터베이스 생성하기
```
npx sequelize db:create
```
- 인터넷에서 본 대로 데이터베이스를 생성해보았다.
```
TypeError [ERR_INVALID_ARG_TYPE]: The "data" argument must be of type string or an instance of Buffer, TypedArray, or DataView. Received type number (1234)
```
오우!😂  
</br>
대충..찾아보니..config.json에서 뭔가를 잘못했다고 한다.  
https://stackoverflow.com/questions/47049399/sequelize-dbmigrate-throw-typeerror-data-must-be-a-string-or-a-buffer  

이쪽이 문제였다.  
```
"password": 1234,
```  
->  
```
"password": "1234",
```  
솔직히 영어 해석 제대로 못했는데 감으로 때려맞췄다.  

해결  

</br>

인줄알았으나..
```
ERROR: Access denied for user 'root'@'localhost' (using password: YES)
```
오우!😂😂  
</br>
내 mysql을 직접 들어가보았다.  
![image4](/public/JS/sequelize4.PNG)   
아 옛날에 비밀번호 바꿔놨구나  

```
"password": "내비밀번호",
```  

진짜 해결!  
![image2](/public/JS/sequelize2.PNG)     
![image3](/public/JS/sequelize3.PNG)     

orm을 사용하여 ~~쉽게?~~ db를 생성하였다.  

## sequelize-cli을 이용하여 모델만들기
> 인터넷에서 많이 찾아봤는데 기껏 sequelize-cli 설치해놓고 명령어로 모델 생성은 잘 안하더란다.  
> 그래서 난 이걸로 해야겠다  

https://sequelize.org/master/manual/migrations.html  

https://velog.io/@jeff0720/Sequelize-CLI%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EA%B0%84%EB%8B%A8%ED%95%9C-User-API-%EB%A7%8C%EB%93%A4%EA%B8%B0-vdjpb8nl0k  
```
We will use model:generate command. This command requires two options:

name: the name of the model;
attributes: the list of model attributes.
Let's create a model named User.

npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string
```   
.......  
do it!  
```
$ npx sequelize model:generate --name Comment --attributes commentId:string,postId:string,userId:string,contents:string,date:date
```  
date의 데이터타입을 찾아보기 위해 조금 더 찾아보았다.  
mysql의 DATETIME은 DATE로 통용해서 쓰는 것 같다.  
https://sequelize.org/v5/manual/data-types.html  
https://stackoverflow.com/questions/29652538/sequelize-js-timestamp-not-datetime   


### 모델 생성!
- models/comment.js

```
'use strict';
const {
  Model
} = require('sequelize');
module.exports = (sequelize, DataTypes) => {
  class Comment extends Model {
    /**
     * Helper method for defining associations.
     * This method is not a part of Sequelize lifecycle.
     * The `models/index` file will call this method automatically.
     */
    static associate(models) {
      // define association here
    }
  };
  Comment.init({
    commentId: DataTypes.STRING,
    postId: DataTypes.STRING,
    userId: DataTypes.STRING,
    contents: DataTypes.STRING,
    date: DataTypes.DATE
  }, {
    sequelize,
    modelName: 'Comment',
  });
  return Comment;
};
```   
- migrations/생성날짜-create-comment.js
```
'use strict';
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('Comments', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      commentId: {
        type: Sequelize.STRING
      },
      postId: {
        type: Sequelize.STRING
      },
      userId: {
        type: Sequelize.STRING
      },
      contents: {
        type: Sequelize.STRING
      },
      date: {
        type: Sequelize.DATE
      },
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE
      },
      updatedAt: {
        allowNull: false,
        type: Sequelize.DATE
      }
    });
  },
  down: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('Comments');
  }
};
```
GOOD!👍  

### 모델 수정
- 아 근데 sequelize에서도 mongoose처럼 자동으로 id를 만들어준다고 한다. 게다가 이건 createdAt이랑 updatedAt까지 자동으로 생성해준다!
> (괜히 userid랑 date만들었다)
- 쓸데없이 만든 userid랑 date는 만들고 난 이후에 수정해도 migrate만 안하면 상관없는 것 같아서 수정했다.
## 테이블 생성하기
- sequelize는 만들어낸 모델로 실제 테이블도 직접 생성해준다!
```
npx sequelize db:migrate
```
```
Sequelize CLI [Node: 14.15.1, CLI: 6.2.0, ORM: 6.7.0]

Loaded configuration file "config\config.json".      
Using environment "development".
== 20211014155413-create-comment: migrating =======
== 20211014155413-create-comment: migrated (0.271s)
```
![image5](/public/JS/sequelize5.PNG)  
GOOD!!!!👍👍👍

## db사용하기
- 원래 mongoose로 구현되어 있었기에 공식문서(https://sequelize.org/master/manual/model-querying-finders.html) 를 보고 바꿔주기만 하면 된다.


</br>

암튼 여차저차해서

```
await Comment.create({
  postId: postId,
  contents: contents,
  userId: userId,
});
```
```
Executing (default): INSERT INTO `Comments` (`commentId`,`postId`,`userId`,`contents`,`createdAt`,`updatedAt`) VALUES (?,?,?,?,?,?);
```
![image6](/public/JS/sequelize6.PNG)  

성공🎉  