cmake_minimum_required(VERSION 3.22)

project(electribevst2 VERSION 0.0.1)

# Adiciona o framework JUCE que é descarregado automaticamente
add_subdirectory(JUCE)

juce_add_plugin(electribevst2
    COMPANY_NAME "Masterneves"
    PLUGIN_NAME "electribevst2"
    FORMATS VST3
    PRODUCT_NAME "electribevst2")

# Usa os ficheiros diretamente a partir da raiz do repositório
target_sources(electribevst2 PRIVATE
    PluginProcessor.cpp
    PluginProcessor.h
    PluginEditor.cpp
    PluginEditor.h
)

target_compile_definitions(electribevst2 PRIVATE
    JUCE_WEB_BROWSER=0
    JUCE_USE_CURL=0)

target_link_libraries(electribevst2 PRIVATE
    juce::juce_audio_utils
    juce::juce_recommended_config_flags
    juce::juce_recommended_warning_flags)
