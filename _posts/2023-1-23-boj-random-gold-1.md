---
layout: post
title: "[백준] 랜덤 골드 문제 풀이 모음 1"
categories: [PS]
use_math: true
tags: [random_gold]
---

## 개요

최근 들어서 PS실력이 편중되어 있다는 생각이 들어서 백준에서 랜덤하게 골드 문제를 해결하면서 실력을 높이려고 하고 있습니다.

해결한 골드 문제들과 그 풀이를 간략하게 정리해두려고 합니다.

### BOJ 27066. 나무 블럭 게임

[Good Bye, BOJ 2022!](https://www.acmicpc.net/category/detail/3426)에 참여해서 푼 문제입니다.

$N$개의 주머니에 각각 나무 블럭이 하나씩 들어있으며, 매번 두 개를 선택해 합칩니다.

이를 원하는 만큼 반복한 뒤 남아있는 주머니 각각의 평균의 중앙값 ($\left[ \frac{K+1}{2} \right]$번째 값)을 최대화하는 문제입니다.

<details>
<summary>풀이</summary>
<div markdown="1">
두 주머니를 하나로 합쳤을 경우 평균은 큰 값의 평균보다 감소합니다.

주머니를 평균을 기준으로 정렬해 두고 생각합시다.

가장 평균이 작은 주머니와 그 다음 주머니 두 개를 합치는 경우를 생각해봅니다.
이때, 새로 만들어진 주머니의 평균 또한 최소입니다.

이렇게 합치는 방식이 제일 좋을까요?
개수가 홀수일 때와 짝수일 때로 나눠서 한 번 생각해 봅시다.

개수가 홀수일 때는, 합친 이후 평균의 중앙값이 그대로 유지됩니다.
(주머니 개수가 하나 줄고, 중앙값 위치도 하나 당겨지기 때문)

개수가 짝수일 때는, 합친 이후 평균의 중앙값이 증가합니다.
(주머니 개수는 하나 줄었는데 중앙값 위치는 그대로이기 때문)

따라서, 이 과정을 반복하면서 평균의 중앙값을 증가시킬 수 있습니다.

단, 개수가 3일 때는 합친 이후 평균의 중앙값이 감소합니다.

&nbsp;

합치는 방법이 평균이 작은 두 주머니를 합치는 방법이기 때문에, 처음 주머니의 개수가 3 이상일 경우 전체의 평균과 값 중 두번째로 큰 값 중 큰 것이 됩니다.

처음 주머니의 개수가 2개일 경우는 두 값의 평균이 됩니다.

물론, $N \leq 100 000$이기 때문에, 매번 주머니를 합치면서 평균의 중앙값의 최댓값을 유지하도록 코드를 짜도 됩니다.
</div>
</details>

### BOJ 27067. 데이터 순서 복원

마찬가지로 [Good Bye, BOJ 2022!](https://www.acmicpc.net/category/detail/3426)에 참여해서 푼 문제입니다.

1부터 $N$까지의 수가 단 한 번씩만 포함된 길이 $N$의 배열이 있습니다.
이 배열을 찾는 문제입니다.

주어지는 데이터는 총 세 개로, 배열의 값 중 하나가 원래 위치에서 더 앞의 위치로 옮겨져 있습니다.

각 데이터마다 앞으로 옮겨진 데이터는 서로 다릅니다.

<details>
<summary>풀이</summary>
<div markdown="1">
첫 번째 데이터를 $a$, 두 번째 데이터를 $b$, 세 번째 데이터를 $c$라고 합시다.

$a$와 $b$를 서로 비교합니다.
$a$의 $i$번째 값이 앞의 위치로 옮겨진 값이라고 가정합니다. $a$에서 $i$번째 값이 빠진 새로운 배열을 만들어 $a'$라고 합시다.

이후 $b$를 순서대로 살피며 $a_i = b_j$인 $j$를 찾는 것과 동시에 $a'$와 $b$에서 순서가 맞지 않은 값을 찾습니다.

만일 순서가 맞지 않은 값이 두 개 이상이면 가정이 틀렸다는 것이므로 다음 $i$로 넘어갑니다.

이 정보를 바탕으로 원래 데이터를 복원할 수 있습니다.

이후 이를 $c$와 비교하며 순서가 맞지 않은 값이 하나뿐인지 확인합니다.

하나뿐일 경우 답을 찾았기 때문에 출력하고, 아닐 경우 다음 $i$로 넘어가서 반복합니다.

위상 정렬을 이용해서도 문제를 해결할 수 있다고 합니다. 이 경우가 풀이가 더 간단할 것 같습니다.
</div>
</details>

### BOJ 27084. 카드 뽑기

$N$장의 카드가 있고 각각을 뽑을 확률이 $\frac{1}{2}$입니다. 뽑은 카드에 적힌 정수가 모두 다를 확률을 구하는 문제입니다.

<details>
<summary>풀이</summary>
<div markdown="1">
$(2^N-1)p$가 정수인 것은 쉽게 알 수 있습니다. 카드를 한 장도 뽑지 않았을 경우 다시 진행하기 때문에, 가능한 모든 경우의 수가 $2^N-1$가지이기 때문입니다.

다르게 이야기하면, 전체 경우의 수는 $2^N-1$이니 뽑은 카드에 적힌 정수가 모두 다른 경우의 수를 찾으면 됩니다.

서로 독립인 여러 부분으로 나눈 후 경우의 수를 계산해 곱하면 전체 경우의 수를 찾을 수 있습니다.
적힌 정수가 같은 카드가 $m$개 있는 상황을 생각해 봅시다. 뽑은 카드에 적힌 정수가 모두 다르기 위해서는 이 카드들 중 아무 것도 뽑지 않은 경우 또는 한 장만 뽑은 경우여야 합니다. 즉, $m+1$개의 경우의 수가 가능합니다.

적힌 정수가 같은 카드들로 나눠 각각 개수를 찾은 후 (개수+1)을 곱합니다.
모든 나눠진 부분에서 한 장도 뽑지 않은 하나의 경우의 수는 제외해야 하므로 1을 뺀 값을 $10^9+7$로 나눈 나머지를 계산하면 됩니다.
</div>
</details>

### BOJ 6594. 방정식 풀기

방정식의 모든 부분식도 일차인 일차방정식이 주어집니다. 방정식의 해를 찾으면 됩니다.

<details>
<summary>풀이</summary>
<div markdown="1">
파싱 및 구현 문제입니다.

`Expr`이라는 클래스를 만들어서 사용했습니다.
`Expr`은 두 개의 멤버 변수 `a, b`를 가지며, $ax+b$를 의미합니다.

부분식도 일차식이라는 점을 활용해 `Expr` 간의 연산을 구현할 수 있습니다.

이제 방정식을 앞에서부터 읽으면서 `Expr`을 계산합니다.
덧셈/뺄셈/곱셈의 경우 연산을 기록해 두고, 괄호를 만나면 재귀호출해서 식을 찾습니다.

이후 곱셈을 먼저 전부 계산하고 덧셈/뺄셈을 순서대로 계산합니다.

이를 통해 식을 계산할 수 있으며, 등호를 기준으로 좌/우 식을 계산하고 서로 뺀 후 $x$를 찾으면 됩니다.
</div>
</details>

### BOJ 20040. 사이클 게임

두 점을 잇는 선분을 그은 순서가 주어질 때 사이클이 생겼는지, 생겼다면 몇 번째 차례에서 사이클이 생겼는지 찾는 문제입니다.

<details>
<summary>풀이</summary>
<div markdown="1">
분리 집합을 이용해 해결할 수 있습니다.

순서대로 merge하면서 진행하다가 parent가 같은 경우는 사이클이 생겼다는 뜻이므로 차례 번호를 출력하면 됩니다.

이때, 개수가 많은 쪽에 개수가 적은 쪽을 붙이도록 진행해야 문제 없이 해결할 수 있습니다.
그냥 붙일 경우 RecursionError 등이 발생합니다.
</div>
</details>

### BOJ 13625. Boss

여러 개의 manage 관계가 주어집니다.
한 사람이 여러 사람에게 manage 될 수도 있고, 한 사람이 여러 사람을 manage 할 수도 있습니다.
manage 관계는 cycle을 구성하지는 않습니다.

각 사람의 나이가 주어집니다.
이후 여러 개의 쿼리를 해결해야 합니다.

첫 번째 쿼리는 두 명의 위치를 뒤바꾸는 쿼리입니다.
위치를 뒤바꾼다는 것은 다른 사람과의 위치관계를 뒤바꾼다는 의미입니다.

두 번째 쿼리는 특정 사람을 manage하는 사람 중 가장 나이가 작은 사람의 나이를 찾는 쿼리입니다.

<details>
<summary>풀이</summary>
<div markdown="1">
문제에 나와있는 그림과는 간선의 방향을 반대로 연결합니다.

각 사람에 해당하는 노드를 (이름, 노드) 쌍의 딕셔너리를 통해 관리합니다.

첫 번째 쿼리의 경우 딕셔너리 정보를 바꿔줍니다.

두 번째 쿼리의 경우 입력으로 들어온 사람에서 출발해서 그래프를 탐색, 나이가 가장 작은 사람의 나이를 구하면 됩니다.
</div>
</details>

### BOJ 23237. How Many Subtrees?

트리가 주어집니다.

이 트리의 subtree의 개수를 찾는 문제입니다.

<details>
<summary>풀이</summary>
<div markdown="1">
임의의 node를 root node로 설정했다고 합시다.

임의의 node $p$에 대해 부분문제 `dp[p] := p를 루트로 하는 subtree에 속한 subtree 개수`로 정의합니다.

subtree 개수는 $p$를 포함하는 subtree 개수 + $p$를 포함하지 않는 subtree 개수입니다.

포함하지 않는 경우는 각 child의 subtree 개수를 구해서 더하면 됩니다.

포함하는 경우는 각 child의 subtree 개수에 1을 더한 후 모두 곱하면 됩니다.

이제 root node를 설정하는 것만 잘 해내면 됩니다.

각 node를 양방향으로 연결하고 임의의 node를 잡아서 높이를 0으로 설정, 높이가 설정되지 않은 연결된 node에 높이를 설정해주는 것을 반복해 모든 node에 높이를 주면 됩니다.

연결된 node 중 높이가 높은 하나의 node가 parent, 나머지가 child가 됩니다.
</div>
</details>

### BOJ 25237. Word Ladder

word ladder을 만드는 문제입니다.

인접한 두 단어는 한 글자만 차이나고, 인접하지 않은 두 단어는 한 글자 넘게 차이나게 해야 합니다.

각 단어의 길이는 최대 10글자로 해야 합니다.

<details>
<summary>풀이</summary>
<div markdown="1">
길이 5000 이상의 word ladder을 만들 수 있다면 끊어서 사용하면 됩니다.

단어 양 끝이 a인 단어들, 단어 양 끝이 b인 단어들, ... 을 만들 것입니다.
이 경우, 서로 단어 양 끝이 다른 경우에는 적어도 두 글자 차이나기 때문에 조건을 만족합니다.

각 분류 안에서 글자를 만들 방법을 생각합니다.
쓸 수 있는 글자가 총 8글자이고 조건을 만족해야 하기 때문에 한 글자씩 바꿔나가야 합니다.

다음과 같은 식으로 중간 8글자를 만듭니다.
aaaaaaaa, aaaaaaab, aaaaaabb, ..., abbbbbbb, bbbbbbbb, bbbbbbbc, ...
이 경우, 인접한 두 글자는 한 글자만 차이나고 인접하지 않은 글자는 두 글자 이상 차이납니다.

단어 양 끝을 변환하는 경우는 순서대로 양 끝을 바꿔주도록 하면 됩니다.

중간 8글자를 만들 때, 한 바퀴를 다 돌지 않고 한 개씩 남겨줍니다.
이를 통해, 단어 양 끝이 같은 단어들의 첫 번째와 마지막 단어가 두 글자 이상 차이나게 유지하면서, 단어 양 끝을 바꾸는 과정에서도 문제가 발생하지 않게 됩니다.
</div>
</details>

### BOJ 11956. OZLJEDA

$a_1, a_2, ..., a_k$가 주어집니다.

$x_1, ..., x_k$는 $a_1, ..., a_k$와 같습니다.

$x_n=x_{n-1} \oplus x_{n-2} \oplus ... x_{n-k}, n>k$입니다. $\oplus$는 bitwise xor을 의미합니다.

$l$과 $r$이 주어지면 $x_l$부터 $x_r$까지를 bitwise xor한 값을 구해야 합니다.

<details>
<summary>풀이</summary>
<div markdown="1">
$x$ 값은 $k+1$의 주기를 가진다는 것을 쉽게 알 수 있습니다.

이를 바탕으로, 누적 합 배열을 구해보면 누적 합 배열 역시 $k+1$의 주기를 가진다는 것을 알 수 있습니다.

$r$까지의 부분합과 $l-1$까지의 부분합을 구해서 bitwise xor하면 답을 구할 수 있습니다.
</div>
</details>

### BOJ 27231. 2023년이 기대되는 이유

[Hello, BOJ 2023!](https://www.acmicpc.net/category/detail/3456) 오픈 콘테스트에서 해결한 문제입니다.

양의 정수가 주어집니다.

양의 정수의 각 자릿수 사이에 0개 이상의 + 기호를 넣어서 계산했을 때 자릿수의 $m$제곱과 같아지도록 하는 $m$의 개수를 구하면 됩니다.

<details>
<summary>풀이</summary>
<div markdown="1">
들어오는 양의 정수 $n$이 0 아니면 1로만 이루어져 있을 경우, 가능한 $m$의 개수는 무수히 많습니다.

적어도 하나의 자릿수 값이 2 이상이라고 합시다.
$m=1$인 경우에는 자명하게 가능합니다.
$n$은 10억 이하이고 $2^30=1073741824>1000000000$이기 때문에, $m$은 최대 29입니다.

모든 가능한 $m=2, 3, ..., 29$에 대해, 자릿수의 $m$제곱을 계산합니다.

이후 자릿수가 많아봐야 10개이므로 +를 넣는 모든 경우를 살펴봅니다.

적당한 가지치기를 해주면 손쉽게 AC를 받을 수 있습니다.
</div>
</details>

### BOJ 27211. 도넛 행성

도넛 행성 위에서 빈 구역의 개수를 세는 문제입니다.

1인 칸은 숲이 있는 칸이며, 숲이 있는 칸을 지나지 않고 도달할 수 있는 칸들은 같은 구역입닌다.

<details>
<summary>풀이</summary>
<div markdown="1">
BFS나 DFS를 사용하면 됩니다.

기본적인 풀이는 [BOJ 1012번](https://www.acmicpc.net/problem/1012)등과 똑같습니다.

도넛의 경우 펼쳤을 때 위아래, 그리고 좌우가 각각 연결되어 있다고 생각하면 됩니다.

이를 생각해서 탐색을 진행하면 됩니다.
</div>
</details>