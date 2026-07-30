# _ROOT Documentation Index

## Overview
This documentation area defines the **Crane Migration Tool's** transformation pipeline, resource compatibility standards, and validation procedures. It serves as the definitive guide for engineers performing cluster migrations using the `crane` CLI, covering everything from the multi-stage Kustomize architecture to pre-deployment manifest validation and environment-specific troubleshooting.

## Files Summary
* **kustomize-multistage.md**: Describes the sequential multi-stage Kustomize pipeline, including directory structure, plugin prioritization, stage chaining, and the "dirty check" mechanism.
* **CRANE_COMPATIBILITY_MATRIX.md**: Outlines the scope of migration support for various Kubernetes resources, distinguishing between fully supported namespace-scoped objects and conditionally supported cluster-scoped infrastructure.
* **pre-apply-validation-guide.md**: Provides a comprehensive checklist and script for validating rendered manifests against a target cluster to prevent partial deployments or permission errors.
* **transform.md**: Details the internal structure of the `transform/` directory, including how to manage manual edits, pass-through stages, and the workflow for integrating custom plugins.
* **stateless-migration-quickstart.md**: Offers an end-to-end tutorial for the standard Crane migration workflow, encompassing export, transform, apply, and validate phases.

## Code Changes That Would Require Documentation Updates
* **Pipeline Schema Changes**: Any modification to the `transform/` directory layout, `kustomization.yaml` requirements, or the `[priority]_[plugin-name]` naming convention.
* **CLI Flag Additions/Removals**: Changes to `crane transform`, `crane apply`, or `crane export` flags (e.g., modifying how `--force` or `--stage` works).
* **Plugin System Updates**: Changes to how plugins are loaded, how priorities are calculated, or how they interact with the transformation chain.
* **Compatibility Logic**: Updates to which resources are automatically white-listed or excluded during the `export` or `transform` phases.
* **Validation/Dry-Run Logic**: Modifications to the `kubectl` checks, API compatibility validation, or the logic within the `validate` command.
* **New Intermediate Stages**: Changes to the automated staging behavior (e.g., adding automatic pre- or post-processing stages).

## Key Technical Concepts
* **Multi-Stage Pipeline**: Sequential transformation using `[priority]_[plugin-name]` directories.
* **Kustomize Integration**: Using `kustomization.yaml` and `patches/` to modify exported resources.
* **Dirty Check**: Protection mechanism that prevents overwriting user-modified stages without `--force`.
* **Resource Whiteout**: The process of excluding unwanted cluster-specific metadata or resources.
* **Server-Side Dry-Run**: Using `kubectl apply --dry-run=server` for real-time validation against the target cluster API.
* **Pass-Through Stages**: Non-plugin stages used for manual YAML editing.
* **RBAC Context**: Requirements for `get`/`create` permissions on cluster-scoped resources.
* **Namespace-Scoped vs. Cluster-Scoped**: Classification logic for determining migration eligibility.

## Related Components
* **`crane-lib`**: The underlying library for plugins and transformation utilities.
* **`kubectl` / `oc`**: The primary external tools used for validation and application.
* **Kustomize**: The engine used to render final manifests.
* **Export/Import Subsystems**: The core components responsible for resource discovery and serialization.
* **Validation Module**: The subsystem responsible for live cluster compatibility checks.