# Online shopping purchase ranking with PySpark

INFOSYS 722 Iteration 4 BDAS. Recorded execution in Google Colab, 15 October 2026.

The executed notebook contains all code and visible outputs. Data preparation, integration, model fitting and evaluation use Spark DataFrames and MLlib. The data is approximately 1 MB; this demonstrates a distributed processing framework on one Colab machine, not multi-machine scalability.

## Files

- `INFOSYS722_I4_BDAS.ipynb`: 102 cells, including 94 executed code cells and retained outputs. No saved unhandled errors.
- `online_shoppers_intention.csv`: unchanged original public dataset, 12,330 rows and 18 fields.
- `ca-gregorian.json` and `Unicode_LICENSE.txt`: original independent calendar reference and its licence.
- `I4_BDAS_native_results_20261015.zip`: native data, source manifests, split, preparation, calendar integration, six fitted models, all figures and final-test evidence. The internal manifest gives per-file hashes.
- `I4_presentation_addendum.zip`: the report tree diagram typeset from the same 13 saved native nodes; includes its reproducible ReportLab source and source hashes. No model or prediction changed.
- `requirements.txt`: main packages and environment notes.
- `SHA256SUMS.txt`: checksums for these project files.

The written report and personal Chrome screenshots are provided separately in the assessment package.

[Google Colab notebook](https://colab.research.google.com/drive/1_-sgqFxsJ5SUeWsVXR39i2mGhRhjpeA1)

## Recorded methods and results

Identical feature profiles stay together across training (7,878 rows), validation (1,975) and test (2,477). Categories, scaling and balanced loss weights are fitted on training only. The model uses 16 source predictors, excluding PageValues, and 80 encoded components.

Three baseline models and three single-parameter refits were actually run: logistic maxIter 100 to 300, tree maxDepth 4 to 6, and forest minInstancesPerNode 50 to 20. Validation tie sensitivity led to an explicit discretionary choice of the baseline forest: 100 trees, depth 6, minimum node size 50 and seed 42. Its original validation capacity count is 139; the tree's nominal 145 is retained and is not concealed.

The workflow freeze at 05:14:22 UTC precedes the single final-test phase at 05:15:52 UTC. The final top 496 records contain 175 of 381 purchases: 45.93% capture, 35.28% precision at capacity and lift 2.2938. ROC-AUC is 0.7650 and Spark PR-AUC 0.3511. No model, processing, capacity or tie rule changed after test exposure. Later cells check saved predictions and create presentation figures only.

## Execution and preservation

The recorded environment is Spark 4.0.4, Python 3.13.16 and Java 21. Native model outputs and predictions are preserved. In Colab the notebook uses `/content/drive/MyDrive/Infosys722_I4_BDAS`; a different user can adapt this one project-root setting and place the original CSV in its `data` subfolder. Inputs and native results are also supplied here and in the archive.

Do not blindly run all cells over the existing project. The split is guarded against changed allocation, and the freeze/start records deliberately prevent silently repeating the final test. For inspection, open the retained outputs and saved `final_test/metrics.json`, `predictions.parquet`, `freeze_manifest.json` and `independent_check.json` in the native archive. A fresh independent reproduction would need a separate working project and transparent provenance; it must not replace the recorded assessment or enable test-driven tuning.

Spark's experimental plotting API produced native HTML, but static export encountered a missing Kaleido package, Plotly compatibility problems and then an absent Chrome binary. The notebook preserves actual repair attempts and messages. The portable charts use Matplotlib on Spark-computed aggregates and native model structures. The final report tree is typeset from preserved nodes using ReportLab, with an explicit true/false branch legend. No scikit-learn model is substituted.

## Sources and limits

Sakar, C., & Kastro, Y. (2018). *Online shoppers purchasing intention dataset* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5F88Q — CC BY 4.0.

Unicode CLDR English Gregorian calendar JSON, pinned commit `91c267402229a59e3ef2774544f001bf959e8809`: https://github.com/unicode-org/cldr-json/blob/91c267402229a59e3ef2774544f001bf959e8809/cldr-json/cldr-dates-full/main/en/ca-gregorian.json . The original Unicode V3 licence is included. This reference supplies month aliases and calendar order; it adds no shopping observations or predictive measurements.

The same source was explored in earlier iterations. There are no user/session IDs, timestamps or years, and availability of all whole-session features before intervention is unverified. Results support retrospective ranking in this extract. They do not establish future-user generalisation, calibrated probabilities, causal sales uplift or commercial profitability.
