---
agent: 'agent'
description: Generate detailed manual test cases in CSV format for the given user story and acceptance criteria.
---
 
# Manual Test Case Generation Prompt
 
## Input Requirements
 
**User Story File Path:** Prompt user to provide the file path at runtime
- Example: `/workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/User Story/User Story_881.md`
 
- The prompt will ask: "Please provide the User Story file path:"
 
**Template Reference:** `/workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/Template/Template_881.md`
 
**Navigation Steps Reference:** `/workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/Reference/Navigation_Steps_881.md`
 
**Output Location:** `/workspaces/Ezdocs-Manual/Optimus Core/4_Design Studio/EZ-881.csv`
 
- The prompt will ask: "Please provide the Output Location file path:"
 
 
---
 
## Goal
 
Generate manual test cases in CSV format based on the user story provided in the input file path. Each test case should follow the template structure and application flow defined in the reference documents.
 
---
 
## Instructions
 
### 1. Read Input Files
- Prompt the user to enter the User Story file path
- Read the user story and acceptance criteria from the provided file path
- Read the template structure from `Template_881.md`
- Read any reference documents for application flow (if available)
- Navigation Steps Reference: `Navigation_Steps_881.md` strictly follow the navigation steps only if they are explicitly required by the user story scenarios.
 
### 2. Analyze User Story
- Identify all distinct scenarios within the user story **ONLY**
- Do not create additional scenarios beyond what is explicitly defined in the user story acceptance criteria
- Extract scenario-specific details:
  - Scenario title/name
  - Acceptance criteria
  - Preconditions (explicit or contextual)
  - Expected outcomes
  - UI elements mentioned
 
### 3. Generate Test Cases
 
For each scenario **explicitly mentioned in the user story**, generate **exactly one** test case with multiple rows (one row per action-expected result pair):
 
#### Multi-Row Structure
 
**First Row (Complete Test Case Information):**
- TC ID: Sequential number
- Test Type: Manual
- Test Case Name: Full descriptive name following format
- Description: Complete objective of the test case
- Action: First action step (numbered as "1. ")
- Expected Result: First expected result (numbered as "1. ")
- Test Repository Path: Full path to test repository
- Status: Done / In Progress / Not Started
- User Story: User Story ID
- Priority: High / Medium / Low
 
**Subsequent Rows (Same Test Case - Additional Steps):**
- TC ID: Same as first row
- Test Type: Leave empty or repeat
- Test Case Name: Leave empty
- Description: Leave empty
- Action: Next action step (numbered as "2. ", "3. ", etc.)
- Expected Result: Next expected result
- Test Repository Path: Leave empty
- Status: Leave empty
- User Story: Leave empty
- Priority: Leave empty
 
#### Test Case Structure (Based on Template)
 
**Required Fields:**
- **TC ID:** Sequential number (1, 2, 3...)
- **Test Type:** Manual
- **Test Case Name:** {Format: TC{ID}_{Scenario name}_{LOB/Module}_{Transaction Type}_{Acceptance Criteria}}
- **Description:** {Clear description of the objective and what the test case validates}
- **Action:** All action steps combined in a single cell, each numbered (1., 2., 3., etc.) and separated by line breaks within the cell
- **Expected Result:** All expected results combined in a single cell as continuous text without numbering, separated by line breaks or spaces
- **Test Repository Path:** {Path to test repository}
- **Status:** Done / In Progress / Not Started
- **User Story:** {User Story ID}
- **Priority:** High / Medium / Low
 
- Multiple action steps are combined in the "Actions" column using line breaks and numbered sequentially (1., 2., 3., etc.)
- Expected results are combined in the "Expected Results" column as continuous text WITHOUT numbering.
 
**Navigation Requirements:**
- Only include navigation steps that are explicitly required by the user story scenarios
- If the user story mentions specific navigation (e.g., "navigate to Claims Overview tab"), include those navigation steps
- If the user story mentions creating specific data or runs, include those creation steps in the first test case only
- If the user story is focused on a specific page/feature, navigate directly to that context after login
- Do not include unnecessary setup steps that are not mentioned in the user story
 
