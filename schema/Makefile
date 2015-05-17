# Paths and filenames for generating API docs from schema
SCHEMA_DIR=.
SCHEMATA_DIR=$(SCHEMA_DIR)/schemata
SCHEMA_FILENAME_ROOT=schema
SCHEMA_FILE=$(SCHEMA_DIR)/$(SCHEMA_FILENAME_ROOT).json
SCHEMA_RENDERED=$(SCHEMA_DIR)/$(SCHEMA_FILENAME_ROOT).md
SCHEMA_METADATA=$(SCHEMA_DIR)/meta.json
SCHEMA_OVERVIEW=$(SCHEMA_DIR)/overview.md

all: schema

schema:
	prmd combine --meta $(SCHEMA_METADATA) $(SCHEMATA_DIR) > $(SCHEMA_FILE)
	prmd verify $(SCHEMA_FILE)
	prmd doc --prepend $(SCHEMA_OVERVIEW) $(SCHEMA_FILE) > $(SCHEMA_RENDERED)
