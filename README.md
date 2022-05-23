# dop_learning_db_wiki

| Groups | Description | Acces |
| ------ | ----------- | ----- |
| feature_map |	array of 0 and 1's denoting if a feature is present, zeros are only ever possible for feedback |"<fip_number>\feature_map\year-month-day" |
| psych_propc |	(8 by 3) matrix contain contrast, propertion correct and errors bar info |	"<fip_number>\psych_proc\year-month-day" |
| idx_stim_right | matrix containing indices for when the contrast appeared in terms of fluorsence rows|"<fip_number>\idx_stim_right\year-month-day" |
| idx_stim_left | same as above, but with info for this group (i.e. stim_left) | "<fip_number>\idx_stim_left\year-month-day" | 
| idx_act_right | same as above, but with info for this group | "<fip_number>\idx_act_right\year-month-day" | 
| idx_act_left | same as above, but with info for this group | "<fip_number>\idx_act_left\year-month-day" |
| idx_feed_right_correct |same as above, but with info for this group | "<fip_number>\idx_feed_right_correct\year-month-day" |
| idx_feed_left_correct |same as above, but with info for this group | "<fip_number>\idx_feed_right_correct\year-month-day" |
| idx_feed_right_incorrect |same as above, but with info for this group | "<fip_number>\idx_feed_right_incorrect\year-month-day" |
| idx_feed_left_incorrect |same as above, but with info for this group | "<fip_number>\idx_feed_left_incorrect\year-month-day" |
| X_stim_right | design matrix columns for group | "<fip_number>\X_stim_right\year-month-day" |
| X_stim_left | design matrix columns for group | "<fip_number>\X_stim_left\year-month-day" |
| X_act_right | design matrix columns for group | "<fip_number>\X_act_right\year-month-day" |
| X_act_left | design matrix columns for group | "<fip_number>\X_act_left\year-month-day" |
| X_feed_right_correct | design matrix columns for group | "<fip_number>\X_feed_right_correct\year-month-day" |
| X_feed_left_correct | design matrix columns for group | "<fip_number>\X_feed_left_correct\year-month-day" |
| X_feed_right_incorrect | design matrix columns for group | "<fip_number>\X_feed_right_incorrect\year-month-day" |
| X_feed_left_incorrect | design matrix columns for group | "<fip_number>\X_feed_left_incorrect\year-month-day" |
| wheel | matrix contain: times, wheel position (uncentered), stim position (centered), wheel velocity, wheel acceleration |
| task_features | matrix of rewards, choices, contrast shown on trial, ... | "<fip_number>\task_features\year-month-day" |
| task_times | matrix of times for task_features | "<fip_number>\task_times\year-month-day" |

## Python example
```python
import h5py
dblock = "\loc\to\db.hdf5"

# automate with a function
def read_data(db_loc, fip, grp, date):
     get_str = str(fip) + "/" + grp + "/" + date
     with h5py.File(db_location, "r") as f:
         data = f[get_str][:]
     return data
     
# example
animal = 29
group = "wheel"
date = "2022-04-22"
wheel_data = read_db(dblock, animal, group, date)
```

## Julia example

```julia
using HDF5
dblock = "/mnt/cup/labs/witten/yoel/julia/fip_db.hdf5"

# to make it consistent with python
function read_db(db_loc, fip, grp, date)
    get_str = string(fip, "/", grp, "/", date)
    return h5read(db_loc, get_str)
end

animal = 29
group = "wheel"
date = "2022-04-22"
wheel_data = read_db(dblock, animal, group, date)
```


## Matlab example
```matlab
wheel_data = h5read('\loc\to\db.hdf5','/29/wheel/2022-04-22')
```
