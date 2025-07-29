# Implementation Plan

<!-- Created by Kiro -->

- [ ] 1. Set up build system and MDF integration foundation

  - Migrate to uv build system with pyproject.toml configuration
  - Add bento-mdf dependency and create SchemaAdapter class to replace ICDC_Schema
  - Update configuration system to specify MDF model files instead of hardcoded schemas
  - _Requirements: 1.1, 3.1, 3.2, 7.1, 7.2_

- [ ] 1.1 Migrate to uv build system with pyproject.toml

  - Create pyproject.toml file with project metadata and dependencies
  - Configure uv as the build system and dependency manager
  - Replace bento submodule with Git dependency in pyproject.toml pointing to bento-common repository
  - Remove requirements.txt and migrate all dependencies to pyproject.toml
  - Remove .gitmodules and bento submodule directory
  - _Requirements: 7.1, 7.2, 7.3_

- [ ] 1.2 Add bento-mdf dependency to project

  - Add bento-mdf package to pyproject.toml dependencies
  - Test bento-mdf import and basic MDF class functionality
  - _Requirements: 1.1_

- [ ] 1.3 Create SchemaAdapter class to wrap bento-mdf MDF

  - Write new schema_adapter.py module to replace icdc_schema.py
  - Implement SchemaAdapter class that uses bento-mdf MDF class and model attribute
  - _Requirements: 1.1, 1.2_

- [ ] 1.4 Update configuration system for MDF model specification

  - Modify configuration files to specify MDF model file paths instead of hardcoded schemas
  - Update BentoConfig class to handle MDF model configuration parameters
  - _Requirements: 3.1, 3.2_

- [ ] 2. Replace ICDC_Schema with SchemaAdapter in core components

  - Update DataLoader, FileLoader, and main loader components to use SchemaAdapter
  - Modify all imports and instantiations to use new MDF-based schema system
  - _Requirements: 1.3, 2.1, 2.2_

- [ ] 2.1 Update DataLoader class for MDF compatibility

  - Replace ICDC_Schema imports with SchemaAdapter in data_loader.py
  - Modify node and relationship creation methods to use MDF.model.nodes and MDF.model.edges
  - _Requirements: 1.3, 4.3_

- [ ] 2.2 Update FileLoader class for MDF compatibility

  - Replace ICDC_Schema usage with SchemaAdapter in file_loader.py
  - Modify file processing logic to work with MDF model structure
  - _Requirements: 1.3, 4.1_

- [ ] 2.3 Update main loader script for MDF integration

  - Modify loader.py to instantiate SchemaAdapter instead of ICDC_Schema
  - Update schema loading to use MDF model files from configuration
  - _Requirements: 1.3, 3.2_

- [ ] 3. Update data validation logic to use MDF model constraints

  - Modify validation methods to use MDF.model structure for property and constraint checking
  - Replace hardcoded validation rules with MDF model-driven validation
  - _Requirements: 1.2, 4.2, 4.4_

- [ ] 3.1 Implement MDF-based property validation

  - Update property type checking to use MDF.model.props for property definitions
  - Modify data cleaning and transformation to respect MDF property constraints
  - _Requirements: 4.2_

- [ ] 3.2 Implement MDF-based node validation

  - Update node validation to use MDF.model.nodes for required properties and constraints
  - Modify node creation logic to follow MDF node specifications
  - _Requirements: 4.2, 4.3_

- [ ] 3.3 Implement MDF-based relationship validation

  - Update relationship validation to use MDF.model.edges for relationship definitions
  - Modify relationship creation to follow MDF edge specifications and multiplicity
  - _Requirements: 4.3_

- [ ] 4. Update ESLoader for MDF model compatibility

  - Modify Elasticsearch index creation and query generation to use MDF model structure
  - Replace hardcoded index mappings with MDF model-driven mappings
  - _Requirements: 1.3, 4.1_

- [ ] 4.1 Update index creation for MDF models

  - Modify index mapping generation to use MDF.model.nodes and properties
  - Update field type mapping to use MDF property type definitions
  - _Requirements: 4.1_

- [ ] 4.2 Update query generation for MDF models

  - Modify Cypher query generation to use MDF model node and edge names
  - Update query logic to work with any MDF model structure
  - _Requirements: 4.1_

- [ ] 5. Update plugin system for MDF compatibility

  - Modify loader plugins to work with SchemaAdapter instead of ICDC_Schema
  - Update plugin interfaces to use MDF.model for node and relationship access
  - _Requirements: 1.3, 5.2_

- [ ] 5.1 Update IndividualCreator plugin for MDF

  - Replace ICDC_Schema usage with SchemaAdapter in individual_creator.py
  - Modify plugin logic to use MDF.model.nodes for node type checking
  - _Requirements: 5.2_

