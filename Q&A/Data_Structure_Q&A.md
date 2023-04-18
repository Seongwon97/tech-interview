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

<details>
<summary>퀵정렬(Quick Sort)에 대해 설명해주세요.</summary>

<br>

- 가장 많이 사용되는 정렬 알고리즘이다. 병합 정렬 알고리즘도 퀵 정렬과 같이 빠르다.
- 기준 데이터(`pivot`)를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 알고리즘이다.
    - 퀵 정렬을 수행하기 전에는 피벗을 어떻게 설정할 것인지 미리 명시해야 한다.
    - 대표적인 분할방식으로는 호어 분할(`Hoare Partition`) 방식이 있다.

      > 호어 분할 방식: 리스트에서 첫 번째 데이터를 피벗으로 정한다.
>

```java
public void quickSort(int[] arr, int start, int end) {
    if (start >= end) {
        return;
    }
    int pivot = start; // 호어 방식으로 첫번째 값을 pivot으로 설정
    int left = start + 1;
    int right = end;
    while (left <= right) {
        // pivot보다 큰 데이터를 찾을 때까지 반복
        while (left <= end && arr[left] <= arr[pivot]) {
            left++;
        }
        // pivot보다 작은 데이터를 찾을 떄까지 반복
        while (right > start && arr[right] >= arr[pivot]) {
            right--;
        }

        if (left > right) { // 엇갈렸다면 작은 데이터와 피벗을 교체
            swap(arr, right, pivot);
        } else { // 엇갈리지 않았다면 작은 데이터와 큰 데이터를 교체
            swap(arr, left, right);
        }
    }
    // 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
    quickSort(arr, start, right - 1);
    quickSort(arr, right + 1, end);
}

private void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

- 퀵 정렬의 평균 시간 복잡도는 $O(NlogN)$이다
    - 최악의 시간복잡도는 $O(N^2)$ 이다. 피벗을 정하는 방식을 가장 왼쪽의 값을 갖는 호어 분할 방식으로 진행할 경우, 이미 데이터가 정렬되어 있는 경우 느리게 작동한다.

</details>

<details>
<summary>계수 정렬(Count Sort)에 대해 설명해주세요.</summary>

<br>

- 특정한 조건이 부합할 때만 사용할 수 있지만 매우 빠른 정렬 알고리즘이다.
- 데이터의 개수가 N, 데이터 중 최댓값이 K 일때, 계수 정렬은 최악의 경우에도 수행시간 $O(N+K)$를 보장한다.
- 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때만 사용 가능하다. (무한한 범위는 사용 불가)
    - 모든 범위를 담을 수 있는 크기의 리스트(배열)을 선언하여 사용하기 때문에 가장 큰 데이터와 가장 작은 데이터의 차이가 너무 커도 계수 정렬은 사용할 수 없다.
- 데이터의 크기가 많이 중복되어 있을수록 유리하다.
- 계수 정렬은 직접 데이터의 값을 비교한 뒤에 위치를 변경하며 정렬하는 방식이 아니다.
- 과정
    1. 가장 큰 데이터와 가장 작은 데이터의 범위가 모두 담길 수 있는 리스트를 생성한다.
    2. 리스트의 모든 데이터가 0이 되도록 초기화한다.
    3. 데이터를 하나씩 확인하며 데이터의 값과 동일한 인덱스의 데이터를 1씩 증가시킨다.
    4. 리스트의 첫 번째 데이터부터 리스트의 값만큼 Index를 출력한다.

```java
public List<Integer> countSort(int[] arr, int max) {
    // 모든 범위를 포함하는 리스트 선언(모든 값은 0으로 초기화)
    int[] count = new int[max + 1];
    for (int i = 0; i < count.length; i++) {
        count[arr[i]]++; // 각 데이터에 해당하는 인덱스 값 증가
    }

    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < count.length; i++) { // 리스트에 기록된 정렬 정보 확인
        for (int j = 0; j < count[i]; j++) {
            result.add(i);
        }
    }
    return result;
}
```

- 시간복잡도는 $O(N+K)$이다.
- 공간복잡도는 $O(N+K)$이다.
- 현존하는 정렬 알고리즘 중에서는 기수 정렬과 더불어 가장 빠르다.

</details>
