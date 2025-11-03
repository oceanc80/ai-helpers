---
description: Create a new OpenShift Enhancement Proposal (EP)
argument-hint: [domain]
---

## Name
enhancements:new

## Synopsis
```
/enhancements:new [domain]
```

## Description
The `enhancements:new` command guides you through creating a new OpenShift Enhancement Proposal (EP) in your local fork of the openshift/enhancements repository. It follows the official enhancement template and prompts for all required information interactively.

## Implementation

### 1. Verify Repository Location

Check if the current directory is within the openshift/enhancements repository:
```bash
git remote -v | grep -E "openshift/enhancements|[your-fork]/enhancements"
```

If not in the repository, prompt the user for the path to their local fork:
- Use the AskUserQuestion tool to ask: "Where is your local fork of openshift/enhancements located?"
- Change to that directory before proceeding

### 2. Locate the Template

Use the local enhancement template from the repository:
```bash
# Find the template in the repository
find . -path "*/guidelines/enhancement_template.md"
```

The template should be located at `guidelines/enhancement_template.md` in the enhancements repository.

### 3. Gather Required Information

Explicitly ask the user for the following information:

**Basic Information:**
- Enhancement title (will be used for filename)
- Enhancement domain (if not provided as argument)
  - Show available domains: agent-installer, api-review, art, authentication, autoscaling, baremetal, builds, cert-manager, cloud-integration, cluster-api, cluster-logging, cluster-scope-secret-volumes, console, dns, etcd, external-secrets-operator, fedramp, helm3, hypershift, image-registry, ingress, insights, installer, kube-apiserver, kubelet, local-storage, machine-api, machine-config, manifestlist, microshift, monitoring, multi-arch, network, node-pull-credentials, node-tuning, observability, oc, ocp-coreos-layering, olm, operator-sdk, platforms, proxy, release, rhcos, samples, sandboxed-containers, scheduling, security, service-catalog, single-node, storage, subscription-content, support-log-gather, test-platform, testing, two-node-fencing, update, vertical-pod-autoscaler, windows-containers, worker-latency-profile, workload-identity-management, workload-partitioning
- **Author name(s)** - Explicitly ask the user to provide a list of authors. Authors should be in the format `@github-username`. Multiple authors should be collected as a comma-separated list or one per line.
- Brief summary of the enhancement (1-2 sentences)

### 4. Create the Filename

Generate the filename following the repository conventions:
- Take the enhancement title
- Convert to lowercase
- Replace spaces and punctuation with hyphens
- Example: "Add New Feature" → "add-new-feature.md"

### 5. Populate the Template

Read the template and update the following sections with user-provided information:
- `title:` - The enhancement title
- `authors:` - The author name(s)
- `creation-date:` - Today's date in YYYY-MM-DD format
- `last-updated:` - Today's date in YYYY-MM-DD format
- `summary` section - The brief summary provided by the user

Keep all other sections as placeholders with instructions for the user to fill in later.

### 6. Create the Enhancement File

Write the populated template to the correct location:
```
enhancements/{domain}/{filename}
```

Example: `enhancements/network/add-new-feature.md`

### 7. Create a Feature Branch

Create a new git branch for this enhancement:
```bash
git checkout -b enhancement/{domain}/{short-name}
```

Example: `git checkout -b enhancement/network/add-new-feature`

### 8. Stage the New File

Add the new enhancement file to git:
```bash
git add enhancements/{domain}/{filename}
```

### 9. Provide Next Steps

Display the following guidance to the user:

```
Enhancement proposal created successfully!

Location: enhancements/{domain}/{filename}
Branch: enhancement/{domain}/{short-name}

Next steps:
1. Open the file and fill in the remaining sections:
   - Motivation and user stories
   - Goals and non-goals
   - Proposal details
   - Risks and mitigations
   - Test plan
   - Graduation criteria

2. Review the enhancement template guidelines:
   https://github.com/openshift/enhancements/blob/master/guidelines/enhancement_template.md

3. When ready, commit your changes:
   git commit -m "Add {title} enhancement proposal"

4. Push to your fork and create a pull request:
   git push -u origin enhancement/{domain}/{short-name}

5. Engage with reviewers and iterate on the proposal
```

## Return Value
- **Format**: Confirmation message with the file location and next steps
- **Output**: The enhancement file path and git branch name

## Examples

1. **Create an enhancement with domain specified**:
   ```
   /enhancements:new network
   ```
   This will prompt for title, author, and summary, then create the enhancement in the `enhancements/network/` directory.

2. **Create an enhancement without domain**:
   ```
   /enhancements:new
   ```
   This will prompt for the domain selection along with other required information.

## Arguments
- `$1` (optional): The domain/subdirectory where the enhancement belongs. If not provided, the user will be prompted to select one.

## Prerequisites

1. **Local Fork**: You must have a local fork of https://github.com/openshift/enhancements
2. **Git**: Git must be installed and configured
3. **curl**: For downloading the template

## Notes

- The command creates a feature branch automatically following the naming convention `enhancement/{domain}/{short-name}`
- The template includes all required sections with helpful comments and instructions
- Reviewers and approvers can be added later through the GitHub pull request process
- The enhancement file follows the repository's naming conventions (lowercase, hyphenated)