- [ ] 5.2 Update VisitCreator plugin for MDF

  - Replace ICDC_Schema usage with SchemaAdapter in visit_creator.py
  - Modify plugin logic to use MDF.model for relationship and property access
  - _Requirements: 5.2_

- [ ] 6. Remove hardcoded ICDC and C3DC references throughout codebase

  - Scan codebase for hardcoded ICDC/C3DC references and replace with generic MDF-based code
  - Update variable names, comments, and documentation to be model-agnostic
  - _Requirements: 2.1, 2.2, 2.3_

- [ ] 6.1 Remove hardcoded references in core modules

  - Update data_loader.py, loader.py, and file_loader.py to remove ICDC/C3DC specific code
  - Replace hardcoded node types and property names with MDF model lookups
  - _Requirements: 2.1, 2.2_

- [ ] 6.2 Remove hardcoded references in configuration files

  - Update all YAML configuration files to remove C3DC-specific settings
  - Replace hardcoded model references with MDF model file specifications
  - _Requirements: 2.2, 3.1_

- [ ] 6.3 Remove hardcoded references in utility modules

  - Update utility functions and helper classes to be model-agnostic
  - Remove any ICDC/C3DC specific constants or hardcoded values
  - _Requirements: 2.1, 2.2_

- [ ] 7. Update configuration files to use MDF model specifications

  - Modify all configuration files to specify MDF model files instead of hardcoded schemas
  - Update example configurations to demonstrate MDF model usage
  - _Requirements: 2.4, 3.1, 3.3_

- [ ] 7.1 Update main configuration files

  - Modify config.yml and related files to specify MDF model file paths
  - Remove C3DC-specific configuration sections and replace with generic MDF settings
  - _Requirements: 3.1, 3.2_

- [ ] 7.2 Update properties configuration files

  - Replace props-c3dc.yml with generic props.yml that works with any MDF model
  - Update property file structure to be model-agnostic
  - _Requirements: 3.1_

- [ ] 7.3 Update Elasticsearch configuration files

  - Modify es_indices_c3dc.yml to be generic and work with any MDF model
  - Update index definitions to use MDF model structure instead of hardcoded schemas
  - _Requirements: 3.1_

- [ ] 8. Create comprehensive test suite for MDF integration

  - Write unit tests for SchemaAdapter class and MDF model integration
  - Create integration tests with multiple different MDF models
  - _Requirements: 6.1, 6.2, 6.3_

- [ ] 8.1 Write unit tests for SchemaAdapter class

  - Test MDF model loading and property/relationship extraction
  - Test data validation using MDF model constraints
  - _Requirements: 6.1_

- [ ] 8.2 Write integration tests for MDF model compatibility

  - Test complete data loading pipeline with different MDF models
  - Test system behavior with various MDF model complexities
  - _Requirements: 6.2, 6.4_

- [ ] 8.3 Write performance tests for MDF-based system

  - Compare performance of MDF-based system against original hardcoded version
  - Test system performance with large and complex MDF models
  - _Requirements: 6.3_

- [ ] 9. Update documentation to reflect MDF-based architecture

  - Update README.md and all documentation files to describe MDF model usage
  - Create guides for using different MDF models with the data loader
  - _Requirements: 2.4, 7.1, 7.2, 7.3_

- [ ] 9.1 Update main documentation files

  - Rewrite README.md to describe the Bento data loader as model-agnostic
  - Update module documentation to explain MDF model integration
  - _Requirements: 7.1, 7.2_

- [ ] 9.2 Create MDF model usage guides

  - Write documentation explaining how to use different MDF models
  - Create examples showing MDF model configuration and usage
  - _Requirements: 7.2, 7.3_

- [ ] 9.3 Update API documentation

  - Update code documentation to reflect SchemaAdapter and MDF integration
  - Document new configuration options for MDF model specification
  - Document uv build system usage and pyproject.toml configuration
  - _Requirements: 7.3, 8.3_

- [ ] 10. Validate system with real-world MDF models

  - Test the refactored system with actual MDF models from different cancer research projects
  - Ensure compatibility and performance with production MDF models
  - _Requirements: 6.4, 7.1_

- [ ] 10.1 Test with sample MDF models

  - Create or obtain sample MDF models for testing
  - Validate that data loading works correctly with these models
  - _Requirements: 6.4_

- [ ] 10.2 Performance validation with real MDF models

  - Test system performance with production-scale MDF models
  - Ensure loading times and resource usage are acceptable
  - _Requirements: 6.3_

- [ ] 10.3 End-to-end validation
  - Run complete data loading workflows with different MDF models
  - Verify that Neo4j database structure matches MDF model specifications
  - _Requirements: 6.4_
