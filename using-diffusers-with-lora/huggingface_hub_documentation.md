[](#huggingface_hub.HfApi)Hugging Face Hub API
==============================================

Below is the documentation for the `HfApi` class, which serves as a Python wrapper for the Hugging Face Hub’s API.

All methods from the `HfApi` are also accessible from the package’s root directly, both approaches are detailed below.

The following approach uses the method from the root of the package:

Copied

from huggingface\_hub import list\_models

models = list\_models()

The following approach uses the `HfApi` class:

Copied

from huggingface\_hub import HfApi

hf\_api = HfApi()
models = hf\_api.list\_models()

Using the `HfApi` class directly enables you to set a different endpoint to that of the Hugging Face’s Hub.

### class huggingface\_hub.HfApi

[](#huggingface_hub.HfApi)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L474)

( endpoint = None )

#### create\_repo

[](#huggingface_hub.HfApi.create_repo)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1222)

( repo\_id: str = Nonetoken: typing.Optional\[str\] = Noneorganization: typing.Optional\[str\] = Noneprivate: typing.Optional\[bool\] = Nonerepo\_type: typing.Optional\[str\] = Noneexist\_ok: typing.Optional\[bool\] = Falsespace\_sdk: typing.Optional\[str\] = Nonename: typing.Optional\[str\] = None ) → `str`

Parameters

*   [](#huggingface_hub.HfApi.create_repo.repo_id)**repo\_id** (`str`) — A namespace (user or an organization) and a repo name separated by a `/`.
    
    Version added: 0.5
    
*   [](#huggingface_hub.HfApi.create_repo.token)**token** (`str`, _optional_) — An authentication token \[1\]\_.
*   [](#huggingface_hub.HfApi.create_repo.private)**private** (`bool`, _optional_) — Whether the model repo should be private.
*   [](#huggingface_hub.HfApi.create_repo.repo_type)**repo\_type** (`str`, _optional_) — Set to `"dataset"` or `"space"` if uploading to a dataset or space, `None` or `"model"` if uploading to a model. Default is `None`.
*   [](#huggingface_hub.HfApi.create_repo.exist_ok)**exist\_ok** (`bool`, _optional_, defaults to `False`) — If `True`, do not raise an error if repo already exists.
*   [](#huggingface_hub.HfApi.create_repo.space_sdk)**space\_sdk** (`str`, _optional_) — Choice of SDK to use if repo\_type is “space”. Can be “streamlit”, “gradio”, or “static”.

Returns

`str`

URL to the newly created repo.

Create an empty repo on the HuggingFace Hub.

References:

*   \[1\] [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

#### dataset\_info

[](#huggingface_hub.HfApi.dataset_info)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1174)

( repo\_id: strrevision: typing.Optional\[str\] = Nonetoken: typing.Optional\[str\] = Nonetimeout: typing.Optional\[float\] = None ) → `DatasetInfo`

Parameters

*   [](#huggingface_hub.HfApi.dataset_info.repo_id)**repo\_id** (`str`) — A namespace (user or an organization) and a repo name separated by a `/`.
*   [](#huggingface_hub.HfApi.dataset_info.revision)**revision** (`str`, _optional_) — The revision of the dataset repository from which to get the information.
*   [](#huggingface_hub.HfApi.dataset_info.token)**token** (`str`, _optional_) — An authentication token \[1\]\_.
*   [](#huggingface_hub.HfApi.dataset_info.timeout)**timeout** (`float`, _optional_) — Whether to set a timeout for the request to the Hub.

Returns

`DatasetInfo`

The dataset repository information.

Get info on one specific dataset on huggingface.co

Dataset can be private if you pass an acceptable token.

References:

*   \[1\] [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

#### delete\_file

[](#huggingface_hub.HfApi.delete_file)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1734)

( path\_in\_repo: strrepo\_id: strtoken: typing.Optional\[str\] = Nonerepo\_type: typing.Optional\[str\] = Nonerevision: typing.Optional\[str\] = None )

Parameters

*   [](#huggingface_hub.HfApi.delete_file.path_in_repo)**path\_in\_repo** (`str`) — Relative filepath in the repo, for example: `"checkpoints/1fec34a/weights.bin"`
*   [](#huggingface_hub.HfApi.delete_file.repo_id)**repo\_id** (`str`) — The repository from which the file will be deleted, for example: `"username/custom_transformers"`
*   [](#huggingface_hub.HfApi.delete_file.token)**token** (`str`, _optional_) — Authentication token, obtained with `HfApi.login` method. Will default to the stored token.
*   [](#huggingface_hub.HfApi.delete_file.repo_type)**repo\_type** (`str`, _optional_) — Set to `"dataset"` or `"space"` if the file is in a dataset or space, `None` or `"model"` if in a model. Default is `None`.
*   [](#huggingface_hub.HfApi.delete_file.revision)**revision** (`str`, _optional_) — The git revision to commit from. Defaults to the head of the `"main"` branch.

Deletes a file in the given repo.

Raises the following errors:

*   [`HTTPError`](https://2.python-requests.org/en/master/api/#requests.HTTPError) if the HuggingFace API returned an error
*   [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError) if some parameter value is invalid

#### delete\_repo

[](#huggingface_hub.HfApi.delete_repo)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1356)

( repo\_id: str = Nonetoken: typing.Optional\[str\] = Noneorganization: typing.Optional\[str\] = Nonerepo\_type: typing.Optional\[str\] = Nonename: str = None )

Parameters

*   [](#huggingface_hub.HfApi.delete_repo.repo_id)**repo\_id** (`str`) — A namespace (user or an organization) and a repo name separated by a `/`.
    
    Version added: 0.5
    
*   [](#huggingface_hub.HfApi.delete_repo.token)**token** (`str`, _optional_) — An authentication token \[1\]\_.
*   [](#huggingface_hub.HfApi.delete_repo.repo_type)**repo\_type** (`str`, _optional_) — Set to `"dataset"` or `"space"` if uploading to a dataset or space, `None` or `"model"` if uploading to a model.

Delete a repo from the HuggingFace Hub. CAUTION: this is irreversible.

References:

*   \[1\] [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

#### get\_dataset\_tags

[](#huggingface_hub.HfApi.get_dataset_tags)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L673)

( )

Gets all valid dataset tags as a nested namespace object.

#### get\_full\_repo\_name

[](#huggingface_hub.HfApi.get_full_repo_name)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1793)

( model\_id: strorganization: typing.Optional\[str\] = Nonetoken: typing.Optional\[str\] = None ) → `str`

Parameters

*   [](#huggingface_hub.HfApi.get_full_repo_name.model_id)**model\_id** (`str`) — The name of the model.
*   [](#huggingface_hub.HfApi.get_full_repo_name.organization)**organization** (`str`, _optional_) — If passed, the repository name will be in the organization namespace instead of the user namespace.
*   [](#huggingface_hub.HfApi.get_full_repo_name.token)**token** (`str`, _optional_) — The Hugging Face authentication token

Returns

`str`

The repository name in the user’s namespace ({username}/{model\_id}) if no organization is passed, and under the organization namespace ({organization}/{model\_id}) otherwise.

Returns the repository name for a given model ID and optional organization.

#### get\_model\_tags

[](#huggingface_hub.HfApi.get_model_tags)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L665)

( )

Gets all valid model tags as a nested namespace object

#### list\_datasets

[](#huggingface_hub.HfApi.list_datasets)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L891)

( filter: typing.Union\[huggingface\_hub.utils.endpoint\_helpers.DatasetFilter, str, typing.Iterable\[str\], NoneType\] = Noneauthor: typing.Optional\[str\] = Nonesearch: typing.Optional\[str\] = Nonesort: typing.Union\[typing.Literal\['lastModified'\], str, NoneType\] = Nonedirection: typing.Optional\[typing.Literal\[-1\]\] = Nonelimit: typing.Optional\[int\] = NonecardData: typing.Optional\[bool\] = Nonefull: typing.Optional\[bool\] = Noneuse\_auth\_token: typing.Optional\[str\] = None )

Parameters

*   [](#huggingface_hub.HfApi.list_datasets.filter)**filter** ([DatasetFilter](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.DatasetFilter) or `str` or `Iterable`, _optional_) — A string or [DatasetFilter](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.DatasetFilter) which can be used to identify datasets on the hub.
*   [](#huggingface_hub.HfApi.list_datasets.author)**author** (`str`, _optional_) — A string which identify the author of the returned models
*   [](#huggingface_hub.HfApi.list_datasets.search)**search** (`str`, _optional_) — A string that will be contained in the returned models.
*   [](#huggingface_hub.HfApi.list_datasets.sort)**sort** (`Literal["lastModified"]` or `str`, _optional_) — The key with which to sort the resulting datasets. Possible values are the properties of the `DatasetInfo` class.
*   [](#huggingface_hub.HfApi.list_datasets.direction)**direction** (`Literal[-1]` or `int`, _optional_) — Direction in which to sort. The value `-1` sorts by descending order while all other values sort by ascending order.
*   [](#huggingface_hub.HfApi.list_datasets.limit)**limit** (`int`, _optional_) — The limit on the number of datasets fetched. Leaving this option to `None` fetches all datasets.
*   [](#huggingface_hub.HfApi.list_datasets.cardData)**cardData** (`bool`, _optional_) — Whether to grab the metadata for the dataset as well. Can contain useful information such as the PapersWithCode ID.
*   [](#huggingface_hub.HfApi.list_datasets.full)**full** (`bool`, _optional_) — Whether to fetch all dataset data, including the `lastModified` and the `cardData`.
*   [](#huggingface_hub.HfApi.list_datasets.use_auth_token)**use\_auth\_token** (`bool` or `str`, _optional_) — Whether to use the `auth_token` provided from the `huggingface_hub` cli. If not logged in, a valid `auth_token` can be passed in as a string.

Get the public list of all the datasets on huggingface.co

Example usage with the `filter` argument:

Copied

\>>> from huggingface\_hub import HfApi

\>>> api = HfApi()

\>>> \# List all datasets
\>>> api.list\_datasets()

\>>> \# Get all valid search arguments
\>>> args = DatasetSearchArguments()

\>>> \# List only the text classification datasets
\>>> api.list\_datasets(filter\="task\_categories:text-classification")
\>>> \# Using the \`DatasetFilter\`
\>>> filt = DatasetFilter(task\_categories="text-classification")
\>>> \# With \`DatasetSearchArguments\`
\>>> filt = DatasetFilter(task=args.task\_categories.text\_classification)
\>>> api.list\_models(filter\=filt)

\>>> \# List only the datasets in russian for language modeling
\>>> api.list\_datasets(
...     filter\=("languages:ru", "task\_ids:language-modeling")
... )
\>>> \# Using the \`DatasetFilter\`
\>>> filt = DatasetFilter(languages="ru", task\_ids="language-modeling")
\>>> \# With \`DatasetSearchArguments\`
\>>> filt = DatasetFilter(
...     languages=args.languages.ru,
...     task\_ids=args.task\_ids.language\_modeling,
... )
\>>> api.list\_datasets(filter\=filt)

Example usage with the `search` argument:

Copied

\>>> from huggingface\_hub import HfApi

\>>> api = HfApi()

\>>> \# List all datasets with "text" in their name
\>>> api.list\_datasets(search="text")

\>>> \# List all datasets with "text" in their name made by google
\>>> api.list\_datasets(search="text", author="google")

#### list\_metrics

[](#huggingface_hub.HfApi.list_metrics)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1057)

( ) → `List[MetricInfo]`

Returns

`List[MetricInfo]`

a list of `MetricInfo` objects which.

Get the public list of all the metrics on huggingface.co

#### list\_models

[](#huggingface_hub.HfApi.list_models)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L683)

( filter: typing.Union\[huggingface\_hub.utils.endpoint\_helpers.ModelFilter, str, typing.Iterable\[str\], NoneType\] = Noneauthor: typing.Optional\[str\] = Nonesearch: typing.Optional\[str\] = Noneemissions\_thresholds: typing.Union\[typing.Tuple\[float, float\], NoneType\] = Nonesort: typing.Union\[typing.Literal\['lastModified'\], str, NoneType\] = Nonedirection: typing.Optional\[typing.Literal\[-1\]\] = Nonelimit: typing.Optional\[int\] = Nonefull: typing.Optional\[bool\] = NonecardData: typing.Optional\[bool\] = Nonefetch\_config: typing.Optional\[bool\] = Noneuse\_auth\_token: typing.Union\[bool, str, NoneType\] = None )

Expand 11 parameters

Parameters

*   [](#huggingface_hub.HfApi.list_models.filter)**filter** ([ModelFilter](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.ModelFilter) or `str` or `Iterable`, _optional_) — A string or [ModelFilter](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.ModelFilter) which can be used to identify models on the Hub.
*   [](#huggingface_hub.HfApi.list_models.author)**author** (`str`, _optional_) — A string which identify the author (user or organization) of the returned models
*   [](#huggingface_hub.HfApi.list_models.search)**search** (`str`, _optional_) — A string that will be contained in the returned models Example usage:
*   [](#huggingface_hub.HfApi.list_models.emissions_thresholds)**emissions\_thresholds** (`Tuple`, _optional_) — A tuple of two ints or floats representing a minimum and maximum carbon footprint to filter the resulting models with in grams.
*   [](#huggingface_hub.HfApi.list_models.sort)**sort** (`Literal["lastModified"]` or `str`, _optional_) — The key with which to sort the resulting models. Possible values are the properties of the `ModelInfo` class.
*   [](#huggingface_hub.HfApi.list_models.direction)**direction** (`Literal[-1]` or `int`, _optional_) — Direction in which to sort. The value `-1` sorts by descending order while all other values sort by ascending order.
*   [](#huggingface_hub.HfApi.list_models.limit)**limit** (`int`, _optional_) — The limit on the number of models fetched. Leaving this option to `None` fetches all models.
*   [](#huggingface_hub.HfApi.list_models.full)**full** (`bool`, _optional_) — Whether to fetch all model data, including the `lastModified`, the `sha`, the files and the `tags`. This is set to `True` by default when using a filter.
*   [](#huggingface_hub.HfApi.list_models.cardData)**cardData** (`bool`, _optional_) — Whether to grab the metadata for the model as well. Can contain useful information such as carbon emissions, metrics, and datasets trained on.
*   [](#huggingface_hub.HfApi.list_models.fetch_config)**fetch\_config** (`bool`, _optional_) — Whether to fetch the model configs as well. This is not included in `full` due to its size.
*   [](#huggingface_hub.HfApi.list_models.use_auth_token)**use\_auth\_token** (`bool` or `str`, _optional_) — Whether to use the `auth_token` provided from the `huggingface_hub` cli. If not logged in, a valid `auth_token` can be passed in as a string.

Get the public list of all the models on huggingface.co

Example usage with the `filter` argument:

Copied

\>>> from huggingface\_hub import HfApi

\>>> api = HfApi()

\>>> \# List all models
\>>> api.list\_models()

\>>> \# Get all valid search arguments
\>>> args = ModelSearchArguments()

\>>> \# List only the text classification models
\>>> api.list\_models(filter\="text-classification")
\>>> \# Using the \`ModelFilter\`
\>>> filt = ModelFilter(task="text-classification")
\>>> \# With \`ModelSearchArguments\`
\>>> filt = ModelFilter(task=args.pipeline\_tags.TextClassification)
\>>> api.list\_models(filter\=filt)

\>>> \# Using \`ModelFilter\` and \`ModelSearchArguments\` to find text classification in both PyTorch and TensorFlow
\>>> filt = ModelFilter(
...     task=args.pipeline\_tags.TextClassification,
...     library=\[args.library.PyTorch, args.library.TensorFlow\],
... )
\>>> api.list\_models(filter\=filt)

\>>> \# List only models from the AllenNLP library
\>>> api.list\_models(filter\="allennlp")
\>>> \# Using \`ModelFilter\` and \`ModelSearchArguments\`
\>>> filt = ModelFilter(library=args.library.allennlp)

Example usage with the `search` argument:

Copied

\>>> from huggingface\_hub import HfApi

\>>> api = HfApi()

\>>> \# List all models with "bert" in their name
\>>> api.list\_models(search="bert")

\>>> \# List all models with "bert" in their name made by google
\>>> api.list\_models(search="bert", author="google")

#### list\_repo\_files

[](#huggingface_hub.HfApi.list_repo_files)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1125)

( repo\_id: strrevision: typing.Optional\[str\] = Nonerepo\_type: typing.Optional\[str\] = Nonetoken: typing.Optional\[str\] = Nonetimeout: typing.Optional\[float\] = None ) → `List[str]`

Parameters

*   [](#huggingface_hub.HfApi.list_repo_files.repo_id)**repo\_id** (`str`) — A namespace (user or an organization) and a repo name separated by a `/`.
*   [](#huggingface_hub.HfApi.list_repo_files.revision)**revision** (`str`, _optional_) — The revision of the model repository from which to get the information.
*   [](#huggingface_hub.HfApi.list_repo_files.repo_type)**repo\_type** (`str`, _optional_) — Set to `"dataset"` or `"space"` if uploading to a dataset or space, `None` or `"model"` if uploading to a model. Default is `None`.
*   [](#huggingface_hub.HfApi.list_repo_files.token)**token** (`str`, _optional_) — An authentication token \[1\]\_.
*   [](#huggingface_hub.HfApi.list_repo_files.timeout)**timeout** (`float`, _optional_) — Whether to set a timeout for the request to the Hub.

Returns

`List[str]`

the list of files in a given repository.

Get the list of files in a given repo.

References:

*   \[1\] [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

#### login

[](#huggingface_hub.HfApi.login)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L478)

( username: strpassword: str ) → `str`

Parameters

*   [](#huggingface_hub.HfApi.login.username)**username** (`str`) — The username of the account with which to login.
*   [](#huggingface_hub.HfApi.login.password)**password** (`str`) — The password of the account with which to login.

Returns

`str`

token if credentials are valid

Call HF API to sign in a user and get a token if credentials are valid.

Warning: Deprecated, will be removed in v0.7. Please use [HfApi.set\_access\_token()](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.HfApi.set_access_token) instead.

Raises the following errors:

*   [`HTTPError`](https://2.python-requests.org/en/master/api/#requests.HTTPError) if credentials are invalid

#### logout

[](#huggingface_hub.HfApi.logout)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L610)

( token: typing.Optional\[str\] = None )

Parameters

*   [](#huggingface_hub.HfApi.logout.token)**token** (`str`, _optional_) — Hugging Face token. Will default to the locally saved token if not provided.

Call HF API to log out.

Warning: Deprecated, will be removed in v0.7. Please use [HfApi.unset\_access\_token()](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.HfApi.unset_access_token) instead.

#### model\_info

[](#huggingface_hub.HfApi.model_info)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1071)

( repo\_id: strrevision: typing.Optional\[str\] = Nonetoken: typing.Optional\[str\] = Nonetimeout: typing.Optional\[float\] = NonesecurityStatus: typing.Optional\[bool\] = None ) → `ModelInfo`

Parameters

*   [](#huggingface_hub.HfApi.model_info.repo_id)**repo\_id** (`str`) — A namespace (user or an organization) and a repo name separated by a `/`.
*   [](#huggingface_hub.HfApi.model_info.revision)**revision** (`str`, _optional_) — The revision of the model repository from which to get the information.
*   [](#huggingface_hub.HfApi.model_info.token)**token** (`str`, _optional_) — An authentication token \[1\]\_.
*   [](#huggingface_hub.HfApi.model_info.timeout)**timeout** (`float`, _optional_) — Whether to set a timeout for the request to the Hub.
*   [](#huggingface_hub.HfApi.model_info.securityStatus)**securityStatus** (`bool`, _optional_) — Whether to retrieve the security status from the model repository as well.

Returns

`ModelInfo`

The model repository information.

Get info on one specific model on huggingface.co

Model can be private if you pass an acceptable token or are logged in.

References:

*   \[1\] [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

#### move\_repo

[](#huggingface_hub.HfApi.move_repo)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1521)

( from\_id: strto\_id: strrepo\_type: typing.Optional\[str\] = Nonetoken: typing.Optional\[str\] = None )

Parameters

*   [](#huggingface_hub.HfApi.move_repo.from_id)**from\_id** (`str`) — A namespace (user or an organization) and a repo name separated by a `/`. Original repository identifier.
*   [](#huggingface_hub.HfApi.move_repo.to_id)**to\_id** (`str`) — A namespace (user or an organization) and a repo name separated by a `/`. Final repository identifier.
*   [](#huggingface_hub.HfApi.move_repo.repo_type)**repo\_type** (`str`, _optional_) — Set to `"dataset"` or `"space"` if uploading to a dataset or space, `None` or `"model"` if uploading to a model. Default is `None`.
*   [](#huggingface_hub.HfApi.move_repo.token)**token** (`str`, _optional_) — An authentication token \[1\]\_.

Moving a repository from namespace1/repo\_name1 to namespace2/repo\_name2

Note there are certain limitations. For more information about moving repositories, please see [https://hf.co/docs/hub/main#how-can-i-rename-or-transfer-a-repo](https://hf.co/docs/hub/main#how-can-i-rename-or-transfer-a-repo).

References:

*   \[1\] [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

#### set\_access\_token

[](#huggingface_hub.HfApi.set_access_token)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L646)

( access\_token: str )

Parameters

*   [](#huggingface_hub.HfApi.set_access_token.access_token)**access\_token** (`str`) — The access token to save.

Saves the passed access token so git can correctly authenticate the user.

#### unset\_access\_token

[](#huggingface_hub.HfApi.unset_access_token)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L658)

( )

Resets the user’s access token.

#### update\_repo\_visibility

[](#huggingface_hub.HfApi.update_repo_visibility)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1451)

( repo\_id: str = Noneprivate: bool = Falsetoken: typing.Optional\[str\] = Noneorganization: typing.Optional\[str\] = Nonerepo\_type: typing.Optional\[str\] = Nonename: str = None )

Parameters

*   [](#huggingface_hub.HfApi.update_repo_visibility.repo_id)**repo\_id** (`str`, _optional_) — A namespace (user or an organization) and a repo name separated by a `/`.
    
    Version added: 0.5
    
*   [](#huggingface_hub.HfApi.update_repo_visibility.private)**private** (`bool`, _optional_, defaults to `False`) — Whether the model repo should be private.
*   [](#huggingface_hub.HfApi.update_repo_visibility.token)**token** (`str`, _optional_) — An authentication token \[1\]\_.
*   [](#huggingface_hub.HfApi.update_repo_visibility.repo_type)**repo\_type** (`str`, _optional_) — Set to `"dataset"` or `"space"` if uploading to a dataset or space, `None` or `"model"` if uploading to a model. Default is `None`.

Update the visibility setting of a repository.

References:

*   \[1\] [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

#### upload\_file

[](#huggingface_hub.HfApi.upload_file)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1590)

( path\_or\_fileobj: typing.Union\[str, bytes, typing.IO\]path\_in\_repo: strrepo\_id: strtoken: typing.Optional\[str\] = Nonerepo\_type: typing.Optional\[str\] = Nonerevision: typing.Optional\[str\] = Noneidentical\_ok: bool = True ) → `str`

Parameters

*   [](#huggingface_hub.HfApi.upload_file.path_or_fileobj)**path\_or\_fileobj** (`str`, `bytes`, or `IO`) — Path to a file on the local machine or binary data stream / fileobj / buffer.
*   [](#huggingface_hub.HfApi.upload_file.path_in_repo)**path\_in\_repo** (`str`) — Relative filepath in the repo, for example: `"checkpoints/1fec34a/weights.bin"`
*   [](#huggingface_hub.HfApi.upload_file.repo_id)**repo\_id** (`str`) — The repository to which the file will be uploaded, for example: `"username/custom_transformers"`
*   [](#huggingface_hub.HfApi.upload_file.token)**token** (`str`, _optional_) — Authentication token, obtained with `HfApi.login` method. Will default to the stored token.
*   [](#huggingface_hub.HfApi.upload_file.repo_type)**repo\_type** (`str`, _optional_) — Set to `"dataset"` or `"space"` if uploading to a dataset or space, `None` or `"model"` if uploading to a model. Default is `None`.
*   [](#huggingface_hub.HfApi.upload_file.revision)**revision** (`str`, _optional_) — The git revision to commit from. Defaults to the head of the `"main"` branch.
*   [](#huggingface_hub.HfApi.upload_file.identical_ok)**identical\_ok** (`bool`, _optional_, defaults to `True`) — When set to false, will raise an [HTTPError](https://2.python-requests.org/en/master/api/#requests.HTTPError) when the file you’re trying to upload already exists on the hub and its content did not change.

Returns

`str`

The URL to visualize the uploaded file on the hub

Upload a local file (up to 5GB) to the given repo. The upload is done through a HTTP post request, and doesn’t require git or git-lfs to be installed.

Raises the following errors:

*   [`HTTPError`](https://2.python-requests.org/en/master/api/#requests.HTTPError) if the HuggingFace API returned an error
*   [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError) if some parameter value is invalid

Example usage:

Copied

\>>> with open("./local/filepath", "rb") as fobj:
...     upload\_file(
...         path\_or\_fileobj=fileobj,
...         path\_in\_repo="remote/file/path.h5",
...         repo\_id="username/my-dataset",
...         repo\_type="datasets",
...         token="my\_token",
...     )
"https://huggingface.co/datasets/username/my-dataset/blob/main/remote/file/path.h5"

\>>> upload\_file(
...     path\_or\_fileobj=".\\\\local\\\\file\\\\path",
...     path\_in\_repo="remote/file/path.h5",
...     repo\_id="username/my-model",
...     token="my\_token",
... )
"https://huggingface.co/username/my-model/blob/main/remote/file/path.h5"

#### whoami

[](#huggingface_hub.HfApi.whoami)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L520)

( token: typing.Optional\[str\] = None )

Parameters

*   [](#huggingface_hub.HfApi.whoami.token)**token** (`str`, _optional_) — Hugging Face token. Will default to the locally saved token if not provided.

Call HF API to know “whoami”.

[](#huggingface_hub.HfFolder)Hugging Face local storage
-------------------------------------------------------

`huggingface_hub` stores the authentication information locally so that it may be re-used in subsequent methods.

It does this using the [HfFolder](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.HfFolder) utility, which saves data at the root of the user.

### class huggingface\_hub.HfFolder

[](#huggingface_hub.HfFolder)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1829)

( )

#### delete\_token

[](#huggingface_hub.HfFolder.delete_token)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1860)

( )

Deletes the token from storage. Does not fail if token does not exist.

#### get\_token

[](#huggingface_hub.HfFolder.get_token)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1845)

( ) → `str` or `None`

Returns

`str` or `None`

The token, `None` if it doesn’t exist.

Retrieves the token

#### save\_token

[](#huggingface_hub.HfFolder.save_token)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/hf_api.py#L1832)

( token )

Parameters

*   [](#huggingface_hub.HfFolder.save_token.token)**token** (`str`) — The token to save to the [HfFolder](/docs/huggingface_hub/v0.5.1/en/package_reference/hf_api#huggingface_hub.HfFolder)

Save token, creating folder as needed.

[](#huggingface_hub.DatasetFilter)Filtering helpers
---------------------------------------------------

Some helpers to filter repositories on the Hub are available in the `huggingface_hub` package.

### class huggingface\_hub.DatasetFilter

[](#huggingface_hub.DatasetFilter)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/utils/endpoint_helpers.py#L67)

( author: str = Nonebenchmark: typing.Union\[str, typing.List\[str\]\] = Nonedataset\_name: str = Nonelanguage\_creators: typing.Union\[str, typing.List\[str\]\] = Nonelanguages: typing.Union\[str, typing.List\[str\]\] = Nonemultilinguality: typing.Union\[str, typing.List\[str\]\] = Nonesize\_categories: typing.Union\[str, typing.List\[str\]\] = Nonetask\_categories: typing.Union\[str, typing.List\[str\]\] = Nonetask\_ids: typing.Union\[str, typing.List\[str\]\] = None )

Expand 9 parameters

Parameters

*   [](#huggingface_hub.DatasetFilter.author)**author** (`str`, _optional_) — A string or list of strings that can be used to identify datasets on the Hub by the original uploader (author or organization), such as `facebook` or `huggingface`.
*   [](#huggingface_hub.DatasetFilter.benchmark)**benchmark** (`str` or `List`, _optional_) — A string or list of strings that can be used to identify datasets on the Hub by their official benchmark.
*   [](#huggingface_hub.DatasetFilter.dataset_name)**dataset\_name** (`str`, _optional_) — A string or list of strings that can be used to identify datasets on the Hub by its name, such as `SQAC` or `wikineural`
*   [](#huggingface_hub.DatasetFilter.language_creators)**language\_creators** (`str` or `List`, _optional_) — A string or list of strings that can be used to identify datasets on the Hub with how the data was curated, such as `crowdsourced` or `machine_generated`.
*   [](#huggingface_hub.DatasetFilter.languages)**languages** (`str` or `List`, _optional_) — A string or list of strings representing a two-character language to filter datasets by on the Hub.
*   [](#huggingface_hub.DatasetFilter.multilinguality)**multilinguality** (`str` or `List`, _optional_) — A string or list of strings representing a filter for datasets that contain multiple languages.
*   [](#huggingface_hub.DatasetFilter.size_categories)**size\_categories** (`str` or `List`, _optional_) — A string or list of strings that can be used to identify datasets on the Hub by the size of the dataset such as `100K<n<1M` or `1M<n<10M`.
*   [](#huggingface_hub.DatasetFilter.task_categories)**task\_categories** (`str` or `List`, _optional_) — A string or list of strings that can be used to identify datasets on the Hub by the designed task, such as `audio_classification` or `named_entity_recognition`.
*   [](#huggingface_hub.DatasetFilter.task_ids)**task\_ids** (`str` or `List`, _optional_) — A string or list of strings that can be used to identify datasets on the Hub by the specific task such as `speech_emotion_recognition` or `paraphrase`.

A class that converts human-readable dataset search parameters into ones compatible with the REST API. For all parameters capitalization does not matter.

Examples:

Copied

\>>> from huggingface\_hub import DatasetFilter

\>>> \# Using author
\>>> new\_filter = DatasetFilter(author="facebook")

\>>> \# Using benchmark
\>>> new\_filter = DatasetFilter(benchmark="raft")

\>>> \# Using dataset\_name
\>>> new\_filter = DatasetFilter(dataset\_name="wikineural")

\>>> \# Using language\_creator
\>>> new\_filter = DatasetFilter(language\_creator="crowdsourced")

\>>> \# Using language
\>>> new\_filter = DatasetFilter(language="en")

\>>> \# Using multilinguality
\>>> new\_filter = DatasetFilter(multilinguality="yes")

\>>> \# Using size\_categories
\>>> new\_filter = DatasetFilter(size\_categories="100K<n<1M")

\>>> \# Using task\_categories
\>>> new\_filter = DatasetFilter(task\_categories="audio\_classification")

\>>> \# Using task\_ids
\>>> new\_filter = DatasetFilter(task\_ids="paraphrase")

### class huggingface\_hub.ModelFilter

[](#huggingface_hub.ModelFilter)[< source \>](https://github.com/huggingface/huggingface_hub/blob/v0.5.1/src/huggingface_hub/utils/endpoint_helpers.py#L153)

( author: str = Nonelibrary: typing.Union\[str, typing.List\[str\]\] = Nonelanguage: typing.Union\[str, typing.List\[str\]\] = Nonemodel\_name: str = Nonetask: typing.Union\[str, typing.List\[str\]\] = Nonetrained\_dataset: typing.Union\[str, typing.List\[str\]\] = Nonetags: typing.Union\[str, typing.List\[str\]\] = None )

Parameters

*   [](#huggingface_hub.ModelFilter.author)**author** (`str`, _optional_) — A string that can be used to identify models on the Hub by the original uploader (author or organization), such as `facebook` or `huggingface`.
*   [](#huggingface_hub.ModelFilter.library)**library** (`str` or `List`, _optional_) — A string or list of strings of foundational libraries models were originally trained from, such as pytorch, tensorflow, or allennlp.
*   [](#huggingface_hub.ModelFilter.language)**language** (`str` or `List`, _optional_) — A string or list of strings of languages, both by name and country code, such as “en” or “English”
*   [](#huggingface_hub.ModelFilter.model_name)**model\_name** (`str`, _optional_) — A string that contain complete or partial names for models on the Hub, such as “bert” or “bert-base-cased”
*   [](#huggingface_hub.ModelFilter.task)**task** (`str` or `List`, _optional_) — A string or list of strings of tasks models were designed for, such as: “fill-mask” or “automatic-speech-recognition”
*   [](#huggingface_hub.ModelFilter.tags)**tags** (`str` or `List`, _optional_) — A string tag or a list of tags to filter models on the Hub by, such as `text-generation` or `spacy`.
*   [](#huggingface_hub.ModelFilter.trained_dataset)**trained\_dataset** (`str` or `List`, _optional_) — A string tag or a list of string tags of the trained dataset for a model on the Hub.

A class that converts human-readable model search parameters into ones compatible with the REST API. For all parameters capitalization does not matter.

Copied

\>>> from huggingface\_hub import ModelFilter

\>>> \# For the author\_or\_organization
\>>> new\_filter = ModelFilter(author\_or\_organization="facebook")

\>>> \# For the library
\>>> new\_filter = ModelFilter(library="pytorch")

\>>> \# For the language
\>>> new\_filter = ModelFilter(language="french")

\>>> \# For the model\_name
\>>> new\_filter = ModelFilter(model\_name="bert")

\>>> \# For the task
\>>> new\_filter = ModelFilter(task="text-classification")

\>>> \# Retrieving tags using the \`HfApi.get\_model\_tags\` method
\>>> from huggingface\_hub import HfApi

\>>> api = HfApi()
\# To list model tags

\>>> api.get\_model\_tags()
\# To list dataset tags

\>>> api.get\_dataset\_tags()
\>>> new\_filter = ModelFilter(tags="benchmark:raft")

\>>> \# Related to the dataset
\>>> new\_filter = ModelFilter(trained\_dataset="common\_voice")

[←Managing local and online repositories](/docs/huggingface_hub/v0.5.1/en/package_reference/repository) [Downloading files→](/docs/huggingface_hub/v0.5.1/en/package_reference/file_download)