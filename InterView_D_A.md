# InterViewProject_자료구조 & 알고리즘

* 자료구조란 무엇인가?
    * 데이터를 효율적으로 저장하기 위한 방법
    
* 알고리즘이란 무엇인가?
    * 어떤 문제를 해결하기위한 방식 및 절차
    
* 배열이란 무엇인가?
    * 개념 : 인덱스를 기반으로 자료를 순서대로 저장하는 방식
    * 장점 : 인덱스를 기반으로 접근하기 때문에 접근이 빠르다.
    * 단점 : 삭제, 삽입 시 쉬프트 로직이 들어간다.
    
* 버블정렬이란 무엇인가?
    * 데이터를 2개씩 비교하면서 정렬하는 간단한 정렬 알고리즘

    ``` swift
    func bubbleSort(num: [Int]) -> [Int] {
        var rect = num
        for i in 0..<(rect.count - 1) {
            for j in 0..<rect.count - 1 {
                if rect[j] > rect[j+1] {
                    rect.swapAt(j, j+1)
                }
            }
        }
        return rect
    }
    ```
