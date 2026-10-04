# Dataset

The Sen1Floods11 dataset is not included in this repository because of its large file size.

## Downloading the dataset

The dataset was developed by Cloud to Street and the current v1.1 release is hosted in a public Google Cloud Storage bucket.

The official dataset repository and download instructions are available here:

https://github.com/cloudtostreet/Sen1Floods11

The complete v1.1 dataset is approximately 14 GB. The official repository provides the following command for downloading the dataset using `gsutil`:

```bash
gsutil -m rsync -r gs://sen1floods11 /YOUR/LOCAL/DIRECTORY/HERE
```

The official documentation for the dataset structure is also available here:

https://github.com/cloudtostreet/Sen1Floods11/blob/master/docs/README.md

## Required directory structure

After downloading and extracting the dataset, place the `Sen1Floods11_raw` directory inside this `Data` folder so that the repository has the following structure:

Data/
└── Sen1Floods11_raw/
└── v1.1/
└── data/

The notebooks in this project expect the dataset to be available at:

`Data/Sen1Floods11_raw/`

The project uses the hand-labelled Sentinel-1 data and associated JRC permanent-water data contained within the Sen1Floods11 v1.1 structure.

## Dataset citation

Please cite the original Sen1Floods11 publication when using the dataset:

Bonafilia, D., Tellman, B., Anderson, T. and Issenberg, E. (2020) 'Sen1Floods11: A georeferenced dataset to train and test deep learning flood algorithms for Sentinel-1', Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops, pp. 835–845.

The original publication and dataset citation information are provided in the official Cloud to Street repository.
