# Autism Image Classification

Can a computer tell photos of autistic and non-autistic children apart using only the area around their eyes? This project trains a model on photos labeled as autistic or non-autistic and tests how well it predicts those labels on photos it has not seen before.

The broader question is whether patterns in photos could one day complement developmental screening and help identify children who might benefit from a professional evaluation. That would require independent clinical studies. This model was trained on photos of children, not adults, and has not been validated for screening or diagnosis. If you have concerns about a child’s development, [talk with their pediatrician about developmental screening](https://www.cdc.gov/autism/diagnosis/) regardless of what the model predicts.

## Try the model on one photo

You don’t need to know Python or install anything on your computer. The project runs in **Google Colab**, a website that runs code in your browser. A **notebook** is a page with instructions and blocks of code called **cells**. To run a cell, click the ▶ button on its left. You don’t need to edit the code. The cell numbers below refer to the labels **inside the notebook**.

### Download two files

Open each file page below and click **Download raw file** (the download arrow above the file preview).

- [Colab notebook: `Autism_Image_Classification.ipynb`](Autism_Image_Classification.ipynb)
- [Project ZIP: `autism-image-classification.zip`](autism-image-classification.zip)

Keep the project ZIP zipped. You do not need Git or the repository’s **Code → Download ZIP** option.

### Open the notebook in Google Colab

Open [Google Colab](https://colab.research.google.com/). If you’re not already signed in, sign in with your Google account first. Then click **Upload notebook** at the top of the page and choose `Autism_Image_Classification.ipynb`, not the ZIP.

### Load the project and set up Colab

Run **Cell 1** by clicking ▶. When prompted, upload `autism-image-classification.zip`.

Once the project loads, run **Cell 2** and wait for the green check. A spinning circle means the cell is still running. You can skip **Cells 3 and 4** for this first run.

### Try a photo

Go to **Cell 5**, leave **Saved project model** selected, and run the cell. Choose a photo you have permission to upload. The photo should show **one child only**, with their **whole face visible**. Both eyes should be open, with no glasses or hair covering them. The child does not need to face the camera directly. If the photo includes other people, crop them out first. Keep the child’s whole face visible and let the program crop around the eyes.

### View the result

**Cell 5** shows how many photos the model could score and how many it labeled autistic. If you uploaded one photo and it was scored, **1 positive** means the model predicted autistic and **0 positives** means it predicted non-autistic. If it says **0 photos scored**, the model did not make a prediction. Try a clearer photo that meets the guidelines above.

To see the individual result in a spreadsheet, go to **Cell 7**, select **Predictions CSV**, check the download box, and run the cell. A **CSV** is a file you can open in a spreadsheet app such as Excel.

## Try several photos at once

In **Cell 5**, choose **Individual photos** or **ZIP of a photo folder**. If you only have a few photos, open the folder in the file picker and select them together. Use the same photo guidelines as above. The model scores each usable photo separately, and **Predictions CSV** has one row per photo scored. Cell 5 also tells you how many photos it could not score.

If you want to use the Bayesian calculator to explore results for one child, run Cell 5 with photos of **that child only**. Run a separate batch for each child. Different photos may add information that a single photo misses, especially if the expression, angle, or lighting changes. Near-identical shots can repeat the same mistake, so more photos don’t necessarily make the prediction more reliable. This project tests accuracy on individual photos; it does not establish how much, if at all, using several photos improves accuracy for one child.

## See how well the model performs

Run **Cell 4** with **Saved project model** selected. No upload is needed. Cell 4 uses the included **test set**, a separate group of labeled photos that the model did not learn from. These photos were also not used to choose which version of the model to keep.

- **Accuracy:** the percentage of test photos the model classified correctly.
- **Sensitivity:** of the test photos labeled autistic, the percentage the model classified as autistic.
- **Specificity:** of the test photos labeled non-autistic, the percentage the model classified as non-autistic.
- **Confusion matrix:** a table made from the test photos only. For each dataset label, it counts how many test photos the model labeled autistic and how many it labeled non-autistic. This shows both what the model got right and what it got wrong on photos that were not used for training.

Cell 4 can also show a **pixel-sensitivity heatmap**. It highlights parts of the eye crop where small changes in brightness tend to affect the model’s score most. It does not show which features cause autism.

To save the evaluation results, go to **Cell 7** and select **Model analysis (ZIP)**.

## Train a new model (optional)

The project already includes a trained model. To train your own, go to **Cell 3**, check the retraining box, and run the cell. Retraining uses the cropped Training and Validation images included in the project ZIP. You don’t need to upload any data.

You can use the same settings as the included model or change them before running the cell:

- **PCA components (`PCA_COMPONENTS`, default: 17):** how many image patterns the model uses to represent each eye crop. PCA is short for **principal component analysis**.
- **Hidden-layer neurons (`HIDDEN_NEURONS`, default: 60):** how many units the neural network uses to combine those inputs.
- **Maximum epochs (`MAXIMUM_EPOCHS`, default: 400):** the maximum number of passes through the training data. One pass is called an epoch.
- **Patience (`PATIENCE`, default: 50):** how many epochs to wait without improvement on the validation set before stopping early. If validation loss (a measure of prediction error) improves, the count starts over. Training keeps the version with the lowest validation loss.

The **training set** is what the model learns from. The **validation set** helps choose which version of the model to keep. The **test set** is used afterward to measure performance. Cell 4 always uses the same included test set.

When training finishes, choose **Retrained in this runtime** in Cell 4 to evaluate the new model or in Cell 5 to try it on photos. A **runtime** is the temporary Colab session that runs the notebook. Use Cell 7 to download the new model before ending that session.

## Try the Bayesian calculator (optional)

Run **Cell 6** to open the calculator. It shows how the calculated probability changes with the number of photos scored, the number of positive predictions, and the **base rate**, which is the assumed share of the population that is autistic.

- **Saved project model:** The calculator uses the confusion matrix included with the project. You can skip Cell 4.
- **Retrained in this runtime:** First run **Cell 4** with **Retrained in this runtime** selected. The calculator uses that model’s test results. If you train another model, run Cell 4 again.

If Cell 5 scored photos using the model you select, the calculator starts with those counts. Otherwise, it starts with **12 positives out of 20 photos**. You can edit both counts. Click **Run calculation**, then use **Cell 7** to download the results.

The calculator assumes that, for a given true label, one prediction does not tell you anything about the others. Photos of the same child can lead to similar mistakes, so the calculator can make the combined result look more certain than the evidence supports. Treat the output as an example of the calculation, not a personal probability or a diagnosis.

## Find the data

The cropped datasets are inside the project ZIP, not separate downloads on GitHub. If you want to browse them, extract the project ZIP and look in the `data/` folder. You do not need to extract them to run the notebook.

- **Processed eye images:** Open `data/processed-eye-strips.zip` inside the extracted project folder. It contains the processed Training, Validation, and Test images.
- **Original photos:** On the [Mendeley dataset page](https://data.mendeley.com/datasets/nfcv6x8n7h/1), choose **Download All**.
- **Test set used in Cell 4:** The separate `data/evaluation/test-eye-strips.zip` contains the same test images as the processed archive. You don’t need to extract it to run the notebook.

### Reproducing the preprocessing

Start with the original ZIP from the [Mendeley dataset page](https://data.mendeley.com/datasets/nfcv6x8n7h/1). Keep the original Training, Validation, and Test splits and their class folders separate. The project ZIP contains the preprocessing code in `scripts/crop.py`. The script locates the eyes, rotates and scales the image to align them, and saves a **128 × 20 pixel grayscale eye strip**. Photos with glasses, closed or nearly closed eyes, or insufficient detail for a crop may be skipped; the script records skipped files in a review CSV.

Brightness normalization happens later, when `scripts/features.py` loads the saved strips. It divides each strip’s pixel values by that strip’s average brightness. You can retrain and evaluate the model in Colab using the included eye strips without repeating the cropping.

**Dataset credit:** Thillaikarasi R (2026), [*Child Facial Image Dataset for Autism Spectrum Detection*, version 1](https://doi.org/10.17632/nfcv6x8n7h.1), Mendeley Data. The source is listed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The bundled eye images are adapted from the original photos. Attribution does not replace permission to share identifiable images. Check privacy and consent requirements before sharing or publishing these files.

Only load project ZIPs you trust and upload photos you have permission to use in Colab. Prediction downloads can include filenames. Clear notebook outputs before sharing a copy.
