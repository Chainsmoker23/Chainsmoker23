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




