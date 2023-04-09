if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    set (SSL_ROOT_PATH ${CMAKE_CURRENT_LIST_DIR}/no-asm)
else()
    set (SSL_ROOT_PATH ${CMAKE_CURRENT_LIST_DIR})
endif()

if (QT_VERSION LESS 6.5.0)
    set(ANDROID_EXTRA_LIBS
        ${SSL_ROOT_PATH}/ssl_1.1/${CMAKE_ANDROID_ARCH_ABI}/libcrypto_1_1.so
        ${SSL_ROOT_PATH}/ssl_1.1/${CMAKE_ANDROID_ARCH_ABI}/libssl_1_1.so
        CACHE INTERNAL "")
else()
    macro (add_target_openssl_libs _target)
        set_property(TARGET ${_target} APPEND PROPERTY QT_ANDROID_EXTRA_LIBS
            ${SSL_ROOT_PATH}/ssl_3/${CMAKE_ANDROID_ARCH_ABI}/libcrypto_3.so
            ${SSL_ROOT_PATH}/ssl_3/${CMAKE_ANDROID_ARCH_ABI}/libssl_3.so
        )
    endmacro()
endif()
