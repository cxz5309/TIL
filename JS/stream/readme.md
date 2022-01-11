# stream 
- 스트림 가능한 소스(file, network input 등) 로부터 데이터를 작은 청크로 쪼개서 처리할 수 있게 한다.
- 큰 데이터를 처리해야 하거나, 비동기적으로만 얻을 수 있는 데이터를 처리할 때 유용
- 5기가의 파일을 처리할때 램에 한꺼번에 5기가를 올리지 않고 처리한다.
- 비동기 처리를 할 때에도 사용된다. (stack이 순서대로 진행하기 때문에 잘라주어야 함)

## readable
스트림에 입력 가능  
fs.createReadStream  
process.stdin  
서버입장의 http요청  
클라이언트 입장의 http 응답  

## writable
스트림에 출력가능  
fs.createWriteStream  
process.stdout  
클라이언트 입자의 http요청  
서버 입장의 http응답  


## duplex
양방향 스트림  
tcp sockets  
zlib streams(압축)  
crypto streams(암호화)  

## fransform
입력 스트림을 새로운 스트림으로 변환  
zlib streams  
crypto streams  

## JSON 스트림 처리기 예시
```js
const fs = require('fs');

//데이터를 읽는다.
const rs = fs.createReadStream('local/jsons', {
    encoding: 'utf-8',//파일스트림을 다른 문자로 인코딩해준다.
    highWaterMark: 6,//청크를 나누어주는 기준이다. 기본적으로 65536이며 늘어날수록 청크의 개수가 줄어든다(처리시간은 줄지만 읽는동안 사용되는 ram의 용량 증가)
});

let totalSum = 0;
let accuJsonStr = '';

// 데이터 하나를 처리하는 동안 콜백 함수를 실행한다.
rs.on('data', (chunk)=>{
    //분할되어 현재 읽는중인 데이터는 chunk라고 부른다.
    if(typeof data !== 'string'){
        return
    }

    accuJsonStr += chunk
    
    //청크의 마지막 endLine 이후 text만 남겨 다음 청크에 붙인다.
    const lastNewLineIdx = accuJsonStr.lastIndexOf('\n');
    accuJsonStr = accuJsonStr.subString(lastNewLineIdx);
    //이전 text는 count처리한다.
    totlaSum += lastNewLineIdx
    .split('\n')
    .map((jsonLine)=>{
        try{
            return JSON.parse(jsonLine);
        }catch{
            return undefined
        }
    .filter((json)=>json)
    .map((json)=>json.data)
    .reduce((sum, curr)=>sum + curr, 0);
    })
})

// 데이터를 전부 처리한 이후 콜백 함수를 실행한다.
rs.on('end', ()=>{
    console.log('Event: end')
    console.log('totalSum', totalSum)
})
```