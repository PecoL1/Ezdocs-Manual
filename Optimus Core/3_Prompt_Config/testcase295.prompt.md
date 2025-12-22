--- 

agent : agent 

tools:
-search/codebase

- edit/editFiles 

- search

description: Generate manual test cases in CSV format based on user story and acceptance criteria 

--- 

  

# Manual Test Case Generation Prompt 

  

## Execution Workflow 

  

When this prompt is executed, follow these steps: 

  
mandatory Step 1: Collect Mandatory Input Paths (REQUIRED AT RUNTIME)

### Step 1: Collect Mandatory Input Paths (REQUIRED AT RUNTIME)

Ask the user for the following three mandatory file paths:

```
Please provide the following mandatory file paths:

1. User Story file path (e.g., /workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/User Story/{STORY_NAME}.md)
2. Template file path (e.g., /workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/Template/{TEMPLATE_NAME}.md)
3. Navigation Steps file path (e.g., /workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/Reference/{NAV_STEPS_NAME}.md)

Do NOT proceed unless all three paths are provided. Validate that each file exists before processing.
```

### Step 2: Analyze Template Structure

- Read and analyze the provided Template file to extract the EXACT writing pattern, field names, and structure
- Extract the following template characteristics:
  - Test case name format and naming conventions
  - Description writing style and level of detail
  - Actions numbering format (e.g., "1. Action text")
  - Expected Results format (continuous text, no numbering)
  - Field mappings (Test type, Priority, Status, etc.)
- Store this template pattern for use in all generated test cases

### Step 3: Analyze User Story and Navigation Steps

- Read and analyze the User Story file to extract:
  - Main acceptance criteria and requirements
  - Key functional areas and features
  - Input constraints and validation rules
  - Output/printing requirements (e.g., English and French documents)
- Read and analyze the Navigation Steps file to extract:
  - Exact workflow sequences and navigation paths
  - Specific screen names and field labels
  - Step-by-step procedural flows
  - Transaction types (Quote, Binder, Policy, MidTerm, etc.)
- Cross-reference user story requirements with navigation steps to identify test scenarios 

  

### Step 4: Generate Test Cases Following Template Pattern

- For each acceptance criterion/scenario identified in the user story, generate exactly one test case
- STRICTLY follow the template structure and writing pattern for ALL fields
- Apply the following test case generation rules:

**Test Case Structure (must match template pattern):**
  1. **Test type:** Use exact value from template (e.g., "Manual")
  2. **Test case Name:** Write in template's style; descriptive and specific to scenario
  3. **Description:** Follow template's description format; include key validation requirements and expected behavior
  4. **Actions:** Number sequentially (1., 2., 3., etc.); use exact screen/field names from Navigation Steps; match template's granularity level
  5. **Expected Results:** Write as continuous text WITHOUT numbering; include all expected outcomes for all transactions (Quote, Binder, Policy if applicable)
  6. **Test Repository Path:** Use consistent path format from template
  7. **Status:** Use template value
  8. **User story:** Extract from filename
  9. **Scenario Type and Priority:** Use template format (e.g., "Positive/High", "Negative/Medium", "Boundary/High")

**Test Case Categories (generate minimum 3 covering all types):**
  - **Positive Scenario:** Valid inputs, successful workflows, verify all required fields and English/French document generation
  - **Negative Scenario:** Invalid inputs, missing required fields, boundary violations; verify error handling and validation messages
  - **Boundary Scenario:** Edge cases like maximum/minimum values, decimal rounding, special characters, long descriptions

- Incorporate specific navigation steps and field names from Navigation_Steps file into each action sequence
- Ensure test cases cover all transaction types mentioned in navigation steps (Quote, Binder, Policy, MidTerm)
- Create CSV with proper multi-line cell formatting (wrap in double quotes)
- Number actions sequentially with line breaks between steps
- Write expected results as continuous text WITHOUT numbering

### Step 5: Save CSV File and Confirm Completion

