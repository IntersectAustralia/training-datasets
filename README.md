# Training Datasets

This is the collection of datasets used within the training courses delivered by
intersect.

The links to download the latest version of the datasets are;

- [intersect_training](https://github.com/IntersectAustralia/training-datasets/releases/latest/download/intersect_training_data.zip)

## Updating Datasets

There are two sets of releases that will automatically take place.
Upon updating the `master` branch,
the Master release will be updated.
The Master release is a pre-release and so doesn't modify the latest release,
providing a method of testing changes.

The creation of a new release,
which will update the data downloaded by participants
can be done in one of two ways.

1. Using the git command line interface, create a tag `git tag -a v0.1.7` and push the
   tag to GitHub ensuring the use of the `--tags` flag, `git push --tags`.
2. Using the GitHub web interface, create a [new release](https://github.com/IntersectAustralia/training-datasets/releases/new)
   setting the name of the new tag and the rest of the information.


## Adding new datasets

New datasets can be added to the repository with some minor changes.
This would involve creating a new directory alongside the `intersect_training`
directory that contains the new dataset.
With this dataset added, the next step is the automation,
which is found in the files
`.github/workflows/draft.yml` and
`.github/workflows/release.yml`.

There are two changes that need to be made to each of these files.
Firstly a new compression step needs to be added
```yaml
      - name: Compress Directories
        uses: montudor/action-zip@v0.1.0
        with:
          args: zip -qq -r new_directory.zip ./new_directory
```
which has to come before the Create Release step.
The final step is to add the name used for the zip file,
here `new_directory.zip` to the end of the files key in the Create Release step giving
```yaml
files: >
    intersect_training_data.zip
    new_directory.zip
```
