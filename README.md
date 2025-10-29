# Specmatic MCP Auto Test

## MCP Inspector
```shell
npx @modelcontextprotocol/inspector
```
### Set up Instructions
1. Set Transport Type to `Streamable HTTP`
2. Set Base URL to `https://mcp.postman.com/minimal`
3. Set Bearer Token to `PMAK-68b82fe8750aba0001c4c047-db12bc86e442be312c20d3e176f33374f3`
4. Click on `Connect`
5. Click on `List Tools` to see the list of tools available
6. Select a tool and provide the required inputs to test the tool

## Test Postman's remote MCP Server
```shell
docker run -v "$(pwd)/build/reports/specmatic:/usr/src/app/build/reports/specmatic" \
-v "$(pwd)/postman_dict.json:/usr/src/app/dict.json" \
specmatic/specmatic mcp test \
--url https://mcp.postman.com/minimal \
--bearer-token PMAK-68b82fe8750aba0001c4c047-db12bc86e442be312c20d3e176f33374f3 \
--dictionary-file dict.json \
--skip-tools createCollectionResponse,createMock,createSpecFile,generateSpecFromCollection,getTaggedEntities,publishMock,getSpecCollections,getStatusOfAnAsyncApiTask,syncCollectionWithSpec,syncSpecWithCollection

./generate_specmatic_report.sh
```

## Test Postman's MCP Server - update mock tool
```shell
docker run -v "$(pwd)/build/reports/specmatic:/usr/src/app/build/reports/specmatic" \
-v "$(pwd)/postman_dict.json:/usr/src/app/dict.json" \
specmatic/specmatic mcp test \
--url https://mcp.postman.com/minimal \
--bearer-token PMAK-68b82fe8750aba0001c4c047-db12bc86e442be312c20d3e176f33374f3 \
--dictionary-file dict.json \
--filter-tools updateMock

./generate_specmatic_report.sh
```

## Test Postman's MCP Server - create workspace with resiliency testing
```shell
docker run -v "$(pwd)/build/reports/specmatic:/usr/src/app/build/reports/specmatic" \
-v "$(pwd)/postman_dict.json:/usr/src/app/dict.json" \
specmatic/specmatic mcp test \
--url https://mcp.postman.com/minimal \
--bearer-token PMAK-68b82fe8750aba0001c4c047-db12bc86e442be312c20d3e176f33374f3 \
--dictionary-file dict.json \
--filter-tools createWorkspace \
--enable-resiliency-tests

./generate_specmatic_report.sh
```

## HuggingFace MCP Server
```shell
docker run -v "$(pwd)/build/reports/specmatic:/usr/src/app/build/reports/specmatic" \
-v "$(pwd)/hugging_face_dict.json:/usr/src/app/dict.json" \
specmatic/specmatic mcp test \
--url https://huggingface.co/mcp \
--dictionary-file dict.json \
--bearer-token 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

./generate_specmatic_report.sh
```

## HuggingFace MCP Server - gr1_flux1_schnell_infer tool
```shell
docker run -v "$(pwd)/build/reports/specmatic:/usr/src/app/build/reports/specmatic" \
-v "$(pwd)/hugging_face_dict.json:/usr/src/app/dict.json" \
specmatic/specmatic mcp test \
--url https://huggingface.co/mcp \
--dictionary-file dict.json \
--bearer-token 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 \
--filter-tools gr1_flux1_schnell_infer \
--enable-resiliency-tests

./generate_specmatic_report.sh
```
