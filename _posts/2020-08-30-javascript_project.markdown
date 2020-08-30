---
layout: post
title:      "JavaScript project"
date:       2020-08-30 21:54:39 +0000
permalink:  javascript_project
---


For my JavaScript project I built an app called choremates. This app allows you to organize house chores between everyone in the house. You can create a schedule with chores for everyone to contribute to the cleanliness of the house. The challenge I faced building this project was to keep my code organize and make it DRY. Since this is my first project with jacvascript, I was lost to how the code should look, but along the way I started to grasp what that should look like.

The secret is to keep your functions to as short as possible, and if you realize, that some code in a function is probably going to be useful elsewhere, write it as its own function. For example, in order to delete and update chores in the schedule, I would have to remove the chore from the cell permanently or remove it and put it elsewhere(for updating). I realozed that both in both functionalities the chores needed to be removed from the schedule, so I made a function for just that: 

```
deleteTableCell = () => {
    let oldDiv = document.getElementById(`table-cell-${this.id}`);
    oldDiv.remove();
}
```

Now we can just delete chores from the schedule, so to delete a chore I can use this function:

```
deleteAssgChore() {
    this.deleteTableCell();
    let card = document.getElementById(`outer-assg-chore-${this.id}`);
    card.remove();
}
```

and to update:

```
updateTableCell = (newDay, newMemId, newName) => {
    this.deleteTableCell();
    this.attachToTableCell(newDay, newMemId, newName);
}
```

In both functions I could have written the same code twice, but this way is more DRY, organized and even easier to read. Realizing that some code in a function could potentially be its own function is crucial to keeping your code organized and DRY.

