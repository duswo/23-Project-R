# 👩 **2377112 이연재**
## 📓 R 언어
## 📅 230504
> 선그래프
- 연도별 증감 추이와 같은 데이터 표현
- 시간 순서에 따른 데이터를 시각화할 때 사용
```R
month = 1:12 # 월 데이터 입력
late = c(5,8,7,9,4,6,12,13,8,6,6,4) # 각 월마다 지각생 수
plot(month, # x 데이터 입력하기
     late, # y 데이터 입력하기
     main="Late students", # 메인 이름
     type= "l", # 그래프의 종류 정하기
     lty=1, # 선의 종류 정하기
     lwd=1, # 선의 굵기 정하기
     xlab="Month ", # x축 이름 정하기
     ylab="Late cnt" # y축 이름 정하기
)
```
> 복수 선그래프
```R
month = 1:12 # 월별 데이터 입력
late2 = c(5,8,7,9,4,6,12,13,8,6,6,4) # 각 월마다 1반 지각생 데이터
late1 = c(4,6,5,8,7,8,10,11,6,5,7,3) # 각 월마다 2반 지각생 데이터 입력
plot(month, # x 데이터
     late1, # y 데이터
     main="Late students", # 메인 제목 입력
     type= "b", # 그래프 초이스
     lty=1, # 선의 종류 초이스
     col="red", # 선의 색깔 초이스
     xlab="Month ", # x축 레이블 입력
     ylab="Late cnt" # y축 레이블 압력
)

lines(month,late2, # 선 별로 데이터 입력
     type = "b",  # 그래프 종류 입력
     col = "blue") # 색깔 입력
```
> 산점도
- 다변량 자료 : 다변량 자료는 두개 이상의 변수를 동시에 다루는 자료
- 일변량 자료는 vectcor, 다변량 자료는 matrix or data frame에 저장
- 각 변수는 데이터셋에서의 열로 표현됨

- mtcars 데이터셋에서 자동차 중량(wt)와 연비(mpg)의 상관관계의 산점도 (두 변수)
```R
wt <-mtcars$wt
mpg <- mtcars$mpg
plot(wt, mpg, # 2개 변수(x축,y축)
main="Car_Weight-mpg", # 제목
xlab="Car_Weight ", # x축 레이블
ylab="Miles_Per_Gallon ", # y축 레이블
col="red", # point 의 color
pch=19) # point 의 종류
```

- pairs()(여러 변수)
```R
vars <- c("mpg","disp","drat","wt") # 대상 변수를 선언
target <- mtcars[,vars] # target에 데이터 셋 입력
pairs(target, # 대상 데이터와 연결
main="Multi plots") # 메인 제목 입력
```

