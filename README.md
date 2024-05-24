# quicksort_practice
# 目的
在不使用python內建的 sort 語法的情形下，以「quicksort.ipynb」將陣列「33, 67, 8, 13, 54, 119, 3, 84, 25, 41」進行quicksort，並在排序過程中印出排序步驟，以呈現quicksort的排序原理。

# 執行結果
>Initial array: [33, 67, 8, 13, 54, 119, 3, 84, 25, 41] <br>
Using pivot 33 at index 0 <br>
Swapped 25 and 67: [33, 25, 8, 13, 54, 119, 3, 84, 67, 41] <br>
Swapped 3 and 54: [33, 25, 8, 13, 3, 119, 54, 84, 67, 41] <br>
Swapped pivot 3 with 33: [3, 25, 8, 13, 33, 119, 54, 84, 67, 41] <br>
Pivot is now at index 4: [3, 25, 8, 13, 33, 119, 54, 84, 67, 41] <br>
Using pivot 3 at index 0 <br>
Swapped pivot 3 with 3: [3, 25, 8, 13, 33, 119, 54, 84, 67, 41] <br>
Pivot is now at index 0: [3, 25, 8, 13, 33, 119, 54, 84, 67, 41] <br>
Using pivot 25 at index 1 <br>
Swapped pivot 13 with 25: [3, 13, 8, 25, 33, 119, 54, 84, 67, 41] <br>
Pivot is now at index 3: [3, 13, 8, 25, 33, 119, 54, 84, 67, 41] <br>
Using pivot 13 at index 1 <br>
Swapped pivot 8 with 13: [3, 8, 13, 25, 33, 119, 54, 84, 67, 41] <br>
Pivot is now at index 2: [3, 8, 13, 25, 33, 119, 54, 84, 67, 41] <br>
Using pivot 119 at index 5 <br>
Swapped pivot 41 with 119: [3, 8, 13, 25, 33, 41, 54, 84, 67, 119] <br>
Pivot is now at index 9: [3, 8, 13, 25, 33, 41, 54, 84, 67, 119] <br>
Using pivot 41 at index 5 <br>
Swapped pivot 41 with 41: [3, 8, 13, 25, 33, 41, 54, 84, 67, 119] <br>
Pivot is now at index 5: [3, 8, 13, 25, 33, 41, 54, 84, 67, 119] <br>
Using pivot 54 at index 6 <br>
Swapped pivot 54 with 54: [3, 8, 13, 25, 33, 41, 54, 84, 67, 119] <br>
Pivot is now at index 6: [3, 8, 13, 25, 33, 41, 54, 84, 67, 119] <br>
Using pivot 84 at index 7 <br>
Swapped pivot 67 with 84: [3, 8, 13, 25, 33, 41, 54, 67, 84, 119] <br>
Pivot is now at index 8: [3, 8, 13, 25, 33, 41, 54, 67, 84, 119] <br>
Sorted array: [3, 8, 13, 25, 33, 41, 54, 67, 84, 119] <br>

# 程式碼
## quicksort 函數
這是主要的快速排序函數，使用遞迴來處理子陣列。它首先調用 partition 函數來劃分陣列，然後對劃分出的子陣列進行排序。
```
def quicksort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)
        print(f"Pivot is now at index {pi}: {arr}")
        quicksort(arr, low, pi-1)
        quicksort(arr, pi+1, high)
```

## partition 函數
這個函數使用陣列的最開始元素作為基準點（樞紐元），並進行劃分。函數會不斷地從兩邊掃描陣列，將小於基準點的元素移到左邊，大於基準點的元素移到右邊，最後將基準點移到正確的位置。
```
def partition(arr, low, high):
    pivot = arr[low]  # 使用陣列最開始的元素為基準點
    print(f"Using pivot {pivot} at index {low}")
    left = low + 1
    right = high
    
    done = False
    while not done:
        while left <= right and arr[left] <= pivot:
            left = left + 1
        while arr[right] >= pivot and right >= left:
            right = right - 1
        if right < left:
            done = True
        else:
            arr[left], arr[right] = arr[right], arr[left]
            print(f"Swapped {arr[left]} and {arr[right]}: {arr}")
    
    arr[low], arr[right] = arr[right], arr[low]
    print(f"Swapped pivot {arr[low]} with {arr[right]}: {arr}")
    
    return right
```
## 主程式
定義了一個要排序的陣列，並呼叫 quicksort 函數來排序陣列。
在每次劃分陣列時，程式會印出當前陣列的狀態及基準點的位置，這樣可以清楚地看到排序過程中的每一步。運行此程式後，您將會看到排序過程中的所有步驟，最後輸出已排序的陣列。
```
arr = [33, 67, 8, 13, 54, 119, 3, 84, 25, 41]
print(f"Initial array: {arr}")
quicksort(arr, 0, len(arr) - 1)
print(f"Sorted array: {arr}")
```