- Automatically save the CSV file to: `/workspaces/Ezdocs-Manual/Optimus Core/4_Design Studio/{filename}_TestCases.csv`
- Confirm completion with message:

```
Test cases generated successfully!

Output file: /workspaces/Ezdocs-Manual/Optimus Core/4_Design Studio/{filename}_TestCases.csv
Total test cases: {count}
```

  

--- 

  

## Input Requirements 

  

**Mandatory Runtime Inputs:** 
- User Story file path (must be provided by user at runtime)
- Template file path (must be provided by user at runtime) 
- Navigation Steps file path (must be provided by user at runtime)

**Reference Files for Analysis:** 
- Extracted automatically from user-provided Template path
- Extracted automatically from user-provided Navigation Steps path

**Output Location:** `/workspaces/Ezdocs-Manual/Optimus Core/4_Design Studio/{filename}_TestCases.csv` (auto-generated) 
  

--- 

  

## Goal 

  

Generate manual test cases in CSV format by:
1. Accepting three mandatory file paths at runtime (User Story, Template, Navigation Steps)
2. Analyzing the Template file to extract and replicate EXACT writing pattern and structure
3. Analyzing the User Story and Navigation Steps to identify acceptance criteria and workflows
4. Creating test cases that strictly follow the template pattern while incorporating user story requirements and navigation steps
5. Ensuring all test cases (Positive, Negative, Boundary) follow the same writing style, field mappings, and procedural format as the provided template

Each test case must be atomic, focused, and consistent with the template's approach to test design.

  

--- 

  

## Important Notes 

  

1. **MANDATORY PATHS:** User Story, Template, and Navigation Steps paths MUST be provided at runtime before processing begins

2. **Template Pattern Analysis:** Before generating any test cases, thoroughly analyze the provided Template file to understand:
   - Writing style and tone
   - Action numbering and format consistency
   - Expected Results composition
   - Field naming conventions and data structure

3. Generate exactly one test case per acceptance criterion in the user story 

4. **Follow Template Writing Pattern:** ALL test cases must follow the exact writing pattern, field structure, and format of the provided template

5. **Use Navigation Steps for Accuracy:** Incorporate exact screen names, field labels, and workflow sequences from Navigation_Steps file into test case actions

6. Include only relevant navigation steps based on the specific acceptance criterion scope (Quote only, Binder only, Policy only, or MidTerm only if specified) 

7. Keep test cases atomic and focused on specific validation scenarios 

8. Ensure proper CSV escaping for special characters and multi-line cells (use double quotes) 

9. Number actions sequentially (1., 2., 3., etc.) with line breaks between steps 

10. Write expected results as continuous text WITHOUT numbering, separated by line breaks 

11. Use forward slashes (/) consistently in all file paths 

12. Extract filename from user story path correctly for output file naming (preserve naming convention from source file)

13. **Include positive, negative, and boundary scenarios:** Generate minimum 3 test cases covering all scenario types 

--- 

  

## Output Format: CSV Structure 

  

**CSV Headers:** 

``` 

TC ID,Test type,Test case Name,Description,Actions,Expected Results,Test Repository Path,Status,User story,Scenario Type and Priority 

``` 

  

**CSV Format Rules:** 

1. Each test case is a single row in the CSV 

2. All actions for a test case are combined in the "Actions" column with line breaks between each step 

3. All expected results for a test case are combined in the "Expected Results" column as continuous text 

4. Wrap multi-line cells (Actions and Expected Results) in double quotes 

5. Escape commas within fields using double quotes 

6. Escape double quotes within fields by doubling them ("") 

7. Number actions sequentially (1., 2., 3., etc.) 

8. Expected results should NOT have numbering - keep as plain text 

9. Use actual line breaks within quoted cells or \n for separating action steps 

  

**Example CSV Output:** 

```csv 

TC ID,Test type,Test case Name,Description,Actions,Expected Results,Test Repository Path,Status,User story,Scenario Type and Priority 

``` 

---

--- 