- 그룹 정보가 있는 2변량 데이터 분포
```R
iris.2 <- iris[,3:4] # 각 데이터 입력하기
point <- as.numeric(iris$Species) # 각각 포인트 모양 정하기
color <- c("red","green","blue") # 각각 포인트 컬러 정하기
plot(iris.2, # 데이터 입력
     main="Iris plot", # 제목 정하기     
     pch=c(point), # 각각 포인트 모양 입력
     col=color[point]) # 가각 포인트 컬러 입력
```
## 📅 230427
> 막대그래프
1. 막대그래프 작성
- 도수분포표 계산하기
```R
favorite <- c('WINTER', 'SUMMER', 'SPRING', 'SUMMER', 'SUMMER', 'FALL', 'FALL', 'SUMMER', 'SPRING', 'SPRING') # 데이터 입력
favorite #favorite의 내용 출력
table(favorite) #도수분포 계산
```
- 막대그래프 작성하기
```R
ds <- table(favorite) # 도수분포표 저장
ds # 도수분포표 내용 확인
barplot(ds, main='favorite season') # 막대그래프 작성
```
- 막대그래프의 색 지정
```R
barplot(ds, main='favorite season', col='blue')

>colors() # R그래프에 사용할 수 있는 색의 이름 조회
```
- 막대별로 색 다르게 지정
```R
barplot(ds, main='favorite season', col=c('blue', 'red', 'green', 'yellow'))
```
- x측, y측 설명 붙이기
```R
barplot(ds, main='favorite season', col='green', xlab='계절', ylab='빈도수')
```
- 팔레트에서 색 선택하여 사용
```R
barplot(ds, main='favorite season', col=rainbow(4))
```
- 그래프 막대 수평 방향으로 출력
```R
barplot(ds, main='favorite season', col='yellow', horiz=TRUE)
```
- x축의 그룹 이름 바꾸기
```R
barplot(ds, main='favorite season', col='yellow', names=c('FA', 'SP', 'SU', 'WI'))
```
- x축의 그룹 이름 수직 방향으로 출력
```R
barplot(ds, main='favorite season', col='green', las=2)
```
2. 중첩 그룹의 막대그래프
- 중첩 그룹 막대그래프 작성
```R
age.A <- c(13709, 10974, 7979, 5000, 4250)
age.B <- c(17540, 29701, 36209, 33947, 24487)
age.C <- c(991, 2195, 5366, 12980, 19007)

ds <- rbind(age.A, age.B, age.C)
colnames(ds) <- c('1970', '1990', '2010', '2030', '2050')
ds

barplot(ds, main='인구 추정')
```
-연령대별로 색 다르게 지정
```R
barplot(ds, main='인구 추정', col=c('green, 'blue', purple'))
```
3. 막대그래프에 범례 추가
```R
barplot(ds, main='인구 추정', col=c('green, 'blue', purple), beside=TRUE, legend.text=T)
```
- 막대그래프 밖에 범례 표시
```R
> par(mfrow=c(1, 1), mar=c(5, 5, 5, 7))
```
- par()함수는 그래프를 표시할 창에 대해 설정
- par()함수 매개변수
  - mfrow=c(1, 1) : c(1,1)은 창을 분할하지 않음 의미.
  - mar=c(5, 5, 5, 7) : 그래프 출력 창과 그래프 출력 영역 밖의 여유 고강 지정
    c(bottom, left, top, right)의 순서로 숫자 지정
 - 범례 그래프 밖에 표시
 ```R
 > par(mfrow=c(1, 1), mar=c(5, 5, 5, 7))
 > barplot(ds, main='인구 추정',
           col=c('green', 'blue', purple),
           beside=TRUE,
           legend.text=T,
           args.legend = list(x='topright', bty='n',
           inset=c(-0.25,0)))
 ```
 - args.legend 지정 사항
   - x='topright' : 범례를 출력할 기본 위치를 지정, 
                    'topright'는 그래프 출력 영역의 위쪽에서 오른쪽을 의미
   - bty='o' : 범례가 표시되는 영역에 테두리선을 표시할지의 여부 지정
               'o'는 테두리선 표시
               'n'은 테두리선 표시 X
   - inset=c(-0.25,0) : 범례를 x축과 y축 방향으로 얼마나 이동시킬지 지정
                        -1~1 사읭 값 지정(%의미)
- 범례 내용 바꾸기
```R
par(mfrow=c(1, 1), mar=c(5, 5, 5, 7)) # 그래프 윈도우 설정
barplot(ds, main='인구 추정',
           col=c('green', 'blue', purple),
           beside=TRUE,
           legend.text=c('0~14세', '15~64세', '65세 이상'),
           args.legend = list(x='topright', bty='n',
           inset=c(-0.25,0)))
par(mfrow=c(1, 1), mar=c(5, 5, 5, 7)+0.1) # 그래프창 설정 해제
```
## 📅 230414
> 파일 입출력
1. 실행 결과 파일로 출력
```R
> sink('result.txt', append=T) # 파일로 출력 시작
> cat('a+b=', a+b, '/n')
> sink() # 파일로 출력 정지
```
- 처리 결과를 파일로 출력하는 코드
- 프로그램 중간에 파일로 출력하고 싶은 부분에서 sink() 함수를 위아래 넣음
- sink( ) 함수 매개변수
  - 'result.txt' : 계산 결과를 출력할 파일 이름.
  - append=T :'result.txt'의 내용 맨 마지막에 덧붙여서 출력
               append=F이면 기존에 있던 내용을 지우고 새로 출력하는 것
```R
> cat('hello world \n') # 화면으로 출력
hello world
```
- cat('hello world \n')의 실행 결과가 다시 화면에 출력
```R
> sink('rewult.txt', append=T) # 파일로 출력 시작
> cat('a*b=', a*b, '\n')
> sink() # 파일로 출력 정지
```
- cat('a*b=', a*b, '\n')의 실행 결과는 화면에 보이지 않음
```R
> print('End work') # 화면으로 출력
[1] "End work"
``` 
- 실행 결과가 다시 화면에 출력
2. 탭이나 공백으로 분리된 파일 읽기
```R
setwd('C:/Rworks') # 작업 폴더 지정
air <- read.table('airquality.txt', header=T, set=' ') # 파일 읽기
head(air) # 내용 확인
```
```R
실행결과
> setwd('C:/Rworks') # 작업 폴더 지정
```
- 읽어올 파일이 있는 폴더를 지정
```R
> head(air) # 내용 확인
  Ozone  Solar.R   Wind  Temp  Month  Day
1    41      190    7.4    67      5    1
2    36      118    8.0    72      5    2
3    12      149   12.6    74      5    3
4    18      313   11.5    62      5    4  
5    NA       NA   14.3    56      5    5
6    28       NA   14.9    66      5    6
```
- 읽어온 파일 내용 확인
```R
> air <- read.table('airquality.txt', header=T, sep='  ') # 파일 읽기
```
- 파일을 읽어 데이터프레임 air에 저장
- read.table( ) 함수 매개변수
  - 'airquality.txt' : 읽어올 파일의 이름
  - header=T : 파일의 첫 줄(첫 번째 행)은 데이터 값이 아닌 열 이름
  - sep=' ' : 데이터에서 열과 열이 공백(' ')으로 분리되어 있음
