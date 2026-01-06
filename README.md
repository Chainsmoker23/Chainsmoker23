# research-pdf-gen

NPM package to generate research paper PDFs from Markdown, JSON, or LaTeX inputs using pre-built templates for formats like IEEE, ACM, etc.

## 📋 Table of Contents
- [Installation](#installation)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
- [Supported Formats](#supported-formats)
- [Research Papers Included](#research-papers-included)
- [Examples](#examples)
- [Development](#development)
- [License](#license)

## 📦 Installation
```bash
npm install research-pdf-gen
```

## 🔧 Prerequisites

This package requires a LaTeX distribution to be installed on your system to generate PDFs:

- **Windows**: [MiKTeX](https://miktex.org/) or [TeX Live](https://www.tug.org/texlive/)
- **macOS**: [MacTeX](https://www.tug.org/mactex/) or BasicTeX
- **Linux**: texlive package (e.g., `sudo apt-get install texlive-full`)

## 🚀 Usage

### Command Line Interface (CLI)

Generate a PDF from a JSON file:
```bash
research-pdf-gen --format ieee --input path/to/file.json --output output.pdf
```

Generate a PDF from a Markdown file:
```bash
research-pdf-gen --format ieee --input path/to/file.md --output output.pdf
```

Generate a PDF with bibliography:
```bash
research-pdf-gen --format ieee --input path/to/file.json --bib path/to/bibliography.bib --output output.pdf
```

Generate a PDF with a custom template:
```bash
research-pdf-gen --format ieee --input path/to/file.json --template path/to/custom-template.tex --output output.pdf
```

Preview the generated LaTeX without creating a PDF:
```bash
research-pdf-gen --format ieee --input path/to/file.json --dry-run
```

### CLI Options

- `--format <format>`: Research format (ieee, acm) - defaults to 'ieee'
- `--input <path>`: Input file (md, json, tex) or JSON string
- `--output <path>`: Output PDF path - defaults to 'output.pdf'
- `--bib <path>`: BibTeX file path
- `--template <path>`: Custom template path
- `--dry-run`: Preview LaTeX without compiling

### Programmatic Usage

```javascript
const { generatePDF } = require('research-pdf-gen');

// Example with JSON input
const options = {
  format: 'ieee',
  input: {
    title: 'My Research Paper',
    abstract: 'This is the abstract of my research paper.',
    sections: [
      {
        heading: 'Introduction',
        content: 'This is the introduction section.'
      },
      {
        heading: 'Methodology',
        content: 'This section describes the methods used.'
      },
      {
        heading: 'Conclusion',
        content: 'This section summarizes the findings.'
      }
    ]
  },
  output: 'output.pdf',
  bibFile: 'path/to/bibliography.bib'  // Optional
};

generatePDF(options)
  .then(() => console.log('PDF generated successfully'))
  .catch(err => console.error('Error:', err));
```

## 📄 Supported Formats

### IEEE Format 📊
- **Document Class**: IEEEtran
- **Features**: 
  - Conference paper format
  - Two-column layout
  - Standard IEEE styling
  - Keywords support
  - Author affiliations
  - ORCID identifiers support
- **LaTeX Requirements**: IEEEtran class files
- **PDF Output**: Professional IEEE-style research papers
- **Logo**: [IEEE](https://www.ieee.org/) - Institute of Electrical and Electronics Engineers

### ACM Format 🖥️
- **Document Class**: acmart
- **Features**:
  - Conference and journal formats
  - Multiple layout options
  - ACM-specific styling
  - Author affiliations
- **LaTeX Requirements**: acmart class files
- **PDF Output**: ACM-style research papers
- **Logo**: [ACM](https://www.acm.org/) - Association for Computing Machinery

### LaTeX Direct Support 🧮
- **Document Class**: User-specified
- **Features**:
  - Direct LaTeX compilation
  - Full LaTeX feature support
  - Math expressions
  - Tables and figures
  - Bibliographies
  - Custom formatting
- **LaTeX Requirements**: Standard LaTeX installation
- **PDF Output**: Exact LaTeX rendering
- **Best For**: Complex academic papers with advanced formatting

## 📚 Research Papers Included

This package includes two complete, ready-to-use research papers in academic format:

### 📰 IEEE-Journal.tex
A comprehensive research paper in IEEE format with:
- Multiple authors with affiliations and ORCID identifiers
- Complete mathematical framework with proper equations
- Tables and figures formatted for IEEE standards
- Full bibliography with citations
- Abstract and keywords
- Example usage: `node cli.js --format ieee --input IEEE-Journal.tex --output IEEE-Journal.pdf`

### 📖 Springer-Journal.tex
A comprehensive research paper in Springer format with:
- Multiple authors with affiliations and ORCID identifiers
- Complete mathematical framework with proper equations
- Tables and figures formatted for Springer standards
- Full bibliography with citations
- Abstract and keywords
- Note: Requires Springer LaTeX class files for compilation
- Example usage: `node cli.js --format ieee --input Springer-Journal.tex --output Springer-Journal.pdf` (with appropriate class files)

### 📚 References.bib
Bibliography file containing all cited references:
- Complete BibTeX entries for all citations
- Properly formatted for IEEE and Springer styles
- Example usage: `node cli.js --format ieee --input paper.tex --bib references.bib --output paper.pdf`

### 🖼️ Adding Figures and Diagrams
To include figures and diagrams in your research papers:

1. Place your image files in the `figures/` directory
2. Use the standard LaTeX `\includegraphics` command in your document:
   ```latex
   \begin{figure}[!t]
   \centering
   \includegraphics[width=3in]{figures/my-diagram.png}
   \caption{Description of the figure}
   \label{fig:mylabel}
   \end{figure}
   ```
3. Reference the figure in your text using `Figure \ref{fig:mylabel}`

The system automatically detects figure references and copies the required image files to the temporary compilation directory during PDF generation. Supports common image formats like PNG, JPG, PDF, and EPS.

## 🧮 Mathematical Expressions

The system properly handles complex mathematical expressions:

- Inline math: `$x = y + z$` → renders as $x = y + z$
- Display math: `$$\sum_{i=1}^{n} x_i$$` → renders as $$\sum_{i=1}^{n} x_i$$
- Complex equations with Greek letters, subscripts, superscripts
- Matrix equations and integrals
- Proper LaTeX math packages included

## 📋 Complete User Scenario: From Installation to Professional Research Paper

This section provides a complete walkthrough of how to use the research-pdf-gen package from installation to generating a professional academic paper with all features.

### Step 1: Installation

Open your terminal/command prompt and install the package globally:

```bash
npm install -g research-pdf-gen
```

Or, if you want to use it in a specific project:

```bash
npm install research-pdf-gen
```

### Step 2: Prerequisites

Make sure you have the following installed on your system:

- **Node.js** (version 12 or higher)
- **MiKTeX** or **TeX Live** (for LaTeX compilation)

On Windows, you can install MiKTeX from: https://miktex.org/

### Step 3: Prepare Your Research Content

Create a LaTeX file for your research paper. Here's a complete example with all features:

#### File: `my-research-paper.tex`

```latex
\documentclass[conference]{IEEEtran}

\usepackage{graphicx}
\usepackage{amsmath,amssymb,amsfonts}
\usepackage{algorithmic}
\usepackage{booktabs}
\usepackage{textcomp}
\usepackage{xcolor}
\usepackage{url}
\usepackage{cite}

\title{Advanced Machine Learning Approaches in Predictive Healthcare Analytics: A Comprehensive Analysis of Deep Learning Models for Medical Diagnosis}

\author{John~Doe,~\IEEEmembership{Member,~IEEE}
        and~Jane~Smith,~\IEEEmembership{Senior~Member,~IEEE}
        and~Robert~Johnson,~\IEEEmembership{Member,~IEEE}% <-this % stops a space
\thanks{J. Doe is with the Department of Computer Science, University of Technology, City, Country.}% 
\thanks{J. Smith is with the Medical Center, City, Country.}
\thanks{R. Johnson is with the Institute for Artificial Intelligence, University of Technology, City, Country.}
\thanks{Corresponding author: john.doe@university.edu}
\thanks{ORCID: John Doe: 0000-0002-1825-0097, Jane Smith: 0000-0001-5678-9012, Robert Johnson: 0000-0003-4567-8901}
}

\begin{document}

\maketitle

\begin{abstract}

The integration of machine learning (ML) in healthcare analytics has revolutionized the way medical professionals approach patient care, diagnosis, and treatment planning. This research paper provides a comprehensive analysis of various machine learning methodologies applied in predictive healthcare analytics. We examine supervised, unsupervised, and deep learning approaches, comparing their effectiveness in predicting patient outcomes, disease progression, and treatment responses. Our study demonstrates that ensemble methods and neural networks achieve superior performance in complex diagnostic scenarios, with accuracy rates exceeding 92\% in certain applications. The findings suggest that hybrid approaches combining multiple ML techniques can significantly improve predictive accuracy while maintaining clinical interpretability. We present a novel framework for incorporating patient demographics, medical history, and real-time vital signs into predictive models, achieving state-of-the-art results on multiple clinical datasets.

\end{abstract}

\begin{IEEEkeywords}
Machine learning, healthcare analytics, predictive modeling, deep learning, clinical decision support, medical diagnosis, artificial intelligence, patient outcomes, ensemble methods, neural networks.
\end{IEEEkeywords}

\section{Introduction}

Healthcare systems worldwide are experiencing unprecedented growth in data generation, with electronic health records (EHRs), medical imaging, genomics, and wearable devices contributing to an ever-expanding pool of health-related information. The effective utilization of this data through machine learning algorithms presents a transformative opportunity to enhance patient care, reduce healthcare costs, and improve clinical decision-making processes.

The application of machine learning in healthcare has shown remarkable promise in several domains, including early disease detection, personalized treatment recommendations, and predictive modeling of patient outcomes \cite{campbell1996index}. However, the complexity and sensitivity of healthcare data require specialized approaches that not only achieve high predictive accuracy but also maintain interpretability and reliability essential for clinical applications.

This paper explores the current state of machine learning applications in healthcare analytics, analyzes various algorithmic approaches, and provides insights into future research directions and implementation challenges \cite{slifka2000clinical}. We introduce a novel multi-modal framework that combines structured EHR data with unstructured clinical notes and medical imaging, demonstrating significant improvements in diagnostic accuracy.

\section{Literature Review}

The application of machine learning in healthcare has evolved significantly over the past decade. Campbell and Gear \cite{campbell1996index} demonstrated the foundational work in numerical methods that underpin many ML algorithms. Subsequently, Slifka and Whitton \cite{slifka2000clinical} expanded the scope to include advanced mathematical modeling approaches, achieving significant improvements in predictive accuracy on datasets of various scales.

Recent advances in deep learning have further enhanced predictive capabilities. Hamburger \cite{hamburger1995quasimonotonicity} developed sophisticated mathematical frameworks for nonlinear systems, achieving state-of-the-art results in complex modeling tasks. Meanwhile, Geddes et al. \cite{geddes1992algorithms} explored the algorithmic foundations that enable efficient computation in large-scale healthcare applications.

\section{Methodology}

\subsection{Data Collection and Preprocessing}

Our research utilized a comprehensive dataset comprising 150,000 patient records from multiple healthcare institutions over a 5-year period. The dataset included demographic information, laboratory results, vital signs, medical history, treatment records, and clinical notes. Data preprocessing involved:

\begin{itemize}
\item Missing value imputation using k-nearest neighbors with $k=5$
\item Outlier detection and treatment using the interquartile range method with factor 1.5
\item Feature scaling and normalization using robust scaling
\item Categorical variable encoding using target encoding
\item Temporal feature engineering for time-series analysis
\end{itemize}

\subsection{Machine Learning Models}

We implemented and evaluated several machine learning approaches:

\subsubsection{Traditional Supervised Learning}

\textbf{Logistic Regression}: Applied for binary classification tasks with L2 regularization to prevent overfitting. Hyperparameters were optimized using 5-fold cross-validation.

\textbf{Random Forest}: Ensemble method combining 200 decision trees with bootstrap aggregation. Feature importance analysis was conducted to identify key predictive variables.

\textbf{Support Vector Machine}: RBF kernel with cross-validation for hyperparameter optimization. Grid search was used to find optimal C and gamma parameters.

\subsubsection{Advanced Deep Learning}

\textbf{Multilayer Perceptron}: 5 hidden layers with 256, 128, 64, 32, and 16 neurons respectively, using ReLU activation functions and dropout regularization.

\textbf{Convolutional Neural Network}: For medical image analysis with 7 convolutional layers and 3 fully connected layers, utilizing batch normalization.

\textbf{Recurrent Neural Network}: Long Short-Term Memory (LSTM) networks for time-series analysis of patient vital signs and lab values.

\subsection{Evaluation Metrics}

Model performance was evaluated using multiple metrics to ensure comprehensive assessment:
\begin{itemize}
\item Accuracy: $(TP + TN) / (TP + TN + FP + FN)$
\item Precision: $TP / (TP + FP)$
\item Recall: $TP / (TP + FN)$
\item F1-Score: $2 \times (Precision \times Recall) / (Precision + Recall)$
\item Area Under the ROC Curve (AUC)
\item Area Under the Precision-Recall Curve
\item Mean Absolute Error for regression tasks
\end{itemize}

\section{Mathematical Framework}

\subsection{Performance Optimization}

The optimization problem for our predictive models can be formulated as:

$$ \min_{\theta} \frac{1}{n} \sum_{i=1}^{n} L(f(x_i; \theta), y_i) + \lambda R(\theta) $$

Where:
\begin{itemize}
\item $\theta$ represents model parameters
\item $L$ is the loss function (cross-entropy for classification, MSE for regression)
\item $f(x_i; \theta)$ is the model prediction for input $x_i$
\item $y_i$ is the true label for input $i$
\item $R(\theta)$ is the regularization term (L1, L2, or elastic net)
\item $\lambda$ controls regularization strength
\end{itemize}

For multi-task learning, we extend this to:

$$ \min_{\theta} \sum_{t=1}^{T} \alpha_t \left[ \frac{1}{n_t} \sum_{i=1}^{n_t} L_t(f_t(x_i; \theta), y_{ti}) \right] + \lambda R(\theta) $$

Where $T$ is the number of tasks and $\alpha_t$ are task-specific weights.

\subsection{Statistical Analysis}

For comparing model performance, we employed the paired t-test:

$$ t = \frac{\bar{d}}{s_d / \sqrt{n}} $$

Where $\bar{d}$ is the mean difference in performance, $s_d$ is the standard deviation of differences, and $n$ is the sample size. Statistical significance was set at $p < 0.05$.

\section{Results}

\subsection{Model Performance Comparison}

\begin{figure}[!t]
\centering
\includegraphics[width=2.5in]{figures/model-architecture.png}
\caption{Neural network architecture for healthcare prediction model. The model consists of input layer, multiple hidden layers with dropout regularization, and output layer.}
\label{fig:architecture}
\end{figure}

As shown in Figure \ref{fig:architecture}, our proposed model architecture includes several key components that contribute to its superior performance. The network consists of an input layer that processes the normalized healthcare data, followed by five hidden layers with ReLU activation and dropout regularization to prevent overfitting.

\begin{table}[htbp]
\centering
\caption{Performance comparison of different machine learning models on healthcare dataset}
\begin{tabular}{lcccccc}
\toprule
Model & Accuracy & Precision & Recall & F1-Score & AUC & Training Time (s) \\
\midrule
Logistic Regression & 0.78 & 0.76 & 0.80 & 0.78 & 0.82 & 2.3 \\
Random Forest & 0.89 & 0.88 & 0.90 & 0.89 & 0.93 & 15.7 \\
SVM & 0.85 & 0.84 & 0.86 & 0.85 & 0.89 & 45.2 \\
Neural Network & 0.92 & 0.91 & 0.93 & 0.92 & 0.95 & 128.4 \\
CNN & 0.94 & 0.93 & 0.95 & 0.94 & 0.97 & 320.1 \\
LSTM & 0.91 & 0.90 & 0.92 & 0.91 & 0.94 & 285.6 \\
\bottomrule
\end{tabular}
\label{tab:performance}
\end{table}

\subsection{Computational Efficiency Analysis}

Processing times for model training and prediction are detailed in Table \ref{tab:performance}. The CNN model achieved the highest accuracy but required the most computational resources. The Random Forest model offered the best balance between performance and computational efficiency, making it suitable for real-time clinical applications.

\subsection{Ablation Studies}

We conducted ablation studies to evaluate the contribution of different components:

\begin{itemize}
\item Feature engineering: +8.3\% improvement in AUC
\item Multi-modal data fusion: +5.7\% improvement in AUC
\item Ensemble methods: +3.2\% improvement in AUC
\item Temporal modeling: +4.1\% improvement in AUC
\end{itemize}

\section{Discussion}

The results demonstrate that ensemble methods and neural networks significantly outperform traditional approaches in predictive healthcare analytics. The CNN model achieved the highest accuracy at 94\%, likely due to its ability to capture complex patterns in multi-modal data. However, Random Forest showed excellent balance between performance and computational efficiency, making it suitable for real-time clinical applications.

The mathematical framework successfully optimized model parameters, with regularization effectively preventing overfitting. The statistical analysis confirmed significant performance differences between models ($p < 0.001$). Our multi-modal approach combining structured and unstructured data showed substantial improvements over single-modality models.

Limitations of our study include the potential for selection bias in the clinical dataset and the need for external validation on datasets from different institutions. Additionally, the interpretability of deep learning models remains a challenge in clinical settings where explainability is crucial.

\section{Conclusion}

Machine learning approaches in predictive healthcare analytics show tremendous potential for improving patient outcomes. Ensemble methods like random forests offer an optimal balance of accuracy, interpretability, and computational efficiency for clinical applications \cite{broy1992software}. Deep learning approaches provide superior accuracy for complex diagnostic tasks but require careful consideration of computational resources and interpretability requirements \cite{taylor2021ethics}.

Future research should focus on developing more interpretable deep learning models, addressing data privacy concerns in healthcare applications \cite{white2020data}, and creating standardized evaluation protocols for clinical ML models. Additionally, the integration of causal inference methods could help establish more robust relationships between treatments and outcomes.

\section*{Acknowledgment}

The authors would like to thank the Department of Computer Science and the Medical Center for their support and resources for this research. We also acknowledge the patients and healthcare providers who contributed data to this study, making this research possible.

\begin{thebibliography}{12}
\bibitem{campbell1996index} S. L. Campbell and C. W. Gear, ``The index of general nonlinear DAEs,'' \emph{Numerische Mathematik}, vol.~72, no.~2, pp. 173--196, 1996.

\bibitem{slifka2000clinical} M. K. Slifka and J. L. Whitton, ``Clinical implications of dysregulated cytokine production,'' \emph{Journal of Molecular Medicine}, vol.~78, no.~2, pp. 74--80, 2000.

\bibitem{hamburger1995quasimonotonicity} C. Hamburger, ``Quasimonotonicity, regularity and duality for nonlinear systems of partial differential equations,'' \emph{Annali di Matematica Pura ed Applicata}, vol.~169, no.~1, pp. 321--354, 1995.

\bibitem{geddes1992algorithms} K. O. Geddes, S. R. Czapor, and G. Labahn, \emph{Algorithms for Computer Algebra}. Boston: Kluwer, 1992.

\bibitem{broy1992software} M. Broy, ``Software engineering---from auxiliary to key technologies,'' in \emph{Software Pioneers}. New York: Springer, pp. 10--13, 1992.

\bibitem{taylor2021ethics} B. Taylor, A. Miller, and L. Jones, ``Ethical considerations in AI-driven healthcare,'' \emph{AI Ethics Journal}, vol.~3, no.~2, pp. 156--171, 2021.

\bibitem{white2020data} C. White, K. Harris, and P. Clark, ``Data quality challenges in healthcare ML applications,'' \emph{Data Science in Medicine}, vol.~7, no.~4, pp. 201--218, 2020.

\bibitem{chen2020multimodal} L. Chen, M. Zhang, and A. Kumar, ``Multimodal learning for clinical decision support,'' \emph{Medical Image Analysis}, vol.~58, pp. 101-112, 2020.

\bibitem{davis2019interpretability} R. Davis, S. Johnson, and T. Williams, ``Interpretable machine learning in healthcare: A review,'' \emph{IEEE Reviews in Biomedical Engineering}, vol.~12, pp. 48-66, 2019.

\bibitem{kim2021privacy} S. Kim, J. Park, and R. Davis, ``Privacy-preserving machine learning in healthcare,'' \emph{Journal of Healthcare Security}, vol.~8, no.~1, pp. 45--62, 2021.

\bibitem{rodriguez2022temporal} C. Rodriguez, D. Thompson, and E. Brown, ``Temporal modeling in clinical time series,'' \emph{Nature Medicine}, vol.~28, pp. 1234--1245, 2022.

\bibitem{patel2020causal} N. Patel, M. Garcia, and T. Wilson, ``Causal inference in healthcare machine learning,'' \emph{Journal of Biomedical Informatics}, vol.~110, pp. 103-115, 2020.

\end{thebibliography}

\end{document}
```

### Step 4: Create the Bibliography File

#### File: `references.bib`

```bibtex
@article{campbell1996index,
  title={The index of general nonlinear DAEs},
  author={Campbell, Stephen L and Gear, C William},
  journal={Numerische Mathematik},
  volume={72},
  number={2},
  pages={173--196},
  year={1996},
  publisher={Springer}
}

@article{slifka2000clinical,
  title={Clinical implications of dysregulated cytokine production},
  author={Slifka, Mark K and Whitton, J Lindsay},
  journal={Journal of molecular medicine},
  volume={78},
  number={2},
  pages={74--80},
  year={2000},
  publisher={Springer}
}

@article{hamburger1995quasimonotonicity,
  title={Quasimonotonicity, regularity and duality for nonlinear systems of partial differential equations},
  author={Hamburger, Christoph},
  journal={Annali di Matematica Pura ed Applicata},
  volume={169},
  number={1},
  pages={321--354},
  year={1995},
  publisher={Springer}
}

@book{geddes1992algorithms,
  title={Algorithms for computer algebra},
  author={Geddes, Keith O and Czapor, Stephen R and Labahn, George},
  year={1992},
  publisher={Springer Science \& Business Media}
}

@incollection{broy1992software,
  title={Software engineering---from auxiliary to key technologies},
  author={Broy, Manfred},
  booktitle={Software Pioneers},
  pages={10--13},
  year={1992},
  publisher={Springer}
}

@article{taylor2021ethics,
  title={Ethical considerations in AI-driven healthcare},
  author={Taylor, Benjamin and Miller, Andrew and Jones, Lisa},
  journal={AI Ethics Journal},
  volume={3},
  number={2},
  pages={156--171},
  year={2021},
  publisher={Springer}
}

@article{white2020data,
  title={Data quality challenges in healthcare ML applications},
  author={White, Christopher and Harris, Katherine and Clark, Paul},
  journal={Data Science in Medicine},
  volume={7},
  number={4},
  pages={201--218},
  year={2020},
  publisher={Springer}
}

@article{chen2020multimodal,
  title={Multimodal learning for clinical decision support},
  author={Chen, Li and Zhang, Ming and Kumar, Arjun},
  journal={Medical Image Analysis},
  volume={58},
  pages={101--112},
  year={2020},
  publisher={Elsevier}
}

@article{davis2019interpretability,
  title={Interpretable machine learning in healthcare: A review},
  author={Davis, Richard and Johnson, Sarah and Williams, Thomas},
  journal={IEEE Reviews in Biomedical Engineering},
  volume={12},
  pages={48--66},
  year={2019},
  publisher={IEEE}
}

@article{kim2021privacy,
  title={Privacy-preserving machine learning in healthcare},
  author={Kim, Seung and Park, Jong and Davis, Richard},
  journal={Journal of Healthcare Security},
  volume={8},
  number={1},
  pages={45--62},
  year={2021},
  publisher={Springer}
}

@article{rodriguez2022temporal,
  title={Temporal modeling in clinical time series},
  author={Rodriguez, Carlos and Thompson, David and Brown, Elizabeth},
  journal={Nature Medicine},
  volume={28},
  pages={1234--1245},
  year={2022},
  publisher={Nature Publishing Group}
}

@article{patel2020causal,
  title={Causal inference in healthcare machine learning},
  author={Patel, Neil and Garcia, Maria and Wilson, Thomas},
  journal={Journal of Biomedical Informatics},
  volume={110},
  pages={103--115},
  year={2020},
  publisher={Elsevier}
}
```

### Step 5: Create a Figures Directory and Add Images

Create a directory for your figures:

```bash
mkdir figures
```

Then place your image files in this directory (e.g., `figures/model-architecture.png`).

### Step 6: Generate the PDF

Now you can generate your professional research paper using the CLI:

```bash
# Generate IEEE format paper
node cli.js --format ieee --input my-research-paper.tex --output my-ieee-paper.pdf

# Or generate Springer format paper
node cli.js --format springer --input my-research-paper.tex --output my-springer-paper.pdf
```

### Step 7: Advanced Features

#### Using External Bibliography File

If you want to use a separate bibliography file:

```bash
node cli.js --format ieee --input my-research-paper.tex --bib references.bib --output my-ieee-paper.pdf
```

#### Custom Templates

To use a custom template:

```bash
node cli.js --format ieee --input my-research-paper.tex --template custom-template.tex --output my-custom-paper.pdf
```

#### Dry Run for Preview

To preview the LaTeX without compiling:

```bash
node cli.js --format ieee --input my-research-paper.tex --dry-run
```

## 💻 Programmatic Usage

You can also use the package programmatically in your Node.js applications:

```javascript
const { generatePDF } = require('research-pdf-gen');

const options = {
  format: 'ieee',
  input: 'my-research-paper.tex',
  output: 'my-paper.pdf',
  bibFile: 'references.bib'  // Optional bibliography file
};

generatePDF(options)
  .then(() => console.log('PDF generated successfully!'))
  .catch(err => console.error('Error:', err));
```

## 🔧 Advanced Programmatic Usage

For more complex scenarios, you can customize the process further:

```javascript
const { generatePDF } = require('research-pdf-gen');

// Example with JSON input
const jsonData = {
  title: 'My Research Paper',
  abstract: 'This is the abstract of my research paper...',
  sections: [
    {
      heading: 'Introduction',
      content: 'This is the introduction section with math: $E = mc^2$'
    },
    {
      heading: 'Methodology',
      content: 'This section describes our methodology...'
    }
  ]
};

const options = {
  format: 'ieee',
  input: jsonData,  // Pass the JSON object directly
  output: 'programmatic-paper.pdf',
  bibFile: 'references.bib'
};

generatePDF(options)
  .then(() => console.log('PDF generated successfully!'))
  .catch(err => console.error('Error:', err));
```

## 📊 Tables and Figures

Support for professional academic tables:
- Booktabs formatting (`\toprule`, `\midrule`, `\bottomrule`)
- Multi-column and multi-row cells
- Table captions and labels
- Figure support with proper positioning

## 📚 Bibliography Support

Full bibliography handling:
- BibTeX file integration
- Proper citation formats (`\cite{key}`)
- Multiple citation styles
- Automatic bibliography generation
- Complete reference lists with proper formatting

## 🔐 Security Features

- Input sanitization to prevent LaTeX injection attacks
- Path traversal protection for file inputs
- Validation of all file paths
- Safe handling of user-provided content

## 🧪 Examples

### Generate PDF from JSON with bibliography
```bash
research-pdf-gen --format ieee --input paper.json --bib references.bib --output paper.pdf
```

### Generate PDF from Markdown with custom output name
```bash
research-pdf-gen --format acm --input paper.md --output my-research-paper.pdf
```

### Generate PDF from LaTeX file (recommended for complex academic papers)
```bash
node cli.js --format ieee --input IEEE-Journal.tex --output IEEE-Journal.pdf
```

### Generate PDF with external bibliography
```bash
node cli.js --format ieee --input paper.tex --bib references.bib --output paper.pdf
```

### Dry run to preview LaTeX code
```bash
research-pdf-gen --format ieee --input paper.json --dry-run
```

## 🛠️ Development

To run tests:
```bash
npm test
```

## 📄 License

MIT
