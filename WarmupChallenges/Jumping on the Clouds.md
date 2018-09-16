# 문제

엠마는 연속된 숫자가 매겨진 구름으로 시작하는 새로나온 모바일 게임을 플레이합니다. 어떤 구름은 천둥구름이고 어떤 구름은 뭉게구름입니다. 엠마는 뭉게구름만 밟을 수 있으며, 한번에 한칸 혹은 두칸 움직일 수 있습니다. 엠마가 천둥구름을 밟지 않고 끝에 도달할 수 있는 최소한의 횟수를 구해주세요.

엠마는 첫번째 구름을 밟고있고, 마지막 구름을 밟으면 게임을 이깁니다. 게임은 항상 깰 수 있게 나옵니다.

뭉게구름은 `0`, 천둥구름은 `1`로 주어집니다. 즉, 0은 건널 수 있고 1은 무조건 피해야 합니다.
예를들어, `c = [0,1,0,0,0,1,0]`는 0에서 6의 index를 가집니다. 반드시 피해야 하는 index는 1과 5입니다. 엠마는 두가지 경우의 수로 구름다리를 건널 수 있습니다: `0>2>4>6` 혹은 `0>2>3>4>6`으로요. 첫번째 경로는 세번만 이동하면 됩니다. 두번째 경로는 4번 건너야 합니다.

# 예시
Input:
```
7
0 0 1 0 0 1 0
```
Output:
```
4
```
설명:
엠마는 무조건 c[2], c[5]를 건너뛰어야 합니다. 4번이면 끝에 도달할 수 있습니다. (0>1>3>4>6)

# 풀이
두칸 뒤가 0이라면 무조건 두칸을 가고, 두칸 뒤가 1이라면 한칸을 가는 것이 최단경로입니다.

게임을 못 깨는 경우는 주어지지 않는다고 했으니,
* 1이 연속되어 나올 수는 없습니다.
* 마지막 구름은 항상 0입니다. 그러므로 검사할 구름이 2개 이하라면 검사를 종료할 수 있습니다.

```js
function jumpingOnClouds(c) {
  let count = 0
  for (let i = 0; i < c.length; i++) {
    count++

    // 더 검사할 구름이 2개 이하로 남았다면 종료합니다.
    if (i >= c.length-3) {
      break
    }
    // 0이면 두칸을 가므로 i++합니다.
    if (c[i + 2] === 0) { i++ }
  }
  return count
}
```