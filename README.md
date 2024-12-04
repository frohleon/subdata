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
  - input: taxonomy_change ({target: (old_category, new_category)}), taxonomy_name (str, default 'modified')
  - updates the specified taxonomy (either newly created if taxonomy_name non-existent or updating if taxonomy_name already created earlier), moving the specified target from old_category to new_category. if new_category == None, then the target will effectively be removed from the updated taxonomy. if new_category (str) not found in specified taxonomy, a new category with name new_category will be added to the updated taxonomy. e.g., {'jews': ('religion', 'race')} will move target 'jews' from category 'religion' to category 'race'. e.g., {'jews': ('religion', None)} will remove target 'jews' from taxonomy. e.g., {'jews': ('religion', 'relevant'), 'blacks': ('race', 'relevant'} will move targets 'jews' and 'blacks' into newly created category 'relevant'.
  - output: taxonomy_dict (df)
- add_target
  - input: target (str), target_category (str), target_keywords [list of str], mapping_name (str, default 'modified'), taxonomy_name (str, default 'modified')
  - creates a new target and moves it into specified target_category for the specified taxonomy (either newly created if taxonomy_name non-existent or updating if taxonomy_name already created earlier), mapping all original keywords specified in target_keywords to the new target for the specified mapping (either newly created if mapping_name non-existent or updating if mapping_name already created earlier). the target_category and target_keywords must already be existing - please refer to the taxonomy and the mapping to identify a valid target_category and valid target_keywords. e.g., target='disabled_general', target_category='disability', target_keywords=['disabled_unspecified','disabled','disabled_other'] creates new target 'disabled_general' in category 'disability' and maps the specified keywords to the newly created target.
  - output: mapping_dict (df)
- update_overview
  - input: overview_name (str, default 'modified'), mapping_name (str, default 'modified'), taxonomy_name (str, defaut 'modified'), hf_token (str, default None)
  - updates the overview that informs the get_info and create_dataset functions and stores the new overview with name overview_name. uses the mapping and taxonomy provided via mapping_name and taxonomy_name to create the updated overview. internally, the function tries to access all datasets to create the full overview, thus requiring a hf_token and the manual upload of relevant datasets into input_folder to consider all available datasets. function should be called after any operation that modifies the mapping or the taxonomy.    

