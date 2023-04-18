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

<details>
<summary>버블정렬(Bubble Sort)에 대해 설명해주세요</summary>

<br>

- 이중 For문에서 n번째와 n+1번째의 숫자를 비교하고 큰 수를 뒤로 보내도록 자리를 바꾸며 매 반복마다 마지막 가장 큰 수를 찾아 정렬해가는 방법이다.
- 이중 for문을 돌아 $O(n^2)$의 시간복잡도를 갖는다.

```java
public void bubbleSort(int[] arr) {
    int size = arr.length;
    for (int i = 1; i < size; i++) {
        for (int j = 0; j < size - i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr, j, j + 1);
            }
        }
    }
}

private void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

</details>

<details>
<summary>삽입정렬(Insertion Sort)에 대해 설명해주세요.</summary>

<br>

- 데이터를 하나씩 확인하며 각 데이터를 적절한 위치에 삽입하는 알고리즘이다.
- 데이터가 거의 정렬되어 있을 때 훨씬 효율적이다.
- 선택 정렬에 비해 실행 측면에서 더 효율적인 알고리즘이다.
- 삽입 정렬은 특정한 데이터가 적절한 위치에 들어가기 이전에 그 앞까지는 이미 정렬되었다고 가정한다.
- 시간복잡도는 $O(N^2)$ 이다.
    - 하지만 배열이 먼저 정렬되어 있다면 $O(N)$의 시간 복잡도를 갖게 된다.

```java
public void insertionSort(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        for (int j = i; j > 0; j--) {
            if (arr[j] < arr[j - 1]) {
                swap(arr, j, j - 1);
            } else {
                break;
            }
        }
    }
}

private void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

</details>