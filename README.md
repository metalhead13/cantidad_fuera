# Customer Request Management Data Repository

This repository contains a structured dataset for managing customer staffing requests and recruitment processes. It provides a comprehensive tracking system for job vacancies, candidate information, and hiring status across multiple countries and clients.

The system maintains detailed records of staffing requests including job profiles, required qualifications, compensation details, and candidate tracking. It supports various work modalities (remote, hybrid, on-site) and handles multiple types of positions across different technical domains. The data structure enables efficient tracking of the complete recruitment lifecycle from initial request to candidate placement.

## Repository Structure
```
.
└── Datos_Clientes.txt    # Main data file containing customer requests and candidate information
```

## Usage Instructions

### Prerequisites
- Text editor with UTF-8 encoding support
- Spreadsheet software (optional) for data analysis
- Database management system (optional) for data import

### Installation
1. Clone the repository:
```bash
git clone [repository-url]
```

2. Ensure proper text encoding:
- For Windows: Use Notepad++ or similar with UTF-8 encoding
- For MacOS/Linux: Use native text editors or VS Code

### Quick Start
1. Open `Datos_Clientes.txt` in your preferred text editor
2. Data is tab-delimited with the following columns:
```
Timestamp | Country | Commercial Manager | Client | Client Manager Info | Vacancies | Job Profile | ...
```

3. Basic data access example (Python):
```python
import pandas as pd

# Read the tab-delimited file
df = pd.read_csv('Datos_Clientes.txt', sep='\t')

# Display basic statistics
print(f"Total requests: {len(df)}")
print(f"Active requests: {len(df[df['Estado'] == 'ATENDIDA'])}")
```

### More Detailed Examples

#### Filtering Requests by Status
```python
# Get all completed placements
completed = df[df['Estado'] == 'CONTRATADO']

# Get active requests
active = df[df['Estado'] == 'ATENDIDA']

# Get requests by country
spain_requests = df[df['Pais'] == 'España']
```

#### Analyzing Work Modalities
```python
# Count requests by work modality
modality_counts = df['Modalidad de Trabajo'].value_counts()
print(modality_counts)
```

### Troubleshooting

#### Common Issues

1. File Encoding Issues
- Problem: Special characters appear corrupted
- Solution: Ensure file is opened with UTF-8 encoding
```python
df = pd.read_csv('Datos_Clientes.txt', sep='\t', encoding='utf-8')
```

2. Data Format Issues
- Problem: Columns not properly separated
- Solution: Verify tab delimiter is preserved
```python
# Check delimiter consistency
with open('Datos_Clientes.txt', 'r', encoding='utf-8') as f:
    first_line = f.readline()
    expected_columns = 28
    if len(first_line.split('\t')) != expected_columns:
        print("Delimiter issue detected")
```

## Data Flow
The system manages customer requests through a linear process from initial submission to candidate placement. Data flows from request creation through candidate selection and final status updates.

```ascii
[Request] -> [Processing] -> [Candidate Selection] -> [Status Update]
   |             |                    |                     |
   v             v                    v                     v
Timestamp    Assignment          Candidates            Final Status
Country      Validation         Evaluation            Update Record
Details      Processing         Selection             Close Request
```

Key Component Interactions:
1. Request Creation: Captures initial client requirements and job details
2. Request Processing: Commercial managers review and validate requests
3. Candidate Management: Tracks potential candidates for each position
4. Status Tracking: Monitors request progress from open to completion
5. Client Communication: Records client manager contact information
6. Resource Allocation: Manages team assignments and equipment requirements
7. Performance Metrics: Tracks time-to-fill and success rates