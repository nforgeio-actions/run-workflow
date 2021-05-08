# start-workflow

**INTERNAL USE ONLY:** This GitHub action is not intended for general use.  The only reason why this repo is public is because GitHub requires it.

Used to start a workflow from within another workflow.  Note that the target workflow must support the **workflow_dispatch** event.

## Examples

**Start a workflow with no inputs:**
```
steps:
- uses: nforgeio-actions/start-workflow@master
  with: 
    repo: nforgeio/neonCLOUD
    workflow: my-workflow
```

**Run a workflow with a manually generated JSON input:**
```
steps:
- uses: nforgeio-actions/start-workflow@master
  with: 
    repo: nforgeio/neonCLOUD
    workflow: my-workflow
    inputs: |
      my-arg: my-value
```

**Start a workflow with multiple inputs:**
```
steps:

**Construct the JSON arguments to be passed as inputs to the new workflow run:**

- uses: nforgeio-actions/start-workflow@master
  with: 
    repo: nforgeio/neonCLOUD                    # Specifies the target workflow's repo
    workflow: my-workflow                       # Identifies the target workflow by name
    inputs: |
      my-arg1: my-value1
      my-arg2: "my-value2"
```

**Start a workflow on a non-master branch:**

- uses: nforgeio-actions/start-workflow@master
  with: 
    repo: nforgeio/neonCLOUD                    # Specifies the target workflow's repo
    workflow: my-workflow                       # Identifies the target workflow by name
    branch: jeff                                # Branch holding the target workflow
```
