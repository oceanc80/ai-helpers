# Enhancements Plugin

A Claude Code plugin for managing OpenShift Enhancement Proposals (EPs) in the [openshift/enhancements](https://github.com/openshift/enhancements) repository.

## Overview

This plugin streamlines the process of creating and managing OpenShift Enhancement Proposals by automating template setup, ensuring proper file naming conventions, and guiding users through the enhancement creation process.

## Commands

### `/enhancements:new [domain]`

Create a new OpenShift Enhancement Proposal following the official template and guidelines.

**Features:**
- Interactive prompts for required information (title, domain, author, summary)
- Automatically downloads the latest enhancement template
- Generates properly formatted filenames (lowercase, hyphenated)
- Creates a feature branch following repository conventions
- Populates metadata (title, authors, dates, summary)
- Stages the new file in git
- Provides clear next steps for completing the proposal

**Usage:**
```bash
# With domain specified
/enhancements:new network

# Without domain (will prompt for selection)
/enhancements:new
```

**Prerequisites:**
- Local fork of https://github.com/openshift/enhancements
- Git installed and configured
- curl for downloading the template

**Example Workflow:**
1. Run `/enhancements:new network`
2. Provide enhancement title: "Multi-Network Policy Support"
3. Provide author name: "John Doe"
4. Provide brief summary: "Add support for network policies across multiple networks"
5. The command creates:
   - File: `enhancements/network/multi-network-policy-support.md`
   - Branch: `enhancement/network/multi-network-policy-support`
6. Fill in remaining sections of the enhancement proposal
7. Commit, push, and create a pull request

## Available Domains

The enhancements repository supports the following domains:

- agent-installer
- api-review
- art
- authentication
- autoscaling
- baremetal
- builds
- cert-manager
- cloud-integration
- cluster-api
- cluster-logging
- console
- dns
- etcd
- hypershift
- ingress
- installer
- kube-apiserver
- machine-config
- monitoring
- network
- oc
- olm
- security
- storage
- update
- and many more...

See the [enhancements directory](https://github.com/openshift/enhancements/tree/master/enhancements) for the complete list.

## Enhancement Template Structure

The enhancement template includes the following sections:

- **Metadata**: Title, authors, reviewers, approvers, dates
- **Summary**: Brief overview of the enhancement
- **Motivation**: User stories, goals, and non-goals
- **Proposal**: Detailed design and implementation details
- **Risks and Mitigations**: Potential issues and how to address them
- **Alternatives**: Other approaches considered
- **Test Plan**: How the enhancement will be tested
- **Graduation Criteria**: Criteria for moving from dev-preview to GA
- **Upgrade/Downgrade Strategy**: Compatibility considerations
- **Operational Aspects**: How the enhancement affects operations

## Resources

- [Enhancement Template](https://github.com/openshift/enhancements/blob/master/guidelines/enhancement_template.md)
- [Enhancement Process](https://github.com/openshift/enhancements)
- [Contributing Guidelines](https://github.com/openshift/enhancements/blob/master/CONVENTIONS.md)

## Contributing

To add new commands to this plugin:

1. Create a new `.md` file in `plugins/enhancements/commands/`
2. Follow the command definition format in `CLAUDE.md`
3. Test the command locally
4. Submit a pull request

## Support

For issues or questions:
- Repository: https://github.com/openshift-eng/ai-helpers
- Enhancement Repo: https://github.com/openshift/enhancements