> 조건문
1. if-else 문
```R
job.type <- 'A'
if (job.type == 'B') {
    bonus <- 200
} else {
    bonus <- 100
}
print(bonus)
```
```R
job.type <- 'A'
bonus <- 100
if (job.type == 'B') {
    bonus <- 200
}
print(bonus)
[1] 100
```
- if() 함수만으로도 조건문 성립 (else 없어도 됨)
```R
a <- 10
if (a<5) {
   print(a)
} else {
   print(a*10)
   print(a/10)
}
```
- {}는 프로그래밍에서 코드블록이 코드블록에 의해 묶인 명령문은 조건에 의해 모두 실행이 되든지, 모두 실행이 안 되는지 둘 중 하나
```R
a <- 10
b <- 20
if (a>5 & b>5) {
    print(a+b)
}
if (a>5 | b>30) {
    print(a*b)
}
```
- 조건문과 조건문 연결 시 논리연산자 사용
- & : 두 조건이 모두 만족 해야 참(True)
- | : 두 조건 중 어느 하나만 만족하면 참(True)
2. ifelse문
- 조건에 따라 선택할 값이 각각 하나씩일 때 사용
- ifelse(비교 조건, 조건이 참일 때 선택할 값, 조건이 거짓일 때 선택할 값)
```R
a <- 10
b <- 20
# if-else문
if (a>b) {
    c <- a
} else {
    c <- b
}
print(c)
# ifelse문
c <- ifelse(a>b, a, b)
print(c)
```
> 반복문
1. for문
- 반복 범위는 박복 변수에 할당할 값을 모다운 벡터, 이 벡터의 길이만큼 for문이 반복됨
- for문이 한 번씩 수행할 때마다 반복 범위의 값을 하나씩 가져와 반복 변수에 저장한 뒤 코드블록 안에 있는 명령문 실행
```R
for(반복 변수 in 반복 범위) {
      반복할 명령문(들)
  }
```
```R
> for(i in 1:9) {
+     cat('2 *', i, '=', 2*i, '\n')
+ }
2 * 1 = 2
2 * 2 = 4
...(생략)
2 * 8 = 16
2 * 9 = 18
```
- cat() 함수는 한 줄에 여러 개의 값을 결합하여 출력할 때 사용
```R
> for(i in 1:20) {
+     if(i%%2==0) {
+         cat(i, ' ')
+     }
+ }
2 4 6 8 10 12 14 16 18 20
```
```R
> sum <- 0
> for(i in 1 :100) {
+     sum <- sum + i
+ }
> print(sum)
[1] 5050
```
```R
norow <- nrow(iris) # iris의 행의 수
mylabel <- c() # 비어있는 벡터 선언
for(i in 1:norow) {
    if (iris$Petal.Length[i] <= 1.6) { # 꽃잎의 길이에 따라 레이블 결정
        mylabel[i] <- 'L'
    } else if (iris$Petal.Length[i] >= 5.1) {
        mylabel[i] <- 'H'
    } else {
        mylable[i] <- 'M'
    }
}
print(mylabel) # 레이블 출력
newds <- data.frame(iris$Petal.Length, mylabel) # 꽃잎 길이와 레이블 결합
head(newds) # 새로운 데이터셋 내용 출력
```
2. while문
```R
sum <- 0
i <- 1
while(i <= 100) {
    sum <- sum + i
    i <- i + 1
}
print(sum)
```
3. apply() 계열 함수
- 매트릭스나 데이터프레임에 있는 행, 열들을 하나하나 차례로 꺼내어 평균이나 합계 등을 구하는 작업 시 유용
- apply(데이터셋, 행/열 방향 지정, 적용 함수)
- 매개변수
  - 데이터셋 : 반복 작업을 적용할 대상인 매트릭스 or 데이터프레임 이름 
  - 행/열 방향 지정 : 행 방향 작업의 경우 1, 열 방향 작업의 경우 2 지정
  - 적용 함수 : 반복 작업의 내용을 알려주는 것으로, R 함수이거나 사용자 정의 함수 지정
 ```R
 apply(iris[,1:4], 1, mean)
 iris 데이터셋에서 4개의 열에 대해 행 방향으로 진행하면서 각 행의 평균(mean)을 계산하여 출력
 apply(iris[,1:4], 2, mean) # 열 방향으로 함수 적용
 iris 데이터셋에서 4개의 행에 대해 열 방향으로 진행하면서 각 행의 평균(mean)을 계산하여 출력
 ```
 > 사용자 정의 함수
 
 사용자가 스스로 만드는 함수
 ```R
 함수명 <- function(매개변수 목록) {
     실행할 명령문(들)
     return(함수의 실행 결과)
 }
 ```
 - 매개변수
   - 함수명 : 사용자 정의 함수의 이름으로 사용자가 만들 수 있음
   - 매개변수 목록 : 함수에 입력할 매개변수 이름을 지정
   - 실행할 명령문(들) : 함수에서 처리하고 싶은 내용 작성
   - 함수의 실행 결과 : 함수의 실행 결과를 반환, 반환 결과가 없으면 return() 함수 생략
 ```R
 mymax <- function(x,y) {
     num.max <- x
     if (y>x) {
         num.max <- y
     }
     return(num.max)
 }
 ```
 ```R
 > mymax(10,15)
 [1] 15
 > a <- mymax(20,15)
 > b <- mymax(31,45)
 > print(a+b)
 [1] 65
 ```
 1. 매개변수에 기본값 설정
 ```R
> mydiv <- function(x,y=2) {
+   result <- x/y
+   return(result)
+ }
> mydiv(x=10,y=3) # 매개변수 이름과 매개변수값을 쌍으로 입력
[1] 3.333333
> mydiv(10,3) # 매개변수값만 입력
[1] 3.333333
> mydiv(10) # x에 대한 값만 입력(y값 생략)
[1] 5
```
2. 여러 개 값 반환
```R
myfunc <- function(x,y) {
   val.sum <- x+y
   val.mul <- x*y
   return(list(sum=val.sum, mul=val.mul))
}
result <- myfunc(5,8)
s <- result$sum
m <- result$mul
cat('5+8 =', s, '\n')
cat('5*8 =', m, '\n')
```
3. 사용자 정의 함수의 저장과 재실행
함수 작성 -> 함수 실행하여 R에 함수 등록 -> 필요한 곳에서 함수 호출
```R
mydiv <- function(x,y=2) {
    result <- x/y
    return(result)
}
```
```R
setwd('c:/Rworks') # myfunc.R이 저장된 폴더
source('myfunc.R') # myfunc.R 안에 있는 함수 실행
a <- mydiv(20,4)   # 함수 호출
b <- mydiv(30,4)   # 함수 호출
a+b
mydiv(mydiv(20,2),5) # 함수 호출
```
4. 조건에 맞는 데이터 위치 찾기
```R
score <- c(76, 84, 69, 50, 95, 60, 82, 71, 88, 84)
which(score==69) # 성적이 69인 학생은 몇 번째?
shich(score>=85) # 성적이 85 이상인 학생은 몇 번째?
max(score) # 최고 점수는 몇 점?
which.max(score) # 최고 점수는 몇 번째?
min(score) # 최저 점수는 몇 점?
which.min(score) # 최저 점수는 몇 번째?
```
```R
score <- c(76, 84, 69, 50, 95, 60, 82, 71, 88, 84)
idx <- which(score<=60) # 성적이 50 이하인 값들의 인덱스
score[idx] <- 61 # 성적이 60 이하인 값들은 61점으로 성적 상향조정
score # 상향조정된 성적 확인

idx <- which(score>=80) # 성적이 80 이상인 값들의 인덱스
score.high <- score[idx] # 성적이 80 이상인 값들만 추출하여 저장
score.high # score.high의 내용 확인
```
## 📅 230406
6. iris 데이터셋
 - iris는 150그루의 붓꽃에 대해 4개 분야의 측정 데이터와 품종 정보를 결합하여 만든 데이터셋
 ```R
 > iris
    Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
 1           5.1         3.5          1.4         0.2    setosa
 2           4.9         3.0          1.4         0.2    setosa
 3           4.7         3.2          1.3         0.2    setosa
 ...(생략)
 150         5.9         3.0          5.1         1.8  virginica
 ```
 ```R
 iris[,c(1:2)] # 1~2열의 모든 데이터
 iris[,c(1,3,5)] # 1, 3, 5열의 모든 데이터
 iris[,c("Sepal.Length","Species")] # 1, 5열의 모든 데이터
 iris[1:5,] # 1~5행의 모든 데이터
 iris[1:5,c(1,3)] # 1~5행의 데이터 중 1, 3열의 데이터
 ```
 - 데이터셋의 기본 정보
 ```R
 dim(iris) # 행과 열의 개수 보이기
 nrow(iris) # 행의 개수 보이기
 ncol(iris) # 열의 개수 보이기
 colnames(iris) # 열 이름 보이기, names() 함수와 결과 동일
 head(iris) # 데이터셋의 앞부분 일부 보기
 tail(iris) # 데이터셋의 뒷부분 일부 보기
 ```
 ```R
 str(iris) # 데이터셋 요약 정보 보기
 iris[,5] # 품종 데이터 보기
 levels(iris[,5]) # 품종의 종류 보기(중복 제거)
 table(iris[,"Species"]) # 품종의 종류별 행의 개수 세기
 ```
 - 행별, 열별로 합계와 평균 계산
 ```R
 colSums(iris[,-5]) # 열별 합계
 colMeans(iris[,-5]) # 열별 평균
 rowSums(iris[,-5]) # 행별 합계
 rowMeans(iris[,-5]) # 행별 평균
 ```
 ```R
 > colSums(iris[,-5])                   # 열별 합계
 Sepal.Length Sepal.Width Petal.Length Petal.Width
        876.5       458.6        563.7       179.9
 > colMeans(iris[,-5])                  # 열별 평균
 Sepal.Length Sepal.Width Petal.Length Petal.Width
     5.843333    3.057333     3.758000    1.199333
 > rowSums(iris[,-5])
   [1] 10.2 9.5  9.4  9.4 10.2 11.4  9.7 10.1  8.9  9.6 10.8 10.0
  [13]  9.3 8.5 11.2 12.0 11.0 10.3 11.5 10.7 10.7 10.7  6.4 10.6
  ...(생략)
 [133] 17.0 15.7 15.7 19.1 17.7 16.8 15.6 17.5 17.8 17.4 15.5 18.2
 [145] 18.2 17.2 15.7 16.7 17.3 15.8
 ```
 - 조건에 맞는 행과 열 값 추출
 ```R
 IR.1 <- subset(iris, Species=='setosa')
 IR.1
 IR.2 <- subset(iris, Sepal.Length>5.0 &
                       Sepal.Width>4.0)
 IR.2
 IR.2[, c(2,4)]    # 2열과 4열의 값만 추출
 ```
 - subset() 함수 매개변수
   - iris : 데이터를 추출하는 대상이 iris 데이터셋
   - Species=='setosa' : 데이터를 추출할 조건을 지정하는 부분, 
                        품종 열의 값이 'setosa'인 행만 추출하라는 의미.
