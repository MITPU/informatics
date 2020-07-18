---
title:  "Хоёртын Мод - Binary Tree"
date:   2020-07-18 00:00:00 -0500
author: "Батцогт"
category: "Өгөгдлийн бүтэц"
---
Хоёртын мод нь шугаман бус (non-linear) өгөгдлийн бүтцийн нэг төрөл бөгөөд элемент бүр нь хамгийн ихдээ баруун зүүн гэсэн хоёр мөчиртэй (элементтэй) мод юм.

<img width="250" alt="image1" src="https://user-images.githubusercontent.com/8675691/87855583-5bb7e380-c8e7-11ea-87c3-bd01236a1287.png">

Дээрх зураг дээр 9 элементтэй 3-ын өндөртэй, үндэс элемент нь 2 гэсэн утгатай, тэнцвэргүй (unbalanced), эрэмбэлэгдээгүй хоёртын модны жишээ харагдаж байна.

Хоёртын модны элемент бүр нь дараах үндсэн хэсгүүдээс бүрдэнэ:
1. Өгөгдөл (утга)
2. Зүүн мөчрийн заагч
3. Баруун мөчрийн заагч

**Хэрэглээ:**

Хоёртын мод нь дараах 2 өөр зүйлд ашиглагддаг:

1. Хоёртын хайлтын мод, хоёртын овоолго (binary heaps) зэргийг бүтээх болон модны элементүүдээр янз бүрийн аргаар гүйх замаар үр дүнтэй хайлт, эрэмбэлэлт зэрэгт ашиглагддаг.
2. Хоорондоо салшгүй уялдаатай салаалсан бүтэц бүхий өгөгдлийг илэрхийлэхэд ашиглагдана. Өөрөөр хэлбэл тухайн модны элементүүдийн өрөлт нь нэгэн цогц мэдээллийг илэрхийлэх бөгөөд баруун зүүн аль нэг элементийн утгыг өөрчлөхөд тухайн мэдээний цогц утга өөрчлөгддөг. Нийтлэг жишээ дурдвал Хаффман кодчлол ба кладограм (Huffman coding and cladograms) юм.


**Java дээрх хоёртын модны код:**

Доорх жишээн дээр энгийн хоёртын хайлтын модны класс байгаа бөгөөд элемент хайх (lookup()), элемент нэмэх (insert()) функцуудыг агуулсан.

{% highlight java %}
// BinaryTree.java
public class BinaryTree {
  //Үндэс элементийн заагч. Хоосон мод байх үед null байна.
  private Node root;
 
  /*
   --Node--
   Элемент бүр өгөгдөл, зүүн болон баруун мөчир лүү
   заах заагчийг агуулна. Заагчид null байж болно.
  */
  private static class Node {
    Node left;
    Node right;
    int data;

    Node(int newData) {
      left = null;
      right = null;
      data = newData;
    }
  }

  /**
   Хоосон хоёртын мод үүсгэх функц.
  */
  public void BinaryTree() {
    root = null;
  }
 

  /**
   Өгөгдлийг хайх рекурсив функцыг дуудах туслах функц.
  */
  public boolean lookup(int data) {
    return(lookup(root, data));
  }
 

  /**
   Өгөгдлийг хайх рекурсив функц.
  */
  private boolean lookup(Node node, int data) {
    if (node==null) {
      return(false);
    }

    if (data==node.data) {
      return(true);
    }
    else if (data<node.data) {
      return(lookup(node.left, data));
    }
    else {
      return(lookup(node.right, data));
    }
  }
 

  /**
   Өгөгдлийг хоёртын модонд нэмэх рекурсив функцыг дуудах туслах функц.
  */
  public void insert(int data) {
    root = insert(root, data);
  }
 

  /**
   Өгөгдлийг хоёртын модонд нэмэх рекурсив функц.
  */
  private Node insert(Node node, int data) {
    if (node==null) {
      node = new Node(data);
    }
    else {
      if (data <= node.data) {
        node.left = insert(node.left, data);
      }
      else {
        node.right = insert(node.right, data);
      }
    }

    return(node);
  }
 }
{% endhighlight %}

**Ашигласан материалууд:**
1. http://cslibrary.stanford.edu/110/BinaryTrees.html#java
2. https://en.wikipedia.org/wiki/Binary_tree
3. https://www.geeksforgeeks.org/binary-tree-data-structure
4. https://www.w3schools.in/data-structures-tutorial/binary-trees
