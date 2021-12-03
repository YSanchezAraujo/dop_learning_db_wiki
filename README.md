# dop_learning_db_wiki

| Groups | Description | Acces |
| ------ | ----------- | ----- |
| col_names |	single array of strings , column names of the design matrix |	"names" |
| design_matrix |	datasets of design matrices for all animals. One dataset per sessions, per animal |	"fip\_#\_day\_#" |
| fluo_data_nac_dms_dls | datasets of fluo data size: (fluo_samples_in_session,  3). One dataset per session, per animal |	"fip\_#\_day\_#" |
| idx_stim_act | indices to index fluo_data_nac_dms_dls, columns correspond to events during task, values of 1 should be ignored| "fip\_#\_day\_#" | 
| idx_feed | indices to index fluo_data_nac_dms_dls, columns correspond to events during task, values of 1 should be ignored| "fip\_#\_day\_#" | 

## Python example
```python
import h5py
dblock = "/mnt/cup/labs/witten/yoel/julia/fip_db.hdf5"

# read in the database
f = h5py.File(dblock, "r")

# get the keys of the dataset groups
f.keys() # these will be things like "design_matrix" below, these will the Groups in the table above

# get design matrix for a particular day, for a particular animal
design_mat = f["design_matrix"].get("fip_16_day_9")[:]

# get fluo data for a particular day, for a particular animal
fluo = ["fluo_data_nac_dms_dls"].get("fip_16_day_9")[:]

# if reading data with h5py.File remember to close it, as others wont be able to access an open database
f.close()

# an alternative is to use with:
with h5py.File(dblock, "r") as f:
    design_mat = f["design_matrix"].get("fip_16_day_9")[:]
    
# automate with a function
def read_data(db_location, group_name, fip_number, day_number):
     get_str = "fip_" + str(fip_number) + "_day_" + str(day_number)
     with h5py.File(db_location, "r") as f:
         data = f[group_name].get(get_str)[:]
     return data
     
# example
design_mat = read_data(dblock, "design_matrix", 13, 1)
fluo = read_data(dblock, "fluo_data_nac_dms_dls", 13, 1)
   
```

## Julia example

```julia
using HDF5
dblock = "/mnt/cup/labs/witten/yoel/julia/fip_db.hdf5"

# manually opening and closing
f = h5open(dblock, "r")
fluo_group = f["fluo_data_nac_dms_dls"]
fluo = read(fluo_group["fip_13_day_1"])
close(f)

# as with python this bypasses the need to manually open and close
fluo = h5read(dblock, "fluo_data_nac_dms_dls/fip_13_day_1")

# to make it consistent with python
function read_data(db_location, group_name, fip_number, day_number)
    get_str = string("fip_", fip_number, "_day_", day_number)
    get_str = string(group_name, "/", get_str)
    return h5read(db_location, get_str)
end

fluo = read_data(dblock, "fluo_data_nac_dms_dls", 13, 1)
```
