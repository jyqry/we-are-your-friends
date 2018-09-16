# 문제
릴라는 string `s` 를 가지고 있습니다: 영어 소문자로 구성되었으며 `s` 가 무한반복됩니다.
integer `n` 이 주어집니다. 무한반복되는 `s`의 n번째까지의 문자 중 `a`의 갯수를 세주세요.

예를들어 `s = 'abcac'`고 `n = 10`이라면 우리가 찾아야 할 것은 `abcacabcac`에서 `a`가 들어간 횟수, 즉 4를 반환하면 됩니다.

# 요약
s: 반복될 string입니다.
n: 고려해야할 문자의 갯수입니다.

# 예시
Input:
```
aba
10
```
Output:
```
7
```
설명:
aba, 10이 입력으로 들어왔으므로 `abaabaabaa`에서 a의 갯수인 7을 출력합니다.

# 풀이
n은 최대 1,000,000,000,000(10^12)이므로 문자열을 만들고 a를 순회한다면 시간이 너무 많이 소요됩니다.

그러므로 s에 a가 몇개 있는지를 센 다음, `Math.floor(n/s.length) // n/s.length의 몫`만큼 곱해줍니다.
`Math.floor(n/s.length)`인 이유는 n번째 문자가 s 중간에서 끝날 수 있기 때문입니다.
그 다음, n/s.length의 나머지만큼 s에서 a 개수를 세서 더해줍니다.

```js
function repeatedString(s, n) {
  let count = 0
  let c = 0
  if (s.indexOf('a') === -1) { return 0 }
  for (let i = 0; i < s.length; i++) {
    if (s[i] === 'a') {
      count++
      if (i < n%s.length ) { c++ }
    }
  }
  return count*Math.floor(n/s.length) + c
}
```
