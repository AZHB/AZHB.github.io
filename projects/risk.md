---
layout: default
permalink: "/projects/risk/"
title: "A Game of Risk"
---

<h1> A Game of Risk" </h1>

Checking if code blocks works:

```
function test() {
  console.log("notice the blank line before this function?");
}
```

<h2> Algorithm Overview </h2>

Monte carlo method
psuedocode

<h2> Code Breakdown </h2>

<p> Generating Dice Rolls</p>

```C++
//Generate random dice rolls
vector<int> aRolls(aDice);
vector<int> dRolls(dDice);
for(vector<int>::iterator it=aRolls.begin();it!=aRolls.end();it++){
	*it = rand() % 6 + 1;
}
for(vector<int>::iterator it=dRolls.begin();it!=dRolls.end();it++){
	*it =rand() % 6 + 1;
}

//Sort random dice rolls for comparison
sort(aRolls.begin(),aRolls.end());
reverse(aRolls.begin(),aRolls.end());
sort(dRolls.begin(),dRolls.end());
reverse(dRolls.begin(),dRolls.end());
```

<p>Calculating result</p>

<h2> Running Time Analysis </h2>

