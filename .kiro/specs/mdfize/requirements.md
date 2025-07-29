# Requirements Document

*Created by Kiro*

## Introduction

This feature refactors the Bento data loader to remove hardcoded ICDC and C3DC models and schemas, replacing them with a generic Model Description Format (MDF) based system. The refactor will enable the data loader to work with any model defined in MDF format as specified by bento-mdf (https://github.com/CBIIT/bento-mdf), making it a truly model-agnostic and reusable data loading platform.

## Requirements

### Requirement 1

**User Story:** As a data engineer working with different cancer research projects, I want the data loader to accept any MDF-formatted model, so that I can use the same tool across multiple projects without code modifications.

#### Acceptance Criteria

1. WHEN an MDF model file is provided THEN the system SHALL parse and validate the model using bento-mdf
2. WHEN the model is loaded THEN the system SHALL generate appropriate database schema and validation rules
3. WHEN processing data files THEN the system SHALL use the MDF model for validation and transformation
4. WHEN multiple MDF models are provided THEN the system SHALL support model composition and inheritance

### Requirement 2

**User Story:** As a developer maintaining the data loader, I want all hardcoded ICDC and C3DC references removed, so that the codebase is clean and model-agnostic.

#### Acceptance Criteria

1. WHEN scanning the codebase THEN the system SHALL contain no hardcoded references to ICDC or C3DC models
2. WHEN the ICDC_Schema class is replaced THEN the system SHALL use a generic MDF-based schema handler
3. WHEN configuration files are updated THEN they SHALL specify MDF model sources instead of hardcoded schemas
4. WHEN documentation is updated THEN it SHALL reflect the model-agnostic nature of the system

### Requirement 3

**User Story:** As a system administrator deploying the data loader, I want to configure which MDF model to use through configuration files, so that I can deploy the same codebase for different projects.

#### Acceptance Criteria

1. WHEN configuring the system THEN I SHALL be able to specify MDF model files or repositories in configuration
2. WHEN the system starts THEN it SHALL load the specified MDF model and validate its structure
3. WHEN model configuration changes THEN the system SHALL reload and apply the new model without code changes
4. WHEN model validation fails THEN the system SHALL provide clear error messages about model issues

### Requirement 4

**User Story:** As a data scientist using the data loader, I want the same data loading capabilities regardless of the underlying model, so that my workflows remain consistent across projects.

#### Acceptance Criteria

1. WHEN using different MDF models THEN the data loading interface SHALL remain consistent
2. WHEN data validation occurs THEN it SHALL use rules defined in the MDF model
3. WHEN relationships are created THEN they SHALL follow the MDF model specifications
4. WHEN data transformation happens THEN it SHALL respect MDF model constraints and types

### Requirement 5

**User Story:** As a developer integrating with the data loader, I want clear APIs for working with MDF models, so that I can extend or customize the system for specific needs.

#### Acceptance Criteria

1. WHEN accessing model information THEN the system SHALL provide a consistent API regardless of the underlying MDF model
2. WHEN extending the system THEN developers SHALL be able to add custom MDF model processors
3. WHEN debugging model issues THEN the system SHALL provide detailed logging about MDF model parsing and validation
4. WHEN testing the system THEN it SHALL support mock MDF models for unit testing

### Requirement 6

**User Story:** As a quality assurance engineer, I want comprehensive testing of MDF model integration, so that I can ensure the refactored system works correctly with various models.

#### Acceptance Criteria

1. WHEN testing the system THEN it SHALL include tests with multiple different MDF models
2. WHEN MDF model validation fails THEN the system SHALL handle errors gracefully and provide useful feedback
3. WHEN performance testing THEN the MDF-based system SHALL perform comparably to the hardcoded version
4. WHEN integration testing THEN the system SHALL work correctly with real-world MDF models from different projects

### Requirement 7

**User Story:** As a developer building and deploying the system, I want the package to use modern Python build tools, so that dependency management and builds are reliable and reproducible.

#### Acceptance Criteria

1. WHEN building the package THEN the system SHALL use uv as the build system
2. WHEN managing dependencies THEN they SHALL be specified in a pyproject.toml file
3. WHEN configuring the build THEN all build configuration SHALL be provided in pyproject.toml
4. WHEN installing dependencies THEN uv SHALL be used for fast and reliable dependency resolution

### Requirement 8

**User Story:** As a documentation maintainer, I want updated documentation that reflects the MDF-based architecture, so that users can understand and use the new system effectively.

#### Acceptance Criteria

1. WHEN documentation is updated THEN it SHALL explain how to use MDF models with the data loader
2. WHEN providing examples THEN they SHALL show real MDF model usage rather than hardcoded schemas
3. WHEN describing configuration THEN it SHALL detail MDF model specification options
4. WHEN troubleshooting guides are created THEN they SHALL cover common MDF model issues and solutions