- 산술연산 적용
```R
> a <- matrix(1:20,4,5)
> a
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20
> a <- a*3
     [,1] [,2] [,3] [,4] [,5]
[1,]    3   15   27   39   51
[2,]    6   18   30   42   54
[3,]    9   21   33   45   57
[4,]   12   24   36   48   60
```
- 자료구조 확인하기
```R
class(iris) # iris 데이터셋 자료구조 확인
is.matrix(iris) # 데이터셋이 매트릭스인지 확인하는 함수
is.data.frame(iris) # 데이터셋이 데이터프레임인지 확인하는 함수
```
- 매트릭스와 데이터프레임 자료구조 변환
```R
# 매트릭스를 데이터프레임으로 변환
is.matrix(state.x77)
st <- data.frame(state.x77)
head(st)
class(st)

# 데이터프레임을 매트릭스로 변환
is.data.frame(iris[,1:4]
iris.m <- as.matrix(iris[,1:4])
head(iris.m)
class(iris.m)
```
- 데이터프레임에만 적용되는 열 추출 방법
```R
iris[,"Species"] # 결과가 벡터-매트릭스, 데이터프레임 모두 가능
iris[,5] # 결과가 벡터-매트릭스, 데이터프레임 모두 가능
iris["Species"] # 결과가 데이터프레임-데이터프레임만 가능
iris[5] # 결과가 데이터프레임-데이터프레임만 가능
iris&Species # 결과가 벡터-데이터프레임만 가능
```
### 데이터 입출력
1. R에서의 입출력
   자료의 입력 -> 자료의 처리/정보의 추출 -> 처리 결과 출력
