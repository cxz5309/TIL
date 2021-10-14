# Sequelize

> MYSQL을 노드에서 쓰려고 한다.  
> 즉 알아야 한다.

- Nodejs에서 mysql을 다루는 orm이다.
- 몽고디비와 다르게 관계형이니까 orm이다.

## 매우 편리한 이니셜라이즈
```
$ npm i sequelize mysql2
$ npm i -g sequelize-cli
$ npx sequelize init
```
- 필요한 파일과 폴더들이 알아서 설치된다.
- 근데 -g는 안붙여도 될 것 같은데 왜 붙였을까
> - 찾아보니 역시 필요없었다. 오히려 -D를 붙여야 한다. + npx

sequelize init을 하게 되면 새 폴더와 파일들이 생성된다.

(프로젝트에 실시간 적용중..)
- config : sequelize를 사용하기 위해 환경을 설정하는 부분이다.
- models/index.js : Model을 정의하고 관계를 설정하는 부분이다.

## models/index.js
- index.js파일이 생겨났다.
- 각각 기능을 알아보자
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
갓-orm은 역시 쉽게 db를 생성해준다.

##  