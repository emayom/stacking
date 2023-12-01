# 정렬 알고리즘 (Sorting Algorithms)

> **정렬(Sorting) 📶**  
> 컬렉션(e.g. an array)의 항목을 재배열하는 과정

<br>

## 정렬 알고리즘의 종류 
1. [선택 정렬(Selection Sort)](./selection-sort.md)
1. [삽입 정렬(Insertion Sort)](./insertion-sort.md)
    ![Static Badge](https://img.shields.io/badge/stable%20sort-E9ECEF?style=flat-square)
1. 퀵 정렬(Quick Sort)
1. [합병 정렬(Merge Sort)](./merge-sort.md)
    ![Static Badge](https://img.shields.io/badge/stable%20sort-E9ECEF?style=flat-square)
1. 힙 정렬(Heap Sort)
1. 기수 정렬(Redix Sort (LSD))
1. 기수 정렬(Redix Sort (MSD))
1. std::sort (gcc)
1. std::stable_sort (gcc)
1. 셸 정렬(Shell Sort)
1. [버블 정렬(Bubble Sort)](./bubble-sort.md)
    ![Static Badge](https://img.shields.io/badge/stable%20sort-E9ECEF?style=flat-square)
1. 칵테일 정렬(Cocktail Shaker Sort)
1. 난쟁이 정렬(Gnome Sort)
1. 바이토닉 정렬(Bitonic Sort)
1. 보고 정렬(Bogo Sort)

<br>

## 치트 시트(Cheat Sheet)
| `Algorithm` | :thumbsup: `Best` | `Avg` | :thumbsdown: `Worst` | `Space Complexity` | `stable`| `in-place` |
| :--- | :----: | :----: | :----: | :----: | :----: | :----: |
| 선택 정렬(Selection Sort)   | O($n^2$) | O($n^2$) | O($n^2$) | O(1) | | :white_check_mark: |
| 삽입 정렬(Insertion Sort) | ||||||
| 퀵 정렬(Quick Sort) | ||||||
| 합병 정렬(Merge Sort) | O($n\\,log\\,n$) | O($n\\,log\\,n$) | O($n\\,log\\,n$) | O($n$) | :white_check_mark: | |
| 힙 정렬(Heap Sort) | ||||||
| 기수 정렬(Redix Sort (LSD))  | ||||||
| 기수 정렬(Redix Sort (MSD))  | ||||||
| std::sort (gcc) | ||||||
| std::stable_sort (gcc) | ||||||
| 셸 정렬(Shell Sort) | ||||||
| 버블 정렬(Bubble Sort) | O($n$) | O($n^2$) | O($n^2$) | O(1) | :white_check_mark: | :white_check_mark: |
| 칵테일 정렬(Cocktail Shaker Sort) | ||||||
| 난쟁이 정렬(Gnome Sort) | ||||||
| 바이토닉 정렬(Bitonic Sort) | ||||||
| 보고 정렬(Bogo Sort) | ||||||


<br>

## Array.prototype.sort()에 대해  

#### Point 1. 브라우저마다 구현된 알고리즘은 다를 수 있다. 
ECMAScript 명세에서는 `Array.prototype.sort()` 매서드에 대해 특정한 정렬 알고리즘에 대한 요구사항을 명시적으로 제공하지 않는다. 브라우저마다 구현된 알고리즘은 다를 수 있다. 

#### Point 2. `compareFn` 생략 시, 문자열 변환 과정을 거쳐 유니 코드 코드 포인트 값에 따라 정렬된다. 
자바스크립트의 내장 정렬 메서드 `sort` 사용 시 옵셔널 `compareFn`을 생략하게 되면, 
배열의 모든 항목이 문자열로 변환되고 각 문자의 유니 코드 코드 포인트 값에 따라 정렬된다. 

#### Point 3. 원본 배열이 변경된다. <sup>`in-place`</sup>
`Array.prototype.sort()` 매서드는 원본 배열을 직접 변경하도록 설계되었다.   

<br>

---
<br>

### Reference 
[15 Sorting Algorithms in 6 Minutes](https://www.youtube.com/watch?v=kPRA0W1kECg)  
[Sorting Algorithms Animations](https://www.toptal.com/developers/sorting-algorithms)
[VisuAlgo - Sorting](https://visualgo.net/en/sorting)