```R
# 데이터 입력
age <- c(28, 17, 35, 46, 23, 67, 30, 50)
age
# 정보 추출
young <- min(age)
old <- max(age)
# 처리 결과 출력
cat('가장 젊은 사람의 나이는 ', young, '이고',
    '가장 나이든 사람의 나이는', old, '입니다,\n')
```
2. 화면에서 데이터 입력받기
```R
install.packages('svDialogs')   # 패키지 설치
library(svDialogs)
user.input <- dlgInput('Input income')$res
user.input
income <- as.numeric(user.input)   # 문자열을 숫자로 계산
income
tax <- income * 0.05   # 세금 계산
cat('세금: ', tax)
```
3. print()함수 vs cat()함수
     |함수|특징|
     |------|---|
     |print()|- 하나의 값을 출력할 때 - 데이터프레임과 같은 2차원 자료구조를 출력할 때 - 출력 후 자동 줄바꿈|
     |cat()|- 여러 개의 값을 연결해서 출력할 때(벡터는 출력되나 2차원 자료구조는 출력되지 않음 - 출력 후 줄바꿈을 하라면 '\n' 필요|
4. 작업 폴더
   자신이 읽거나 쓰고자 하는 파일이 위치하는 폴더
   ```R
   getwd() # 현재 작업 폴더 알아내기
   setwd('C:/Rworks') # 작업 폴더 변경하기
   getwd()
   ```
5. csv 파일 읽기와 쓰기
   R에서 데이터 분석을 위해 가장 많이 사용하는 파일 형태
   - csv 파일에서 데이터 읽기
   ```R
   setwd('C:/Rworks') # 작업 폴더 지정
   air <- read.csv('airquality.csv', header=T) # .csv 파일 읽기
   header(air)
   class(air) # air의 자료구조 확인
   ```
   - csv 파일에서 데이터 쓰기
   ```R
   setwd('C:/Rworks') # 작업 폴더 지정
   my.iris <- subset(iris, Species=='setosa') # setosa 풍속 데이터만 추출
   write.csv(my.iris, 'my_iris.csv', row.name=F) # .csv 파일에 저장하기
   ```
6. 엑셀 파일 읽기와 쓰기
   ```R
   install.packages('xlsx') # 패키지 설치하기
   library(xlsx) # 패키지 불러오기
   air <- read.xlsx('C:/Rworks/airquality.xlsx', header=T,
                     sheetIndex=1) # .xlsx 파일 읽기
   head(air)
   ```
   ```R
   library(xlsx) # 패키지 불러오기
   my.iris <- subset(iris, Speciess=='setosa') # iris 데이터셋에서 setosa 품종의 행들만 추출하여 my.iris.에 저장
   write.xlsx(my.iris, 'my_iris.xlsx', row.names=F) # 파일에 저장하기
   ```
## 📅 230330
### 자료의 종류
  1. 1차원 자료 : 단일 주제에 대한 값들의 모아 놓은 자료 (ex 벡터, 리스트, 팩터)
  2. 2차원 자료 : 복수 주제에 대한 값들을 모아 놓은 자료 (ex 매트릭스, 데이터프레임, 조사 결과)
  3. 범주형 자료 : '분류'의 의미를 갖는 값들로 구성된 자료, 보통 문자로 표현되고 산술연산을 적용할 수 없음
  4. 수치형 자료 : 값들이 크기를 가지며 산술연산 가능 
### 백터 연산
1. 벡터에 대한 산술연산은 벡터 안에 포함된 값들 하나하나에 대한 연산으로 바뀌어 실행
```R
d <- c(1,4,3,7,8)
2*d
[1] 2 8 6 14 16
```
2. 벡터와 벡터의 연산 : 벡터 간 대응되는 위치의 값들끼리 연산
```R
x <- c(1,2,3,4)
y <- c(5,6,7,8)
z <- x+ y
z
[1] 6 8 10 12
```
3. 벡터와 벡터의 연산이 가능하기 위한 조건
   1. 두 벡터의 길이가 동일해야 함
   2. 두 벡터에 포함된 값의 종류 동일
4. 벡터에 적용 가능한 함수들
     |함수명|설명|
     |------|---|
     |sum()|벡터에 저장된 값들의 합|
     |mean()|벡터에 저장된 값들의 평균|
     |max(), min()|벡터에 저장된 값들의 최댓값, 최솟값|
     |var()|벡터에 저장된 값들의 분산|
     |sort()|벡터에 저장된 값들을 정렬(오름차순이 기본)|
     |length()|벡터에 저장된 값들의 개수(벡터의 길이)|
 5. 벡터에 논리연산자 적용
     |연산자|사용 예|설명|
     |------|---|---|
     |<|A<B|B가 A보다 크면 TRUE|
     |<=|A<=B|B가 A보다 크거나 같으면 TRUE|
     |==|A==B|A와 B가 같으면 TRUE|
     |!=|A!=B|A와 B가 같지 않으면 TRUE|
     |&|A&B|A와 B모두 TRUE일 때만 TRUE|
 6. 벡터와 벡터의 연산 : 벡터 간 대응되는 위치의 값들끼리 연산
```R
d <- 1:9
d >= 5
[1] FALSE FALSE FALSE FALSE TRUE TRUE TRUE TRUE TRUE
```
### 팩터와 리스트
1. 팩터(facotr)
   문자형 데이터가 저장되는 벡터, 저장되는 문자값들이 어떠한 종류를 나타내는 값일 때 사용
   ```R
   bt <- c('A', 'B', 'B', 'O', 'AB','A') # 문자형 벡터 bt 정의
   bt.new <- factor(bt) # 팩터 bt.new 정의
   bt # 벡터 bt의 내용 출력
   bt.new # 팩터 bt.new의 내용 출력
   bt[5] # 벡터 bt의 5번째 값 출력 [1] "AB"
   bt.new[5] # 팩터 bt.new의 5번째 값 출력 [1] AB
   levels(bt.new) # 팩터에 저장된 값의 종류를 출력 [1] "A" "AB" "B" "O"
   as.integer(bt.new) # 팩터의 문자값을 숫자로 바꾸어 출력 [1] 1 3 3 4 2 1
   bt.new[7] <- 'B' # 팩터 bt.new의 7번째에 'B' 저장
   bt.new # 팩터 bt.new의 내용 출력
   ```
2. 리스트(list)
   자료형이 다른 값들을 한곳에 저장
   ```R
   이름 : 'Tom' 나이 : 25
   학생 여부 : TRUE 취미 : 'balling', 'tennis', 'ski'
   ```
   ```R
   h.list <- c('balling', 'tennis', 'ski')
   person <- list(name='Tom', 
                  age=25,
                  student=TRUE, 
                  hobby=h.list)
   ```
   ```R
   person[[1]]
   [1] "Tom"
   person$age
   [1] 25
   ```
### 매트릭스와 데이터프레임
    2차원 자료 저장하는 자료구조
1. 매트릭스(matrix)
  - 모든 자료의 종류가 동일
  - 가로줄 : 행 or 관측값
  - 세로줄 : 열 or 컬럼 or 변수
  - 보통 숫자로만 구성된 2차원 자료 저장
  ```R
  z <- matrix(1:20, nrow=4, ncol=5)
  z
       [,1] [,2] [,3] [,4] [,5]
  [1, ]   1    5    9   13   17
  [2, ]   2    6   10   14   18
  [3, ]   3    7   11   15   19
  [4, ]   4    8   12   16   20
  ```
2 데이터프레임(data frame) : 서로 다른 종류의 데이터 저장
  - 숫자형 자료와 문자형 자료가 결합되어 있는 형태
  ```R
  city <- c("Seoul", "Tokyo", "Washington") # 문자로 이루어진 벡터
  rank <- c(1,3,2) # 숫자로 이루어진 벡터
  city.info <- data.frame(city, rank) # 데이터프레임 생성
  city.info # city.info의 내용 출력
  ```
## 📅 230323
### R 패키지
  1. 패키지(package) ?
      - 함수들을 기능별로 묶어 놓은 것
      - 로딩(loading) : 패키지를 R에서 사용할 수 있도록 불러오는 작업
      - 패키지는 작업 중인 컴퓨터의 특정 폴더에 저장되어 있어야 로딩 가능
  2. 패키지 설치
      
      ` 1. 특정함수를 포함하고 있는 패키지 설치하기(install)
        2. 설치한 패키지 불러오기(load)`
      - install.packages() 함수를 이용하여 설치
      - 로딩(loading) : 패키지를 R에서 사용할 수 있도록 불러오는 작업
      - 패키지는 작업 중인 컴퓨터의 특정 폴더에 저장되어 있어야 로딩 가능
      - library() 함수를 이용해 패키지 로드
### 변수(variable)
  - 어떤 값을 저장해 놓을 수 있는 역할
  - <- : 값을 변수에 저장하는 연산자
  - a <- 10 = 10을 a에 저장하라
  1. 변수명 작명 규칙
      - 첫 글자는 영문자 or 마침표로 시작
      - 두 번째 글자부터 영문자, 숫자, 마침표, 밑줄 사용 가능
      - 대문자와 소문자 별개 취급
      - 변수명 중간 공백 입력 불가
  1. 자료형(data type) : 변수에 저장할 수 있는 값의 종류
     
     |자료형|사용 예|비고|
     |------|---|---|
     |숫자형|1,-4,12.8|정수, 실수 모두 가능|
     |문자형|'YeonJae', "duswo"|작은따옴표나 큰따옴표로 묶어서 표현|
     |논리형|TRUE(참), FALSE(거짓)|T,F로 줄여서도 사용 가능|
     |특수값|NULL|정의되어 있지 않음|
### 벡터(vector)
  - 다수의 값을 한꺼번에 저장하는 기능, 1차원 배열
  - 벡터 만들기
  
    `x <- c(1,2,3)`
    
    `y <- c('a','b','c')`
    
    `z <- c(TRUE,TRUE, FALSE,TRUE)`
  - 인덱스(index) : 벡터에 저장된 각 값들을 구별하기 위해 앞쪽 값부터 순서를 부여
### 함수
  - y = f(x)
  - 어떤 값 x를 입력받아 정해진 계산 수행 후 결과값f(x)를 돌려주는 것
  - 매개변수(parameter) : 입력 값을 받는 변수
## 📅 230316
### R 언어의 특징
1. 미적이고 기능적인 통계 그래프 제공
 - 데이터 분석에 있어 분석 결과를 시각적으로 표현하는 것 중요
 - ggplot 패키지 : 아름다우면서 기능적인 그래프 작성을 지원하는 패키지
2. 편리한 프로그래밍 환경
 - R 스튜디오 : R 프로그래밍 위한 개발 환경
 - 프로그램 작성, 실행, 수정 등 여러 작업 수행 가능
 => 통합 개발 환경 = IDE
### R을 배우는 이유
 1. 4차 산업혁명의 중심 '데이터'
 2. 시대적 흐름은 데이터를 잘 다룰 줄 알아야 우위 점령 가능
 3. 컴퓨팅 사고와 데이터 활용 능력은 더욱더 중요해지는 스펙
 4. 배우기 쉬우면서도 강력한 데이터 처리 및 데이터 분석 능력 제공
 5. 프로그래밍 언어로 컴퓨팅 사고를 배우기에 적합
### R 스튜디오 화면 구성
 1. 소스 영역
  - 소스창(Source Pane) : R 명령문 작성, 실행하는 영역
  - Run 버튼을 눌러야 명령문 실행
  - 명령문 ? 컴퓨터에서 어떤 일을 시키기 위한 작업 지시 문장
     R 프로그램은 명령문들의 집합으로 이루어짐
 2. 콘솔 영역
  - 콘솔창(Console Pane) : 소스창에서 작성한 R 명령문 실행시 결과가 표시되는 영역
  - 터미널창(Terminal Pane) : 윈도우의 '명령 프롬포트'와 동일한 기능
 3. 환경 영역
  - 환경창(Environment Pane) : R 명령문이 실행되는 동안 만들어지는 각종 변수, 자료구조의 내용을 보여주는 영역
  - 히스토리창(History Pane) : R 스튜디오에서 실행한 명령문, 결과, 패키지 설치, 오류 등 거의 모든 작업 과정에 대한 이력 표시
  - 커넥션창(Connection Pane) : R과 데이터 관리를 위한 서버를 연결하는 창
  - 튜토리얼창(Tutorial Pane) : R을 따라하며 배울 수 있는 창
 4. 파일 영역
  - 파일창(Files Pane) : 윈도우의 파일 탐색기와 동일 역할
  - 특정 파일을 R 스튜디오를 불러오거나 복사, 삭제, 이동등의 작업 수행 가능작업 폴더 지정 가능
  - 작업 폴더 설정 방법 : [More]-[Set As Working Directory]
  - 플롯창(Plot Pane : 그래프가 표시되는 영역
  - 패키지창(Packages Pane) : 함수들의 작성 목정, 개발자에 따라 패키지 형태로 묶여 제공
  - 도움말창(Help Pane) : 특정 함수에 대한 도움말 제공
  - 뷰어창(Viewer Pane) : 분석의 결과가 이미지 형태일 때 웹브라우저 상에 결과를 출력하는 경우가 있음, 이 경우 뷰어창에 표시
### R 명령문
  1. '<-' 대입 연산자
  2. 'print()' 출력함수
  3. 실행
      - 소스창에 있는 모든 명령문 실행 : Ctrl + Alt + R
  4. 한 줄에 여러 개의 명령문 작성시 명령문 사이에 ';' 입력
      
       `3 + (4 * 5) ; A <- 51:80 ; print(A)`
