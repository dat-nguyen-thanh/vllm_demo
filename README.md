# vllm_demo
Step 0: Prepare a dataset file (e.g `output_file.txt`), each line in the file is a single prompt

Step 1: Run `python launch_vllm --port XXXX --model facebook/opt-125M`. NOTE: By default, vLLM will load OPT-125M, please refer to their docs to find supported models

Step 2: Run `python benchmark_throughput.py --backend vLLM --results_filename #FILE_NAME_TO_SAVE_LOG_RESULTS --port #### --prompts_filename #LOCATION_TO_PROMPT_FILE --fixed_max_tokens #_MAX_TOKENS`. NOTE: By default, it will send burst requests to API server. If you wish to send requests over a period of time, add `--distribution poisson --qps #N` where `--distribution` is the distribution of requests sent over time and `--qps` is number of requests per seconds you wish to send. 

Step 3: The result would look something like `backend vLLM dur_s 1155.58 tokens_per_s 427.45 qps 0.36 successful_responses 420 prompt_token_count 138112 response_token_count 355840, median_token_latency=0.3383212293653438, median_e2e_latency=519.6614083051682`
`dur_s` is the total time to process all requests
`token_per_s` is the throughput of model
`qps` is the number of request model handled by second
`successful_respones` is the number of requests successfully processed
`prompt_token_count` is the total # of token counts (prompt)
`response_token_count` is the total # of token counts (response)
`median_e2e_latency` is the median latency for a request to get processed 