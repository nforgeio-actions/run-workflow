# run-workflow

**INTERNAL USE ONLY:** This GitHub action is not intended for general use.  The only reason why this repo is public is because GitHub requires it.

Used to run a workflow from within another workflow.  Note that the target workflow must support the **workflow_dispatch** event.

## Examples

**Run a workflow with no inputs:**
```
steps:
- uses: nforgeio-actions/run-workflow@master
  with: 
    repo: nforgeio/neonCLOUD
    workflow: my-workflow
```

**Run a workflow with a manually generated JSON input:**
```
steps:
- uses: nforgeio-actions/run-workflow@master
  with: 
    repo: nforgeio/neonCLOUD
    workflow: my-workflow
    inputs: "{\"arg\":\"my value\"}"    # <--- ugly?
```

**Run a workflow with a generated JSON inputs:**
```
steps:

**Construct the JSON arguments to be passed as inputs to the new workflow run:**

- id: arg-0
  uses: nforgeio-actions/input-builder@master
  with:
    name: "arg0"
    value: "value of arg 0"
- id: arg-1
  uses: nforgeio-actions/input-builder@master
  with:
    name: "arg1"
    value: "value of arg 1"
    json: ${{ steps.arg-0.outputs.json }}       # Note how we're chaining the output of the previous arg
- id: arg-2
  uses: nforgeio-actions/input-builder@master
  with:
    name: "arg2""
    value: "value of arg 2"
    json: ${{ steps.arg-1.outputs.json }}        # Note how we're chaining the output of the previous arg

**Schedule a workflow, passing the arguments:**

- uses: nforgeio-actions/run-workflow@master
  with: 
    repo: nforgeio/neonCLOUD                    # Specifies the target workflow's repo
    workflow: my-workflow                       # Identifies the target workflow by name
    inputs: ${{ steps.arg-2.outputs.json }}     # Obtain the JSON from the last input-builder step
```

**Schedule a workflow on a non-master branch:**

- uses: nforgeio-actions/run-workflow@master
  with: 
    repo: nforgeio/neonCLOUD                    # Specifies the target workflow's repo
    workflow: my-workflow                       # Identifies the target workflow by name
    branch: jeff                                # Branch holding the target workflow
```
