# js 오류 목록

## error handling

- 일반적으로 에러가 생겼을 경우
```
const updateReview = async (req, res) => {
  try {
    const { productId } = req.params
    const { review, reviewsId, } = req.body;
    const { user_id } = res.locals;
    const thisReview = await Reviews.findByPk(reviewsId);

    await thisReview.update({ review: review });
    res.send({ result: true, msg: "댓글이 수정되었습니다" });
  } catch (error) {
    res.status(400).send({ result: false, "오류 발생" });
  }
};
```  
- throw를 사용하여 에러 메세지를 상황에 따라 커스텀
```  
const updateReview = async (req, res) => {
  try {
    const { productId } = req.params
    const { review, reviewsId, } = req.body;
    const { user_id } = res.locals;
    const thisReview = await Reviews.findByPk(reviewsId);

		 if (thisReview.productId !== productId || thisReview.user_id !== user_id)
      throw new Error("서버 검증 오류");
    }
    await thisReview.update({ review: review })
			.then(() => {
        return res.send({ result: true, msg: "댓글이 수정되었습니다" });
      })
      .catch((err) => {
        if (err) throw new Error("db수정 실패, 개발팀에 문의해주세요");
      });
  } catch (error) {
    res.status(400).send({ result: false, msg : error.message });
  }
};
```  
그러나 예상 외로 이 경우에 db에러가 try catch오류로 전송되지 않았다.   

그 이유는 콜백 내에서 오류를 던지면 작동하지 않는다고 한다.  

[https://stackoverflow.com/questions/27794750/node-js-with-express-throw-error-vs-nexterror](https://stackoverflow.com/questions/27794750/node-js-with-express-throw-error-vs-nexterror)  
- next(err)를 이용하여 에러를 보내는 상태  
[https://yohanpro.com/posts/nodejs/error-handling](https://yohanpro.com/posts/nodejs/error-handling)  
next와 미들웨어를 이용하여 콜백 내의 에러도 제어해준다.  

```
const updateReview = async (req, res) => {
  try {
    const { productId } = req.params
    const { review, reviewsId, } = req.body;
    const { user_id } = res.locals;
    const thisReview = await Reviews.findByPk(reviewsId);

		 if (thisReview.productId !== productId || thisReview.user_id !== user_id)
      throw new Error("서버 검증 오류");
    }
    await thisReview.update({ review: review })
			.then(() => {
        return res.send({ result: true, msg: "댓글이 수정되었습니다" });
      })
      .catch((err) => {
        if (err) next(new Error("db수정 실패, 개발팀에 문의해주세요"));
      });
  } catch (error) {
    return next(new Error(error.message));
  }
};
```  
전체 에러를 컨트롤해주는 미들웨어도 만든다  
```
const errorHandler = (err, req, res, next) => {
  console.error(err.stack);
  res.status(err.status || 500).send({ result: false, msg: `code ${err.status || 500}: ${err.message}` });
}
```
대부분의 에러를 커스텀할 수 있게 되었지만 상태코드가 마음에 들지 않았다.  
### 최종 해결
- http-errors의  createError함수 사용
```
var createError = require('http-errors');

const myError = (status, message) => {
  return createError(status, message);
}

module.exports = myError;
```
```
const updateReview = async (req, res) => {
  try {
    const { productId } = req.params
    const { review, reviewsId, } = req.body;
    const { user_id } = res.locals;
    const thisReview = await Reviews.findByPk(reviewsId);

		 if (thisReview.productId !== productId || thisReview.user_id !== user_id)
      throw new Error("서버 검증 오류");
    }
    await thisReview.update({ review: review })
			.then(() => {
        return res.send({ result: true, msg: "댓글이 수정되었습니다" });
      })
      .catch((err) => {
        if (err) next(myError(500, "db수정 실패, 개발팀에 문의해주세요"));
      });
  } catch (error) {
    return next(myError(400, err.message));
  }
};
```
대부분의 에러 메세지와 상태 코드를 커스텀할 수 있게 되었다  


## ERROR 2003 (HY000): Can't connect to MySQL server on 'localhost' (10061)
### 해결
https://hoon93.tistory.com/9

## sequelize seed 생성시 외래키 적용 오류
npx sequelize-cli db:seed:all 로 seed 생성시  
ERROR: Cannot add or update a child row: a foreign key constraint fails  
오류가 발생  
액션의 외래키가 routineId인데 이게 1, 2로 고정값으로 해놓았었는데 routine이 전체 삭제를 하더라도 mysql을 끄지 않는 한?(확인되지 않음) 다시 1부터 시작되지 않아 생기는 문제    

### 해결
[https://stackoverflow.com/questions/48732223/sequelize-seed-with-associations](https://stackoverflow.com/questions/48732223/sequelize-seed-with-associations)  
그래도 sequelize가 인간적으로 seed 생성시 부모부터 생성하긴 하는 것 같아  
안쪽에 부모의 id를 찾는 쿼리를 생성해 해결  
```
up: async (queryInterface, Sequelize) => {

    //  Add seed commands here.
    //  Example:

    const routines = await queryInterface.sequelize.query(
      `SELECT id from Routines;`
    );
    const routineRows = routines[0];
		await queryInterface.bulkInsert('actions', [
      {
        ...,
        routineId: routineRows[0].id,
				...
      },]);
		}
```

