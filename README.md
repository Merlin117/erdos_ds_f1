# erdos_ds_f1
This is a repository for the F1 project of the Erdos summer 2025 Data Science bootcamp. Group members were: Carter Swift, Merlin Hart, Patrick Martin II, and Jaegeon Shin.
### Purpose
- The purpose of this project was to create a model that can predict how exciting a Formula 1 race will be, as defined by how different the finishing order of the race is from the starting order.

### Interested Parties
- FIA, so they can see trends in how exciting a race is to watch and use that information to market to new audiences or make strategic changes to increase the excitment for viewers.
- F1 fans, so they can know what to expect of a race before it happens.
- People that haven't watched F1 before, so they can watch some of the more exciting races while still figuring out the nuances of the sport.

### Results
With our chosen features out model was able to predict with an $r^2\approx 0.13$ which implies that our model has some predictive power. The $MSE\approx 0.86$ which isn't terrible since the ALPC of a given race can typically range between $0$ and $4$. We did notice, however, that there appeared to be a correlation between the number of DNFs in a race and the ALPC of a race as seen in the plot below: 
![image](https://github.com/user-attachments/assets/c8efc7e4-2db7-48f2-a70d-29f5b64f300d)
This was further confirmed when we changed the input data for our model to exclude racers who had a DNF in the race. The model was then able to garner better results with an $r^2\approx 0.18$ and a $MSE\approx 0.83$. 

### Repository Structure
The repository is organized as follows:

- The final model and processed features are in the `Final Model and Features` directory.
- Our executive summary and presentation slides are located in `Erdos Submission`
- `data_f1db` contains all of the raw data.
- `cleaned_data` contains cleaned datafiles in two versions, with one set having DNFs removed and the other preserving DNFs.
