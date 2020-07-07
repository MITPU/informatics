---
layout: post
title:  "Нэгтгэн эрэмбэлэх - Merge Sort"
date:   2020-06-16 00:00:00 -0500
author: "Ууганболд"
category: "эрэмбэлэлт"
---
*Merge sort* бол энгийн, хэрэгжүүлэхэд хялбархан боловч маш хучирхэг эрэмбэлэлтийн алгоримт юм. Энэхүү алгоритм нь [Divide and Conquer][Divide and Conquer] аргачлал дээр суурилдаг буюу том өөгдлийг жижиг дэд хэсгүүдэд хуваагаад (divide), тэдгээр жижиг дэд хэсгүүдийг эрэмбэлсэний дараа буцаан нэгтгэх (conquer) байдлаар өгөгдлийг эрэмбэлдэг. 

Энэ алгоримт нь хоёр зүйлээр онцлог бөгөөд давуу талтай. 1. Хүлээгдэж буй хугацааны үнэлгээ нь хамгийн муу тохиолдолд O(n log n) буюу [Харьцуулах аргаар эрэмбэлэх](https://en.wikipedia.org/wiki/Comparison_sort) алгоримтын боломжит хамгийн сайн үнэлгээнд ажиллана. 2. Энэ алгоримт нь [тогтовортой эрэмбэлэлт](https://en.wikipedia.org/wiki/Sorting_algorithm#Stability) хийдэг буюу хамгийн ижил утгатай өгөгдлийн байрыг эрэмбэлэх үедээ алдагдуулдаггүй.

Энэхүү алгоримтын дутагдалтай тал нь ажиллахын тулд O(n) нэмэлт санах ой хэргэлдэг.

<center class="table-title">Хугацаа болон санах ойн үнэлгээ</center>

{:.time-space-complexity}
|                | Хугацаа         | Санах ой         |
|----------------|-----------------|------------------|
| Сайн нөхцөлд   | Ω(n log n)      | O(n)             |
| Дундаж нөхцөлд | Θ(n log n)      | O(n)             |
| Муу нөхцөлд    | O(n log n)      | O(n)             |


{% highlight java %}
public class MergeSort{

    public static void sort(int[] arr){
          sort(arr, 0, arr.length);
    }

    public static void sort(int[] arr, int low, int high){
        //1-ээс их урттай хэсгийг л эрэмбэлнэ.
        //1 урттай нь эрэмбэлэгдсэн гэсэн үг.
        if(low+1 < high){

            //divide хэсэг. 
            //массивийг хоёр тэнцүү хэсэгт хувааж тус бүрд нь эрэмбэлнэ.
            int mid = low+ (high-low)/2;
            sort(arr, low, mid);
            sort(arr, mid, high);

            //conquer хэсэг.
            //эрэмбэлэгдсэн дэд хэсгүүдийг нэгтгэнэ.
            merge(arr, low, mid, high);
        }
    }

    private static void merge(int[] arr, int low, int mid, int high){

        /*Нэмэлт санах ой ашиглан эрэмбэлэгдсэн дэд
        хэсгүүдийг хуулж байна.
        */
        int[] left=java.util.Arrays.copyOfRange(arr,low,mid);
        int[] right=java.util.Arrays.copyOfRange(arr,mid,high);

        /*
        Эрэмбэлэгдсэн дэд хэсгүүдээс алхам бүрд аль багыг нь сонгон авч
        буцаан эрэмбэлэх ёстой массив уруу хуулна.
        */
        int l=0;
        int r=0;
        while( l<left.length && r< right.length){
             if(left[l]< right[r]){
                 arr[low++]=left[l++];
             }else{
                 arr[low++]=right[r++];
             }
        }

        /*
        Өмнөх алхамд дуусгаагүй үлдэгдэл байвал түүнийг хуулна.
        */
        while(l<left.length){
            arr[low++]=left[l++];
        }

        while(r<right.length){
            arr[low++]=right[r++];
        }
    }
}

{% endhighlight %}

[Divide and Conquer]: https://en.wikipedia.org/wiki/Divide-and-conquer_algorithm
