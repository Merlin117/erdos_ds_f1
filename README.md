# erdos_ds_f1
This is a repository for the F1 project of the Erdos summer 2025 Data Science bootcamp. Group members were: Carter Swift, Merlin Hart, Patrick Martin II, and Jaegeon Shin.
### Purpose
The purpose of this project was to create a model that can predict how exciting a Formula 1 race will be, as defined by how different the finishing order of the race is from the starting order.

### Interested Parties
- FIA, so they can see trends in how exciting a race is to watch and use that information to market to new audiences or make strategic changes to increase the excitment for viewers.
- F1 fans, so they can know what to expect of a race before it happens.
- People that haven't watched F1 before, so they can watch some of the more exciting races while still figuring out the nuances of the sport.

### The Math in our Model
We wanted to find a good way to quantify how exciting a race could be based off of how much the finishing grid changes from the starting grid of a race. To do this we came up with a metric called 'Average Local Position Change' (ALPC) determined by the following formula
$$ALPC=\frac{1}{N(N-1)}\sum_{i=1}^N\left |\sum_{\substack{j=1 \\ j\neq i}^N (i-j)-(\sigma^{-1}(i)-\sigma^{-1}(j))}\right |$$
where $N$ is the number of drivers and $\sigma$ is the permutation which represents the finishing positons of the racers. We chose this over an excitement metric like the total number of overtakes since there can exist uninteresting races which have the same number of overtakes as exciting ones. Consider the finishing positions $15234$ and $13524$. Both have the same number of overtakes, but the first one seems to be uninteresting since the only change from the starting grid $12345$ is the racer in 5th moving up to 2nd. 

For our features we had the 'Absolute Grid Delta' (AGD) and the 'Median Gap Time' (MGT) both utilizing what we called the 'Pace Rank Grid' for a race. To get the pace rank grid we ordered the racers by their fasted qualifying or free practice time. Let $\tau$ be the permutation of the starting grid which gets the pace rank grid, and let $t(i)$ be the time of racer $i$ in the pace rank grid. Then our features are determined by the following formulas:
$$AGD = \frac{1}{N}\sum_{i=1}^n|i-\tau(i)|$$
$$MGT = \text{median}(t(i+1)-t(i))_{0\leq i\leq N-1}.$$

### Results
With our chosen features our model was able to predict with an $r^2\approx 0.13$ which implies that our model has some predictive power. The $MSE\approx 0.86$ which isn't terrible since the ALPC of a given race can typically range between $0$ and $4$. We did notice, however, that there appeared to be a correlation between the number of DNFs in a race and the ALPC of a race as seen in the plot below: 
![image](https://github.com/user-attachments/assets/c8efc7e4-2db7-48f2-a70d-29f5b64f300d)

This was further confirmed when we changed the input data for our model to exclude racers who had a DNF in the race. The model was then able to garner better results with an $r^2\approx 0.18$ and a $MSE\approx 0.83$. 

### Repository Structure
The repository is organized as follows:

- The final model and processed features are in the `Final Model and Features` directory.
- Our executive summary and presentation slides are located in `Erdos Submission`
- `data_f1db` contains all of the raw data.
- `cleaned_data` contains cleaned datafiles in two versions, with one set having DNFs removed and the other preserving DNFs.
