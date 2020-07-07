---
layout: post
title:  "Disjoint-set"
date:   2020-07-07 00:00:00 -0500
author: "Амар"
category: "Өгөгдлийн бүтэж"
comments: true
---
**Бодлого**

Өрөөнд $$N$$ хүн байгаа. Хоёр хүнийг шууд буюу шууд бус байдлаар холбогдсон тохиолдолд найз гэнэ.

Шууд бус байдлаар найз гэдэг нь

$$A$$ - $$B$$ хоёр ямар нэгэн байдлаар найз ( Шууд эсвэл шууд бус байдлаар найз )

$$B$$ - $$C$$ хоёр ямар нэгэн байдлаар найз ( Шууд эсвэл шууд бус байдлаар найз )

байвал $$A$$ - $$C$$ хоёр нь найз юм.

Тиймээс доорх хүсэлтүүдийг биелүүлдэг програм бичнэ үү.

**Оролт:**

Эхний мөр $$N$$ тоо - нийт хүний тоо

Хоёр дахЬ мөр $$Q$$ тоо -  нийт орж ирэх хүсэлтийн ( query ) тоо

Дараагийн $$Q$$ мөрөнд 2 төрлийн хүсэлтийн аль нэг нь нэгэн мөрөнд байрласан байна

 - Эхнийх нь `merge p1 p2` - Энэ нь `p1`, `p2` нь найз боллоо гэсэн үг

 - Дараах нь `is_friend p1 p2` - Энэ нь асуулт юм асуулт асуух тухайн агшинд `p1`, `p2` нь найзууд уу гэсэн асуулт юм

**Гаралт:**

`is_friend p1 p2` гэсэн бүтэцтэй хүсэтл бүрд

хэрэв `p1`, `p2` нь хоёр найз байх юм бол `"YES"` үгүй бол `"NO"` гэж хэвлэнэ

**Жишээ оролm:**
{% highlight python %}
5 # Нийт хүний тоо
4 # Нийт орж ирэх хүсэлтийн тоо
merge 1 2 # 1 2 Найз боллоо
is_friend 1 2 # 1 2 Найзууд уу?
is_friend 1 3 # 1 3 Найзууд уу?
merge 2 3 # 2 3 Найз боллоо
is_friend 1 3 # 1 3 Найзууд уу?
{% endhighlight %}

**Жишээ гаралт:**
{% highlight python %}
YES # 1 2 Найзууд уу?
NO # 1 3 Найзууд уу?
YES # 1 3 Найзууд уу? Description: (1,2) найзууд мөн (2,3) найзууд болсон учираас (1,3) нь найз юм
{% endhighlight %}


**Бодолт 1:**
{% highlight cpp %}

// Syntax алдаа байж болзошгүй :)
vector<int> parent;

void init(int n){
    parent.resize(n);
    for (int i=0; i<n; i++)
        parent[i] = i;
}

int find(int p1){
    if (parent[p1] != p1)
        parent[p1] = find(parent[p1]);
    return parent[p1];
}

void merge(int p1, int p2){
    p1 = find(p1);
    p2 = find(p2);
    parent[p1] = p2;
}

bool is_friend(int p1, int p2){
    return find(p1) == find(p2);
}
{% endhighlight %}

**Бодолт 2:**

Уг бодолт performance маш сайн бараг л шулуун хугацаанд ажилллана

{% highlight cpp %}

// Syntax алдаа байж болзошгүй :)

vector<int> rank, parent;

void init(int n){
    parent.resize(n);
    rank.resize(n);
    for (int i=0; i<n; i++){
        parent[i] = i;
        rank[i] = 1;
    }
}

int find(int p1){
    if (parent[p1] != p1)
        parent[p1] = find(parent[p1]);
    return parent[p1];
}

void merge(int p1, int p2){
    p1 = find(p1);
    p2 = find(p2);
    if ( rank[p1] > rank[p2] )
        parent[p2] = p1;
    else
        if ( rank[p2] > rank[p1] )
            parent[p1] = p2;
        else {
            parent[p1] = p2;
            rank[p2]++;
        }
}

bool is_friend(int p1, int p2){
    return find(p1) == find(p2);
}
{% endhighlight %}


**Бодож болох бодлогууд**

- [[ Spoj ] - Herding](http://www.spoj.com/problems/HERDING/){:target="blank"}


- [[ Hackerrank ] - Merge Communities](https://www.hackerrank.com/challenges/merging-communities){:target="blank"}
- [[ Hackerrank ] - Components in a graph](https://www.hackerrank.com/challenges/components-in-graph){:target="blank"}
- [[ Hackerrank ] - Kundu and Tree](https://www.hackerrank.com/challenges/kundu-and-tree){:target="blank"}

**Холбоос**:

- [Topcoder - Disjoint-set data structures](https://www.topcoder.com/community/data-science/data-science-tutorials/disjoint-set-data-structures/){:target="blank"}
- [Wikipedia - Disjoint-set data structure](https://en.wikipedia.org/wiki/Disjoint-set_data_structure){:target="blank"}
