### Placeholder

Current functionality:
- create_target_dataset
  - input: target (str), mapping_name (str, default 'original'), overview_name (str, default 'original', hf_token (str, default None)
  - takes a valid target, downloads, processes and combines all available datasets for the target and returns a single dataset df with text, target and source columns. some datasets are only available if providing a valid huggingface token or uploading the raw data to input_folder. uses the specified mapping, taxononmy and overview for the creation of the dataset, defaulting to the original versions.
  - output: target_dataset (df) 
- create_category_dataset
  - input: category (str), mapping_name (str, default 'original'), taxonomy_name (str, default 'original', overview_name (str, default 'original'), hf_token (str, default None)
  - takes a valid category, downloads, processes and combines all available datasets for the targets in that category and returns a single dataset df with text, target and source columns. some datasets are only available if providing a valid huggingface token or uploading the raw data to input_folder. uses the specified mapping, taxononmy and overview for the creation of the dataset, defaulting to the original versions.
  - output: target_dataset (df)
- get_target_info
  - input: target (str), overview_name (str, default 'original')
  - takes a valid target and returns an overview of the datasets from which the target is available, the number of instances for the target in the dataset as well as the access requirements for the dataset. if the dataset is not readily available there is also information on how to access the dataset. uses the specified overview for the provided information, defaulting to the original version.
  - output: none
- get_category_info
  - input: category (str), overview_name (str, default 'original'), taxonomy_name (str, default 'original')
  - takes a valid category and returns an overview of the targets and the corresponding number of instances within the category, an overview of the datasets from which the targets are available and the corresponding number of instances per dataset, as well as the access requirements for the dataset. if the dataset is not readily available there is also information on how to access the dataset. uses the specified taxonomy and overview for the provided information, defaulting to the original versions.
  - output: none
- update_mapping_specific
  - input: mapping_change ({dataset_name: {key_original: value_new}}), mapping_name (str, default 'modified')
  - updates the specified mapping (either newly created if mapping_name non-existent or updating if mapping_name already created earlier) per dataset according to the provided dictionary. referring to the original mapping, users may map the key_original found in the original dataset_name to new targets (value_new). e.g., {'fanton_2021': {'POC': 'blacks'}} would map instances in dataset 'fanton_2021' that have the key_original 'POC' to value_new 'blacks' (originally, these are mapped to 'race_unspecified'). stores the resulting mapping with name 'mapping_name'. requires existing key_original (keys in original datasets) and value_new (targets) - refer to original mapping to identify valid values.
  - output: mapping_dict (df) 
- update_mapping_all
  - input: mapping_change ({key_original: value_new}), mapping_name (str, default 'modified')
  - updates the specified mapping (either newly created if mapping_name non-existent or updating if mapping_name already created earlier) across datasets according to the provided dictionary. referring to the original mapping, users may map the key_original found in different datasets to new targets (value_new). e.g., {'africans': 'origin_unspecified'} would map instances in any dataset that have the key_original 'africans' to value_new 'origin_unspecified' (originally, these are mapped to 'blacks'). stores the resulting mapping with name 'mapping_name'. requires existing key_original (keys in original datasets) and value_new (targets) - refer to original mapping to identify valid values.
  - output: mapping_dict (df) 
- update_taxonomy
- update_overview
- add_target
