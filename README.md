# Agentic AI for ZIF-8 Nanocrystal Synthesis

**Scientific literature retrieval, experimental-data provenance, machine-learning regression and autonomous tool use through Claude and the Model Context Protocol (MCP).**

## Project overview

ZIF-8 (zeolitic imidazolate framework-8) is a porous metal–organic framework whose crystal size and morphology are influenced by synthesis conditions. Understanding these relationships requires careful interpretation of experimental evidence, particularly when information comes from different publications, synthesis methods and characterisation techniques.

This project investigates how an AI research agent can support the retrieval, organisation and analysis of scientific evidence related to ZIF-8 nanocrystal synthesis.

The notebook combines scientific literature retrieval, structured evidence storage, Claude-based agentic tool use, MCP integration and two separately trained Random Forest regression models.

The work draws on my experimental research background in ZIF-8 synthesis and porous materials, combined with applied AI and data-science methods.

## Research objectives

The project addresses four questions:

1. Can an AI agent retrieve relevant scientific literature and organise its sources in a traceable way?
2. Can scientific tools be exposed through MCP and selected autonomously by a language-model agent?
3. Can machine-learning models be integrated into the agent's workflow while retaining information about their training data, provenance and limitations?
4. What can a small published experimental dataset reveal about the feasibility and limitations of ZIF-8 particle-size prediction?

The aim is not to replace experimental research, but to explore how AI-assisted scientific workflows can support literature analysis, experimental-data evaluation and preliminary modelling.

## Scientific workflow

### 1. Literature retrieval and evidence management

The notebook uses **OpenAlex** and **Crossref** to retrieve scientific publication metadata relevant to ZIF-8 synthesis.

A **SQLite database** provides structured storage for literature records and experimental evidence, supporting traceability between retrieved publications, screened sources and extracted data.

The workflow distinguishes between:

- Publications identified through bibliographic searches.
- Sources examined for relevance to the scientific question.
- Experimental measurements supported by identifiable sources.
- Synthetic data generated solely for computational demonstrations.

This distinction is essential because bibliographic metadata alone does not establish the validity or comparability of experimental results.

### 2. Claude research agent and MCP integration

A scientific research agent is implemented using the **Anthropic Claude API**.

The notebook first explores native tool use and agent execution, then introduces the **Model Context Protocol (MCP)** as a standardised interface through which the agent can discover and invoke external tools.

The MCP workflow demonstrates:

- Scientific tool registration and discovery.
- Autonomous tool selection by Claude.
- Tool execution and interpretation of returned information.
- Integration of scientific literature services and regression models.
- Communication of model provenance and limitations.

The agent's role is to coordinate computational tasks and assist scientific interpretation, not to establish experimental facts independently.

## Machine-learning models

The notebook develops **two separate Random Forest regression models**, each with a different purpose and dataset.

### Model 1 — Synthetic regression demonstration

The first model demonstrates how a trained machine-learning model can be incorporated into an agentic scientific workflow.

A synthetic dataset of **300 ZIF-8-like synthesis records** is generated with numerical synthesis variables and illustrative particle-size values.

A Random Forest regression model is trained using **240 records** and evaluated on **60 held-out records**.

The trained model is saved together with relevant metadata and exposed as an MCP tool, allowing Claude to select and invoke it autonomously.

**Scientific interpretation:** This model demonstrates the technical integration of machine learning and agentic tool use. Because its training data are synthetic, its predictions do not constitute experimentally validated ZIF-8 particle-size estimates.

### Model 2 — Published experimental-data regression

The second model uses published experimental data rather than synthetic records.

**Dataset source:**

Du, Y. (2024). *Characterization results and synthesis parameters of ZIF-8*. Zenodo.

https://doi.org/10.5281/zenodo.14063747

The dataset contains **27 experimental particle-size records**, representing **23 distinct combinations of recorded synthesis inputs**. Some repeated input combinations have different reported particle sizes.

The notebook examines the dataset's provenance, available synthesis variables, repeated conditions and suitability for exploratory regression.

Three approaches are evaluated:

- Random Forest regression.
- Ridge regression.
- A training-mean baseline.

**Five-fold grouped cross-validation** is used to keep records with identical input conditions together, reducing the risk of information leakage between training and validation sets.

### Experimental model results

| Model | Mean absolute error (MAE) |
|---|---:|
| Random Forest | 29.92 nm |
| Ridge regression | 31.89 nm |
| Training-mean baseline | 40.20 nm |

Random Forest achieved the lowest mean absolute error, approximately **25.6% lower than the baseline**.

However, the dataset is small, and the validation results vary between folds. The mean cross-validation R² values are negative, indicating that predictive performance remains limited and sensitive to the validation split.

These findings support the feasibility of constructing an exploratory experimental-data workflow, **not** the reliability of the model for independent synthesis prediction.

### Autonomous experimental-model invocation

The experimental Random Forest is saved with scientific metadata and integrated into the MCP server as a separate prediction tool.

