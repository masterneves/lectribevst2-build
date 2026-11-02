cmake_minimum_required(VERSION 3.22)

project(electribevst2 VERSION 0.0.1)

# Adiciona a pasta do JUCE descarregada pelo GitHub Actions
add_subdirectory(JUCE)

# Configura o plugin apenas para o formato VST3
juce_add_plugin(electribevst2
    COMPANY_NAME "Masterneves"
    PLUGIN_NAME "electribevst2"
    FORMATS VST3
    PRODUCT_NAME "electribevst2"
    NEEDS_MIDI_INPUT TRUE
    IS_SYNTH TRUE)

# Aponta diretamente para os ficheiros C++ na raiz do repositório
target_sources(electribevst2 PRIVATE
    PluginProcessor.cpp
    PluginProcessor.h
    PluginEditor.cpp
    PluginEditor.h
)

# Desativa explicitamente o VST2 para eliminar o erro C1189 de automação
target_compile_definitions(electribevst2 PRIVATE
    JUCE_WEB_BROWSER=0
    JUCE_USE_CURL=0
    JucePlugin_Build_VST2=0)

target_link_libraries(electribevst2 PRIVATE
    juce::juce_audio_utils
    juce::juce_recommended_config_flags
    juce::juce_recommended_warning_flags)
