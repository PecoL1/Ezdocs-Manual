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
 
 
 
### Step 1: Prompt for User Story Path
 
Ask the user:
 
```
 
Please provide the User Story file path : /workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/User Story/EDD-1424.md
 
```
 
 
 
### Step 2: Generate Test Cases and Save CSV File
 
- For each acceptance criterion/scenario in the user story, generate one test case
 
- Create a CSV file with proper structure and multi-line cell formatting (wrap in double quotes)
 
- Number actions sequentially (1., 2., 3., etc.) with line breaks between steps
 
- Write expected results as continuous text WITHOUT numbering
 
- Automatically save the CSV file to: `/workspaces/Ezdocs-Manual/Optimus Core/4_Design Studio/{filename}_TestCases.csv`
 
- Confirm completion with message:
 
```
 
Test cases generated successfully!
 
Output file: /workspaces/Ezdocs-Manual/Optimus Core/4_Design Studio/{filename}_TestCases.csv
Total test cases: {count}
 
```
 
 
 
---
 
 
 
## Input Requirements
 
 
 
**User Story File Path:** Provided by user at runtime
 
**Template Reference:** `/workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/Template/Template_1424.md`
 
**Navigation Reference:** `/workspaces/Ezdocs-Manual/Optimus Core/1_Base_Repo/Reference/Navigation_Steps_1424.md`
 
**Output Location:** `/workspaces/Ezdocs-Manual/Optimus Core/4_Design Studio/{filename}_TestCases.csv` (auto-generated)
 
 
 
---
 
 
 
## Goal
 
 
 
Generate manual test cases in CSV format based on the user story and acceptance criteria. Each test case should follow the template structure and incorporate the CCA application navigation flow from Navigation_Steps_1424.md.
 
 
 
---
 
 
 
## Important Notes
 
 
 
1. Generate exactly one test case per acceptance criterion in the user story
 
2. Include only relevant navigation steps based on the specific acceptance criterion scope 
 
3. Keep test cases atomic and focused on specific validation scenarios
 
4. Ensure proper CSV escaping for special characters and multi-line cells (use double quotes)
 
5. Number actions sequentially (1., 2., 3., etc.) with line breaks between steps
 
6. Write expected results as continuous text WITHOUT numbering, separated by line breaks
 
7. Reference Navigation_Steps_1424.md for accurate EZDocs workflow patterns
 
8. Use Template_1424.md structure for field mapping and test case structure (reference only, not copy values)
 
9. Use forward slashes (/) consistently in all file paths
 
10. Extract filename from user story path correctly for output file naming (e.g., EDD-1424.md → EDD-1424)
 
---
 
 
 
## Output Format: CSV Structure
 
 
 
**CSV Headers:**
 
```
 
TC ID,Test type,Test case Name,Description,Actions,Expected Results,Test Repository Path,Status,User story,Priority
 
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
 
TC ID,Test type,Test case Name,Description,Actions,Expected Results,Test Repository Path,Status,User story,Priority
 
 
```
 
---
 
 
 
 
1. Generate exactly one test case per acceptance criterion in the user story
 
2. Include only relevant navigation steps based on the specific acceptance criterion scope
 
3. Keep test cases atomic and focused on specific validation scenarios
 
4. Ensure proper CSV escaping for special characters and multi-line cells (use double quotes)
 
5. Number actions sequentially (1., 2., 3., etc.) with line breaks between steps
 
6. Write expected results as continuous text WITHOUT numbering, separated by line breaks
 
7. Reference navigation_steps.md for accurate EDD workflow patterns
 
8. Use Template.md structure for field mapping and test case structure
 
9. Use forward slashes (/) consistently in all file paths
 
10. Extract filename from user story path correctly for output file naming (e.g., EDD-1424.md → DD-1424)
 
11.Just refer the Template_1424.md file. Don't use the content or values present in the Template_1424.md file.
 
12.The addition of options in action dropdown will be visible for Complaints Officer not for Customer Care Lead and Customer Care roles.

13. Please include positive and negative scenarios.
---