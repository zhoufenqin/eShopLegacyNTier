---
name: dotnet-upgrade-assessment
description: Runs .NET upgrade assessment only. Does not create plans, execute upgrades, or modify source code.
---

# .NET Upgrade Assessment Skill

This skill runs a .NET upgrade assessment using the AppModDotNetUpgrade MCP server. It performs ONLY assessment — no plans, no code changes, no upgrades.

## Input Parameters

- `workspace-path` (optional): Path to the project root containing the `.sln` or `.slnx` file. Defaults to `.` (current directory). For a repository with multiple solutions, pass the solution folder path.
- `assessment_dir` (required): Absolute path to the assessment output directory where the MCP server writes results.
- `target-framework` (optional): Target .NET framework version for upgrade (e.g., `net8`, `net9`, `net10`).

## Prerequisites — ua-settings.json Setup

Before calling any MCP tools, you MUST create the settings file and export the environment variable:

```bash
mkdir -p {workspace-path}/.github/modernize
cat > {workspace-path}/.github/modernize/ua-settings.json << 'EOF'
{
  "outputPath": "{assessment_dir}"
}
EOF
export UA_SETTINGS_FILE_PATH="$(realpath {workspace-path}/.github/modernize/ua-settings.json)"
```

Replace `{workspace-path}` and `{assessment_dir}` with the actual parameter values provided by the caller.

## Execution Steps

Execute these steps IN ORDER. Do NOT skip any step. Do NOT deviate from this sequence.

### Step 1: Call `get_state()`

Call the MCP tool `get_state()` to initialize the workflow state.

### Step 2: Call `get_scenarios()`

Call the MCP tool `get_scenarios()`. From the response, identify the scenario for ".NET version upgrade" and note its `scenarioId`.

### Step 3: Call `initialize_scenario`

Call the MCP tool `initialize_scenario` with:
- `scenarioId`: the ID found in Step 2
- `description`: "Upgrade assessment for {solution file name}"

### Step 4: Find the solution file

Look for `.sln` or `.slnx` files in `{workspace-path}`. Use the first one found.

### Step 5: Call `generate_dotnet_upgrade_assessment`

Call the MCP tool `generate_dotnet_upgrade_assessment` with:
- `inputMode`: `"solution"`
- `paths`: the full path to the solution file found in Step 4

If `target-framework` was provided as an input parameter, pass it as well.

### Step 6: Return the result

Report the assessment output file path. STOP.

## Cleanup

After the assessment completes (whether successful or failed), remove the settings file:

```bash
rm -f {workspace-path}/.github/modernize/ua-settings.json
```

## Rules

- **ALL work MUST go through MCP tool calls.** Do NOT analyze code yourself.
- **Do NOT create plans or modify source files.** This is assessment only.
- **Do NOT ask for user input.** Run all steps in one session without pausing.
- **If a tool call fails, report the exact error.** Do NOT work around it or retry with different parameters.
- **Do NOT load additional skills or instructions.** Follow only the steps above.
- **Do NOT call `get_instructions`, `start_task`, `complete_task`, `break_down_task`, or any task/workflow management tools.** Those are for upgrade execution, not assessment.
- **Do NOT create git branches, commits, or source control operations.**
- **Do NOT read or analyze source code files.** The MCP tools handle all analysis internally.
