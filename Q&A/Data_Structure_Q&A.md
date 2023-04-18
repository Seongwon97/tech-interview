<details>
<summary>선택정렬(Selection Sort)에 대해 설명해주세요.</summary>

<br>

- 가장 작은 것을 선택해서 앞으로 보내는 과정을 반복해서 수행하는 정렬 방법이다.
    - 앞으로 보낼 때는 보내야할 위치의 수와 값을 변경하는 식으로 진행된다.
- 연산 횟수는 `N + (N-1) + (N-2) + … + 2`로 `N x (N + 1) / 2`가 된다. 그래서 시간복잡도는 $O(N^2)$ 가 된다.

```java
public void selectionSort(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        int minIndex = i;
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[minIndex] > arr[j]) {
                minIndex = j;
            }
        }
        swap(arr, i, minIndex);
    }
}

private void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

- 선택 정렬은 기본 정렬과 퀵 정렬과 비교하였을 때 매우 비효율적이다. 하지만 **특정한 리스트에서 가장 작은 데이터를 찾는 일이 코딩 테스트에서 잦으므로 선택 정렬 코드를 익혀두는 것이 좋다.**

</details>

