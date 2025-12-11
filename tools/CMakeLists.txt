# dependencies

find_package(Threads REQUIRED)

# third-party

# ...

# flags

llama_add_compile_flags()

# tools

# Helper macro to conditionally add tool subdirectories
macro(add_tool_subdirectory subdir)
    if(NOT LLAMA_TOOLS_BUILD_LIST OR "${subdir}" IN_LIST LLAMA_TOOLS_BUILD_LIST)
        add_subdirectory(${subdir})
    endif()
endmacro()

if (EMSCRIPTEN)
else()
    add_tool_subdirectory(batched-bench)
    add_tool_subdirectory(gguf-split)
    add_tool_subdirectory(imatrix)
    add_tool_subdirectory(llama-bench)
    add_tool_subdirectory(main)
    add_tool_subdirectory(perplexity)
    add_tool_subdirectory(quantize)
    if (LLAMA_BUILD_SERVER)
        add_tool_subdirectory(server)
    endif()
    add_tool_subdirectory(run)
    add_tool_subdirectory(tokenize)
    add_tool_subdirectory(tts)
    add_tool_subdirectory(mtmd)
    if (GGML_RPC)
        add_tool_subdirectory(rpc)
    endif()
    if (NOT GGML_BACKEND_DL)
        # these examples use the backends directly and cannot be built with dynamic loading
        add_tool_subdirectory(cvector-generator)
        add_tool_subdirectory(export-lora)
    endif()
endif()