The notebook demonstrates Claude autonomously selecting and invoking this model, returning a particle-size estimate together with the relevant input conditions, source information and limitations.

The workflow distinguishes between predictions for recorded synthesis conditions and estimates for conditions not represented by an identical recorded input combination.

A model-generated estimate is explicitly treated as a **prediction, not an experimental measurement**.

## Technologies and research resources

| Technology or resource | Role in the project |
|---|---|
| Python | Scientific programming and workflow implementation |
| Jupyter Notebook / Google Colab | Interactive development and execution |
| Anthropic Claude API | AI research agent and autonomous tool use |
| Model Context Protocol (MCP) | Standardised access to scientific and machine-learning tools |
| OpenAlex | Scientific literature discovery |
| Crossref | Publication metadata retrieval |
| Zenodo | Published experimental dataset |
| SQLite | Structured storage and scientific provenance |
| pandas / NumPy | Data handling and numerical operations |
| scikit-learn | Regression modelling, preprocessing and validation |
| Matplotlib | Data visualisation |

## Notebook structure

The notebook is organised into eleven main sections:

1. **Scientific Problem Definition** — research context, objectives, questions and scope.
2. **Environment Setup** — Python libraries and API configuration.
3. **Scientific Data Infrastructure** — OpenAlex retrieval and SQLite storage.
4. **Claude Agent Architecture and Native Tool Use** — agent implementation and tool interaction.
5. **Agent Execution and Scientific Validation** — initial execution and observations.
6. **Structured Experimental Data and Scientific Provenance** — literature screening, source curation and experimental evidence.
7. **Multi-Source Scientific Tools and MCP Integration** — Crossref, MCP server implementation and autonomous tool selection.
8. **Synthetic Regression Demonstration and MCP Integration** — synthetic dataset, Random Forest training, model persistence and autonomous invocation.
9. **Retrieval and Assessment of Published Experimental ZIF-8 Data** — Zenodo dataset, provenance and data-quality assessment.
10. **Experimental-Data Regression and Validation** — model comparison, grouped cross-validation, persistence and Claude–MCP invocation.
11. **Conclusions and Future Directions** — scientific interpretation, limitations and potential extensions.

Each major stage includes scientific observations or evaluation of the results.

## How to run the notebook

The project is provided as a Jupyter notebook and was developed for execution in **Google Colab**.

1. Open the `.ipynb` notebook in Google Colab.
2. Configure your own Anthropic API key in **Colab Secrets** under `ANTHROPIC_API_KEY`.
3. Run the notebook cells sequentially, following the installation and setup instructions.
4. Allow access to the external literature services and published dataset where required.
5. Review the observations and conclusions alongside the computational outputs.

An Anthropic API key is required for the Claude-powered sections. API usage may incur charges.

**Security:** Never place API keys directly in the notebook or upload credentials to a public repository.

The notebook is a research demonstration rather than a packaged software application. Reproduction of live API and MCP operations depends on the availability and compatibility of the relevant services and execution environment.

## Scientific limitations

The notebook documents several important limitations:

**Experimental data availability:** Published synthesis studies differ in their reported variables, methods and characterisation procedures. Not all retrieved literature can be converted into directly comparable numerical records.

**Synthetic versus experimental evidence:** The synthetic model demonstrates computational functionality only. It must not be interpreted as evidence of experimentally established synthesis relationships.

**Small experimental dataset:** The published regression dataset contains only 27 records and 23 distinct input combinations. This limits statistical power and generalisation.

**Validation uncertainty:** Although Random Forest achieved the lowest mean absolute error in grouped cross-validation, negative mean R² values and variation between folds indicate substantial predictive uncertainty.

**Scientific interpretation:** An AI agent can retrieve information, invoke tools and report predictions, but its outputs require verification against primary sources and experimental evidence.

**No independent laboratory validation:** Neither regression model has been independently validated through new synthesis experiments conducted as part of this project.

## Conclusions and future directions

The project demonstrates an end-to-end scientific AI workflow connecting literature retrieval, structured evidence management, autonomous tool use and machine-learning model invocation.

It establishes two distinct regression pathways: a synthetic model for testing the agent–MCP architecture and an exploratory experimental model trained on published ZIF-8 data.

The experimental modelling results also illustrate a central challenge in materials informatics: **a technically functioning prediction pipeline is not necessarily a scientifically reliable predictive model**.

Potential future work includes expanding the curated experimental dataset, improving comparability between published synthesis records, incorporating additional scientifically justified variables, and evaluating predictions against independent experimental measurements.

## Author

**Joanna Cookney**

Materials scientist and chemical engineer with research experience in ZIF-8 synthesis, metal–organic frameworks, porous materials, membrane systems and gas separation, with additional training in applied AI and data science.

This project combines experimental materials-science knowledge with computational methods to investigate practical opportunities and limitations of agentic AI in scientific research.
