# dop_learning_db_wiki

| Groups | Description | Acces | name |
| :----: | :--------------------------------------------------------------: | :---: |
| col_names |	single array of strings , column names of the design matrix |	"names" |
| design_matrix |	datasets of design matrices for all animals. One dataset per sessions, per animal |	"fip_#_day_#" |
| fluo_data_nac_dms_dls | datasets of fluo data size: (fluo_samples_in_session,  3). One dataset per session, per animal |	"fip_#_day_#" |


```python
import h5py
dblock = "/mnt/cup/labs/witten/yoel/julia/fip_db.hdf5"

# read in the database
f = h5py.File(dblock, "r")

# get the keys of the dataset groups
f.keys() # these will be things like "design_matrix" below

# get design matrix for a particular day, for a particular animal
design_mat = f["design_matrix"].get("fip_16_day_9")[:]

# get fluo data for a particular day, for a particular animal
fluo = ["fluo_data_nac_dms_dls"].get("fip_16_day_9")[:]
```
