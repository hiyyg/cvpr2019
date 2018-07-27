# CVPR2019 Project

## Repo Structure

Two other git repos are embedded within this repo (and slightly modified). They originally come 
from the repos <https://github.com/bearpaw/pytorch-pose> and 
<https://github.com/weigq/3d_pose_baseline_pytorch>. 

~~~~ 
README.md                                           readme
main.py                                             main entry point for training (scripts)
options.py                                          options to run code with
eval.py                                             entry point for evaluating predicitons (quantitive scores)
vis.py                                              entry point for visualizing results
twod_threed/                                        folder containing code for 2D pose to 3D pose (from: https://github.com/weigq/3d_pose_baseline_pytorch)
    ...
stacked_hourglass/                                  folder containing code for RGB to 2D pose estimation (from: 
    ...                                      
model_checkpoints/                                             folder where models will be saved
    ... (empty initially)
visualizations/                                     folder where visualizations will be saved
    ... (empty initially)                            
data/                                               folder to save data (including outputs from networks)
    ... (empty initially)
~~~~

N.B. we didn't write the code in the "twod_threed" and "stacked_hourglass" folders, so the overall "code consistency" is 
likely to be missing. All code outside of these folders was hopefully written in a consistent manor, and hopefully also 
somewhat documents the other repositories in how they are used.

## Changes made to the pre-existing repos
### Stacked Hourglass code
- Changes to parse_args options, for consistency

### 2D to 3D code
- Changes to parse_args options, for consistency

## Data

### MPII dataset
Download the images:
`wget https://datasets.d2.mpi-inf.mpg.de/andriluka14cvpr/mpii_human_pose_v1.tar.gz`

Soft link the data to `<REPO_DIR>/stacked_hourglass/data/mpii/images` using the command: `ln -s <MPII_DATA_DIR>/images <REPO_DIR>/stacked_hourglass/data/mpii/images`.


###Human3.6m 2D and 3D pose data
TODO

### Human3.6m Dataset
TODO

### TODO:
TODO: describe the process of downloading the data (incl downloading the 2D and 3D ground truths).

TODO: explain that it needs to be simlinked or copied into the `data` directory.

## Running the code

### Training Models
Models are trained using the following commands:

- `python main.py "hourglass"` Train a stacked hourglass network (RGB image > 2D pose)
    - Prereqs: MPII dataset downloaded as above
    - Default `--input_dir` specifies where the input images of MPII are (default: `./data/hourglass/images`)
    - Example usage (assuming that data has been setup as above) `python main.py hourglass --exp test`
- `python main.py "2d3d"` Train the "3D pose baseline model". (2D pose > 3D pose)
    - Prereqs: Human3.6m 2D and 3D pose data downloaded as above
    - Default `--input_dir` specifies where the 2D pose estimates input is (default: `./data/2d3d/train_2d.pth.tar`)
- `python main.py "stitched"` Train the "Stitched" model
    - `--load_hourglass` Specify a checkpoint to load the hourglass model from (if none specified, then we randomly initialize the network) 
    - `--load_2d3d` Specify a checkpoint to load the 2d3d model from (if none specified, then we randomly initialize the network)
    - `--load` Spefies a checkpoint for the **entire** stitched network to load from 
- The following are options that can be given to ANY of the above commands
    - `--exp` Provides an experiment id (string) (default: '0') 
    - `--input_dir` Specify an input dataset (default: depends on script above)
    - `--checkpoint_dir` Specify where model checkpoints are stored (default: `model_checkpoints`)
    - `--output_dir` Specify where to put the output (will be saved in a folder `<output_dir>/<script_<exp id>`)
    - `--load` Specify a checkpoint to load training from 


TODO: explain where models are saved and the file format

TODO: continue explaining params. For example, how to specify the checkpoints for each of the models in the 'stitched' model, and --lr. (Have one per **useful** option in options.py)
