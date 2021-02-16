---
layout: default
permalink: "/projects/risk/"
title: "A Game of Risk"
---

<h1> A Game of Risk </h1>

This project showcases a C++ implementation of an algorithm that simulates the probability of victory in any given battle in the board game Risk. The algorithm is based on a Monte-Carlo approach, involving the efficient simulation of thousands of rounds by emulating dice rolls using repeated random draws from a probability distribution. An accurate result is calculated efficiently and almost instantaneously even for battles with thousands of dice rolls. The resulting console application was swiftly (and rightfully) banned by friends and family!

<table style="margin-left:auto;margin-right:auto">
	<tr>
	<td> <img src="https://azhb.github.io/websiteRisk.jpg" alt="Risk" width="460"><img src="https://azhb.github.io/websiteRiskBoard.jpg" alt="Risk" width="460"> </td> 
	<td> <img src="https://azhb.github.io/websiteRiskC++.PNG" alt="Risk" width="508"> </td>
	</tr>
</table>

<h2> The Rules </h2>

To provide some context on the inner workings of the algorithm, it is useful to briefly outline <a href="https://www.hasbro.com/common/instruct/risk.pdf"> the rules </a> that determine the victor in a battle in Risk. In a battle, there are *a* attacking units and *d* defending units. Battles consist of a number of rounds, until one player has no units left (or the attacker decides to stop). The possible outcomes of a round are below:

<table style="float:right">
	<tr>
		<td style="text-align:center"> <h3> Outcomes </h3> </td>
	</tr>
	<tr>
		<td style="text-align:center"> Defender loses one unit </td>
	</tr>
	<tr>
		<td style="text-align:center"> Defender loses two units </td>
	</tr>
	<tr>
		<td style="text-align:center"> Attacker loses one unit </td>
	</tr>
	<tr>
		<td style="text-align:center"> Attacker loses two units </td>
	</tr>
	<tr>
		<td style="text-align:center"> Attacker loses one unit and defender loses one unit </td>
	</tr>
</table>

In a single round, the attacking player rolls a maximum of *3* dice and the defender rolls a maximum of *2* dice. The highest dice roll of each player is compared, and then the second highest and so on. If the dice roll of the attacking player is greater than the defender's, then the defender loses a unit. If the dice roll of the attacking player is less than or equal to the defender's, then the attacker loses a unit. Below are some examples to demonstrate this from the official rules:

<div class="center">
<table>
	<tr>
	<td> <img src="https://azhb.github.io/websiteRiskExamples.PNG" alt="Risk examples" width="791px"> </td>
	</tr>
</table>
</div>

Once a round has been resolved, the next round begins and new dice are cast (assuming that both players still have units left!). The attacking player can choose to stop after any round, but for our algorithm it will be assumed that the attacking player fights to the last!

<h2> Algorithm Overview </h2>

Monte carlo method
psuedocode

<h2> Code Breakdown </h2>

<p> Generating Dice Rolls</p>

```cpp
//Generate random dice rolls
vector<int> aRolls(aDice);
vector<int> dRolls(dDice);
for(vector<int>::iterator it=aRolls.begin();it!=aRolls.end();it++){
	*it = rand() % 6 + 1;
}
for(vector<int>::iterator it=dRolls.begin();it!=dRolls.end();it++){
	*it =rand() % 6 + 1;
}
```

<p> Sorting Dice Rolls </p>

```cpp
//Sort random dice rolls for comparison
sort(aRolls.begin(),aRolls.end());
reverse(aRolls.begin(),aRolls.end());
sort(dRolls.begin(),dRolls.end());
reverse(dRolls.begin(),dRolls.end());
```

<p>Calculating result</p>

```cpp
//Calculate damage to attacker and defender
int battles = min(aRolls.size(),dRolls.size());
for(int i=0;i!=battles;i++){
	if(aRolls[i]>dRolls[i]){
		dCopy--;
	}
	else{
		aCopy--;
	}	
}
```

<h2> Running Time Analysis </h2>

Do some big-O analysis here perhaps?
