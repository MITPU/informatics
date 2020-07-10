---
title:  "Хурдан эрэмбэлэх - Quick Sort"
date:   2019-12-10 00:00:00 -0500
author: Адъяа
category: "эрэмбэлэлт"
---
[Quicksort][Quicksort] бол [Divide and Conquer][Divide and Conquer] дээр суурилсан эрэмбэлэлтийн алгоритм юм.  Quicksort нь массиваас пивот цэг сонгон аваад массивийн элемэнтүүдийг тухайн пивот элемэнтээс их болон бага гэсэн 2 жижиг массивт хуваан дахин 2 жижиг массивыг энэхүү байдалаар эрэмбэлнэ. 

<center class="table-title">Хугацааны үнэлгээ</center>

{:.time-space-complexity}
|                | Хугацаа         |
|----------------|-----------------|
| Хамгийн шилдэг | O(n log n)      |
| Дундаж         | O(n log n)      |
| Хамгийн муу    | O(n^2)          |

{% highlight python %}

def partition(arr, low, high): 
    i = ( low-1 )         #жижиг элемэнтүүдийн индекс
    pivot = arr[high]     # пивот 
    for j in range(low , high): 
  
        # хэрэв одоо байгаа элемент пивот элементээс бага буюу тэнцүү үед
        if   arr[j] <= pivot: 
            i = i+1 
            arr[i],arr[j] = arr[j],arr[i] 
  
    arr[i+1],arr[high] = arr[high],arr[i+1] 
    return ( i+1 ) 
  
def quickSort(arr, low, high): 
    if low < high: 
        # pi пивот идекс 
        pi = partition(arr, low, high) 
 
        # пивот цэгээс өмнөх болон дараах (их, бага) дэд массивыг дахин эрэмбэлэх
        quickSort(arr, low, pi-1) 
        quickSort(arr, pi+1, high) 
{% endhighlight %}

## **Ашигласан материалууд:**
1. https://en.wikipedia.org/wiki/Quicksort
2. https://www.topcoder.com/community/competitive-programming/tutorials/sorting

[Quicksort]: https://en.wikipedia.org/wiki/Quicksort
[Divide and Conquer]: https://en.wikipedia.org/wiki/Divide-and-conquer_algorithm