**Setup Requirements:**
- If the user story requires creating runs or uploading data, include these steps in the first test case
- For subsequent test cases, reference the existing setup: "Use the Run created in TC1"
 
#### Validation Requirements
 
- Set priority based on user story importance
- Clearly define expected results for each action step
 
## Output Format: CSV Structure
 
Generate test cases in CSV format with the following columns:
 
**CSV Headers:**
```
TC ID,Test Type,Test Case Name,Description,Action,Expected Result,Test Repository Path,Status,User Story,Priority
```
 
**CSV Format Rules:**
1. **Each Action-Expected Result pair is a separate row**
2. **First row of each test case** contains:
   - TC ID (e.g., 1, 2, 3)
   - Test Type (Manual)
   - Test Case Name (full descriptive name)
   - Description (objective of the test case)
   - Action: First Action step (numbered as "1. ")
   - Expected Result: First Expected Result (numbered as "1. ")
   - Test Repository Path
   - Status
   - User Story ID
   - Priority
3. **Subsequent rows for the same test case** contain:
   - TC ID: Same as first row
   - Test Type: Empty
   - Test Case Name: Empty
   - Description: Empty
   - Action: Next Action step (numbered as "2. ", "3. ", etc.) - IN THE ACTION COLUMN ONLY
   - Expected Result: Next Expected Result- IN THE EXPECTED RESULT COLUMN ONLY
   - Test Repository Path: Empty
   - Status: Empty
   - User Story ID: Empty
   - Priority: Empty
4. Escape commas within fields using double quotes
5. Escape double quotes within fields by doubling them ("")
6. Number actions sequentially (1., 2., 3., etc.)
7. Number expected results sequentially (1., 2., 3., etc.)
8. **CRITICAL:** Keep Action and Expected Result in SEPARATE columns - do NOT combine them
 
#### Scenario Coverage Rules
 
**Focus on Explicit Requirements:**
- Focus only on the specific functionality described in each scenario
- Do not add edge cases, boundary testing, or negative scenarios unless explicitly mentioned in the user story
- Generate **exactly one test case per scenario** as defined in the user story
- Include scope considerations (e.g., Domestic, Produced)
- Ensure all transaction types mentioned in the user story are covered:
  - New Business
  - Quote, Binder, Policy, MidTerm Transactions
  - Scope: Domestic, International.
- Genearte atleast 8 to 10 test cases covering all scenarios and transaction types mentioned in the user story
- The number of test cases must match exactly the number of scenarios defined in the user story
 
**No Duplicate Test Cases:**
- Do not create duplicate test cases for the same scenario
- Do not create additional scenarios beyond what is defined in the user story
- Do not include steps/validations not explicitly mentioned in the user story or acceptance criteria
 
---
**CSV Formatting:**
- Ensure proper escaping of special characters
- Use double quotes for fields containing commas
- Use || as step separator and | as input/expected separator
- Keep formatting consistent across all test cases
- Strictly follow Template_861.md structure for column names and order for CSV output
- Follow Template_861.md template, but don't use the example data provided there; generate new data based on the user story provided in the input file path.
 
---
 
## Example Test Case Generation
 
**Given User Story:**
```
User Story: Verify that the field name should be renamed from “Local Policy Means” to “FoS Hub Master Policy” for Form Interlocking and Hold Harmless Endorsement (Canadian Master Policy) ZC-ZPRO-474-A CW. 
 
Acceptance Criteria:
1 .Verify that the field name should be renamed from “Local Policy Means” to “FoS Hub Master Policy” for Form Interlocking and Hold Harmless Endorsement (Canadian Master Policy) ZC-ZPRO-474-A CW. 
 
```
 
**Generated CSV Output:**
```csv
TC ID,Test Type,Test Case Name,Description,Action,Expected Result,Test Repository Path,Status,User Story,Priority
```
---
 
## Execution Command
 
When ready to generate test cases, the system will:
1. Prompt user for input file path
2. Read and analyze the user story
3. Generate test cases following the template
4. Save as CSV in the specified location
5. Display confirmation with file path and test case count
 
---
 