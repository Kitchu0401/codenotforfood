# Mongodb 명령어 정리

## database 관련
```
show dbs
use database_name
db.dropDatabase() // database 선택되어있어야 함
```

## collection 관련
```
show collections
db.createCollection(name, [options])
db.collection_name.drop()
```

## document 관련
```
db.collection_name.find(criteria, [projection])
db.collection_name.update(criteria, value, [options])
db.collection_name.remove(criteria, [justOne])
```

## document.find(): query parameter
```
// 비교 연산자
$eq     // equals
$ne     // not equals
$gt     // greater than
$gte    // greater than equals
$lt     // less than
$lte    // less then equals
$in     // in arrays
$nin    // not in arrays

// 논리 연산자
$or
$and
$not
$nor

// 정규표현식 연산자
$regex      // /pattern/
$options    // <options>
- i, m, x, s

// 자바스크립트 연산자
$where      // this로 document 접근 가능

// subdocument quering 연산자
$elemMatch
```

## document.find(): projection parameter
조회된 document 중 후처리로 전달할 filtering condition을 적용
```
$slice      // limit
$elemMatch  // subdocument filtering
```

## document.find(): 후처리 연산자 sort()
조회된 document를 전달하기 전 정렬
```
db.collection_name.find(query, [projection]).sort({ 'value': 1 })   // 오름차순 정렬
db.collection_name.find(query, [projection]).sort({ 'value': 1 })   // 내림차순 정렬
```

## document.find(): 후처리 연산자 limit()
조회된 document를 전달하기 전 숫자 제한
```
// 조회된 document 중 3건만 보여줌
db.collection_name.find(query, [projection]).limit(3)
```

## document.find(): 후처리 연산자 skip()
조회된 document를 전달하기 전 지정된 숫자만큼의 document를 건너뛴다
```
// 조회된 document 중 2건 이후 건들부터 보여줌
db.collection_name.find(query, [projection]).skip(2)
```

## document.update(): value 연산자
```
$set            // field update
$upset          // field remove
$push           // add subdocument element
$each           // add multiple subdocument element
$sort           // add multiple subdocument element with sorting
$pull           // remove subdocument element ()
$pull + $in     // remove multiple subdocument element with matching condition
```

## document.update(): options
```
upsert  // true일 경우, match된 document가 존재할 경우 update, 존재하지 않을 경우 insert
```