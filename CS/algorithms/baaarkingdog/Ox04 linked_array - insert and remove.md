# before watching explaining video

### preset code
```java
#include <bits/stdc++.h>
using namespace std;

const int MX = 1000005;
int dat[MX], pre[MX], nxt[MX];
int unused = 1;

void traverse(){
  int cur = nxt[0];
 
  while(cur != -1){
    cout << dat[cur] << ' ';
    cur = nxt[cur];
  }
  cout << "\n\n";
}
```

### trying before explaining
```java
void insert(int addr, int num){
  //first we got address so i need to know about the dat at addr
  int theVal = dat[addr];
  //and i need to add new value 'num's previous addr then need to know about pre[addr]
  int prevAddr = pre[addr]
  //actually what i need are
  // just set new number in dat[unused] and
  // give pre[addr] to pre[unused] and give unused to pre[addr]
  // give nxt[addr] to next[unused] and unused to nxt[addr]
  // don't need to know theValue;
  // so ignore code above

  //set value
  dat[unused] = num;
  //set prev
  pre[unused] = pre[addr];
  pre[addr] = unused;
  //set nxt
  nxt[unused] = nxt[addr];
  nxt[addr] = unused;
  //increase unused;
  unused ++;
}

void erase(int addr){
  //then probably erase is same way
  //let's think .. 
  //i need to set all of array's value in index (addr) to -1
  //before do that i need to set previous data's next address as next data's address and next data's previous address as next data's address
  
  //set previous data's next address
  nxt[pre[addr]] = pre[nxt[addr]];
  //set next data's prev address
  pre[nxt[addr]] = nxt[pre[addr]];
  unused --;
}
```

### The answer
```java
void insert(int addr, int num){
  data[unused]= num;
  pre[unused] = addr;
  nxt[unused] = nxt[addr] 
  if(nxt[addr] != -1) pre[nxt[addr]] = unused;
  nxt[addr] = unused;
  unused++;
}
```

i had wrong answer let's compare with the answer
```java
//first make code easy to compare
//my code
void insert(int addr, int num){
  data[unused] = num;
  pre[unused] = pre[addr];
  nxt[unused] = nxt[addr];

  pre[addr] = unused;
  nxt[addr] = unused;
  used ++;
}
```
