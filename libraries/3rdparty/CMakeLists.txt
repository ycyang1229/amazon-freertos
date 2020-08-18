# -------------------------------------------------------------------------------------------------
# 3rdparty libraries
# -------------------------------------------------------------------------------------------------
# http_parser - HTTP message parser
if(EXISTS "${AFR_3RDPARTY_DIR}/http_parser")
    afr_3rdparty_module(http_parser)
    target_sources(
        3rdparty::http_parser INTERFACE
        "${AFR_3RDPARTY_DIR}/http_parser/http_parser.h"
        "${AFR_3RDPARTY_DIR}/http_parser/http_parser.c"
    )
    target_include_directories(
        3rdparty::http_parser INTERFACE
        "${AFR_3RDPARTY_DIR}/http_parser"
    )
endif()

# jsmn - JSON parser
if(EXISTS "${AFR_3RDPARTY_DIR}/jsmn")
    afr_3rdparty_module(jsmn)
    target_sources(
        3rdparty::jsmn INTERFACE
        "${AFR_3RDPARTY_DIR}/jsmn/jsmn.h"
        "${AFR_3RDPARTY_DIR}/jsmn/jsmn.c"
    )
    target_include_directories(
        3rdparty::jsmn INTERFACE
        "${AFR_3RDPARTY_DIR}/jsmn"
    )
endif()

# lwip
if(EXISTS "${AFR_3RDPARTY_DIR}/lwip" AND NOT "${AFR_BOARD}" STREQUAL "pc.windows")
    add_library(
        afr_3rdparty_lwip STATIC EXCLUDE_FROM_ALL
    )
    target_sources(
        afr_3rdparty_lwip
        PRIVATE
            "${AFR_3RDPARTY_DIR}/lwip/src/api/api_lib.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/api/api_msg.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/api/err.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/api/netbuf.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/api/netdb.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/api/netifapi.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/api/sockets.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/api/tcpip.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/def.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/dns.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/inet_chksum.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/init.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/mem.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/memp.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/netif.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/raw.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/stats.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/sys.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/tcp.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/tcp_in.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/timeouts.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/udp.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/pbuf.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/tcp_out.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ip.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/acd.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/autoip.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/dhcp.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/icmp.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/igmp.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/ip4.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/ip4_addr.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/ip4_frag.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv4/etharp.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/dhcp6.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/ethip6.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/icmp6.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/inet6.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/ip6.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/ip6_addr.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/ip6_frag.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/mld6.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/core/ipv6/nd6.c"
            "${AFR_3RDPARTY_DIR}/lwip/src/netif/ethernet.c"
    )
    target_include_directories(
        afr_3rdparty_lwip
        PUBLIC
            "${AFR_3RDPARTY_DIR}/lwip/src/include"
    )
    target_link_libraries(
        afr_3rdparty_lwip
        PRIVATE
            AFR::kernel
            3rdparty::lwip_osal
    )
    add_library(3rdparty::lwip ALIAS afr_3rdparty_lwip)
endif()

# lwip implementation based on FreeRTOS
if(EXISTS "${AFR_3RDPARTY_DIR}/lwip_osal" AND NOT "${AFR_BOARD}" STREQUAL "pc.windows")
    add_library(
        afr_3rdparty_lwip_osal STATIC EXCLUDE_FROM_ALL
    )

    target_include_directories(
        afr_3rdparty_lwip_osal
        PUBLIC
            "${AFR_3RDPARTY_DIR}/lwip_osal/include"
    )

    target_sources(
        afr_3rdparty_lwip_osal
        PRIVATE
            "${AFR_3RDPARTY_DIR}/lwip_osal/include/lwipopts_freertos.h"
            "${AFR_3RDPARTY_DIR}/lwip_osal/include/arch/cc.h"
            "${AFR_3RDPARTY_DIR}/lwip_osal/include/arch/perf.h"
            "${AFR_3RDPARTY_DIR}/lwip_osal/include/arch/sys_arch.h"
            "${AFR_3RDPARTY_DIR}/lwip_osal/src/sys_arch.c"
    )
    target_link_libraries(
        afr_3rdparty_lwip_osal
        PRIVATE
            AFR::kernel
            3rdparty::lwip
    )
    add_library(3rdparty::lwip_osal ALIAS afr_3rdparty_lwip_osal)
endif()
# #YC_TBD, #mbedtls.
# mbedtls - TLS protocol implementation
if(EXISTS "${AFR_3RDPARTY_DIR}/mbedtls")
    afr_glob_src(mbedtls_library DIRECTORY "${AFR_3RDPARTY_DIR}/mbedtls/library" RECURSE)
    afr_glob_src(mbedtls_include DIRECTORY "${AFR_3RDPARTY_DIR}/mbedtls/include" RECURSE)

    # Build to static library to save some time.
    add_library(
        afr_3rdparty_mbedtls STATIC EXCLUDE_FROM_ALL
        ${mbedtls_library}
        ${mbedtls_include}
        "${AFR_3RDPARTY_DIR}/mbedtls_utils/mbedtls_utils.c"
        "${AFR_3RDPARTY_DIR}/mbedtls_utils/mbedtls_error.h"
        "${AFR_3RDPARTY_DIR}/mbedtls_utils/mbedtls_error.c"
        "${AFR_MODULES_ABSTRACTIONS_DIR}/pkcs11/mbedtls/threading_alt.h"
    )
    # The "${AFR_3RDPARTY_DIR}/pkcs11" directory must be included before
    # "${AFR_3RDPARTY_DIR}/mbedtls/include/mbedtls". This is because mbedtls/include
    # contains a pkcs11.h header file that will be used over the pkcs11.h file defined
    # in the pkcs11 directory. These pkcs11.h files are not interchangeable, the one in
    # the pkcs11 directory should be used. Ideally everywhere the mbed tls header files
    # are used, they would reference #include "mbedtls/xxx.h" to avoid a naming
    # conflict. Some vendor/external code does not do this and for that reason we need
    # to include the "${AFR_3RDPARTY_DIR}/mbedtls/include/mbedtls" directory
    target_include_directories(
        afr_3rdparty_mbedtls PUBLIC 
        "${AFR_3RDPARTY_DIR}/pkcs11"
    )
    target_include_directories(
        afr_3rdparty_mbedtls PUBLIC
        "${AFR_3RDPARTY_DIR}/mbedtls/include"
        "${AFR_MODULES_ABSTRACTIONS_DIR}/pkcs11/mbedtls"
        "${AFR_3RDPARTY_DIR}/mbedtls/include/mbedtls"
        "${AFR_3RDPARTY_DIR}/mbedtls_utils"
    )
    target_link_libraries(
        afr_3rdparty_mbedtls
        PRIVATE AFR::kernel
    )
    add_library(3rdparty::mbedtls ALIAS afr_3rdparty_mbedtls)
endif()

# pkcs11 standard header
if(EXISTS "${AFR_3RDPARTY_DIR}/pkcs11")
    add_library(afr_3rdparty_pkcs11 INTERFACE)
    target_sources(
        afr_3rdparty_pkcs11 INTERFACE
        "${AFR_3RDPARTY_DIR}/pkcs11/pkcs11.h"
        "${AFR_3RDPARTY_DIR}/pkcs11/pkcs11f.h"
        "${AFR_3RDPARTY_DIR}/pkcs11/pkcs11t.h"
    )
    target_include_directories(
        afr_3rdparty_pkcs11 INTERFACE
        "${AFR_3RDPARTY_DIR}/pkcs11"
    )
    add_library(3rdparty::pkcs11 ALIAS afr_3rdparty_pkcs11)
endif()

# tinycbor - CBOR implementation
if(EXISTS "${AFR_3RDPARTY_DIR}/tinycbor")
    set(tinycbor_src
        "${AFR_3RDPARTY_DIR}/tinycbor/src/cborpretty.c"
        "${AFR_3RDPARTY_DIR}/tinycbor/src/cborpretty_stdio.c"
        "${AFR_3RDPARTY_DIR}/tinycbor/src/cborencoder.c"
        "${AFR_3RDPARTY_DIR}/tinycbor/src/cborencoder_close_container_checked.c"
        "${AFR_3RDPARTY_DIR}/tinycbor/src/cborerrorstrings.c"
        "${AFR_3RDPARTY_DIR}/tinycbor/src/cborparser.c"
        "${AFR_3RDPARTY_DIR}/tinycbor/src/cborparser_dup_string.c"
    )
    add_library(
        afr_3rdparty_tinycbor STATIC EXCLUDE_FROM_ALL
        ${tinycbor_src}
    )
    target_sources(
        afr_3rdparty_tinycbor
        PRIVATE
            ${tinycbor_src}
    )
    target_include_directories(
        afr_3rdparty_tinycbor
        PUBLIC
            "${AFR_3RDPARTY_DIR}/tinycbor/src"
    )
    target_link_libraries(
        afr_3rdparty_tinycbor
        PRIVATE AFR::compiler::mcu_port
    )
    target_compile_options(
        afr_3rdparty_tinycbor
        PRIVATE
            $<$<C_COMPILER_ID:GNU>:-w>
    )
    add_library(3rdparty::tinycbor ALIAS afr_3rdparty_tinycbor)
endif()

# tracealyzer - Trace record library from FreeRTOS
if(EXISTS "${AFR_3RDPARTY_DIR}/tracealyzer_recorder")
    afr_3rdparty_module(tracealyzer_recorder)
    target_sources(
        3rdparty::tracealyzer_recorder INTERFACE
        "${AFR_3RDPARTY_DIR}/tracealyzer_recorder/trcKernelPort.c"
        "${AFR_3RDPARTY_DIR}/tracealyzer_recorder/trcSnapshotRecorder.c"
    )
    target_include_directories(
        3rdparty::tracealyzer_recorder INTERFACE
        "${AFR_3RDPARTY_DIR}/tracealyzer_recorder/Include"
    )

    # WinPcap - pcap port for windows
    afr_3rdparty_module(win_pcap)
    target_include_directories(3rdparty::win_pcap INTERFACE "${AFR_3RDPARTY_DIR}/win_pcap")
    if(MSVC)
        target_link_libraries(3rdparty::win_pcap INTERFACE "${AFR_3RDPARTY_DIR}/win_pcap/wpcap.lib")
    elseif(MINGW)
        target_link_libraries(3rdparty::win_pcap INTERFACE "${AFR_3RDPARTY_DIR}/win_pcap/libwpcap.a")
    endif()
endif()

# tinycrypt standard header
if(EXISTS "${AFR_3RDPARTY_DIR}/tinycrypt")
    afr_3rdparty_module(tinycrypt)
    afr_glob_src(tinycrypt_src_lib DIRECTORY "${AFR_3RDPARTY_DIR}/tinycrypt/lib" RECURSE)
    afr_glob_src(tinycrypt_src_asn1 DIRECTORY "${AFR_3RDPARTY_DIR}/tinycrypt/asn1" RECURSE)
    target_sources(
        3rdparty::tinycrypt INTERFACE
        ${tinycrypt_src_lib}
        ${tinycrypt_src_asn1}
    )
    target_include_directories(
        3rdparty::tinycrypt INTERFACE
        "${AFR_3RDPARTY_DIR}/tinycrypt/asn1"
        "${AFR_3RDPARTY_DIR}/tinycrypt/lib/include"
    )
endif()

# unity - test framework
if(EXISTS "${AFR_3RDPARTY_DIR}/unity")
    afr_3rdparty_module(unity)
    target_sources(
        3rdparty::unity INTERFACE
        "${AFR_3RDPARTY_DIR}/unity/src/unity.c"
        "${AFR_3RDPARTY_DIR}/unity/src/unity.h"
        "${AFR_3RDPARTY_DIR}/unity/src/unity_internals.h"
        "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture.c"
        "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture.h"
        "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture_internals.h"
        "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src/unity_fixture_malloc_overrides.h"
    )
    target_include_directories(
        3rdparty::unity INTERFACE
        "${AFR_3RDPARTY_DIR}/unity/src"
        "${AFR_3RDPARTY_DIR}/unity/extras/fixture/src"
    )
    target_compile_definitions(3rdparty::unity INTERFACE UNITY_INCLUDE_CONFIG_H)
endif()

# #YC_TBD, # #libwebsockets
if(EXISTS "${AFR_3RDPARTY_DIR}/libwebsockets")
    afr_glob_src(libwebsockets_library DIRECTORY "${AFR_3RDPARTY_DIR}/libwebsockets/lib" RECURSE)
    afr_glob_src(libwebsockets_include DIRECTORY "${AFR_3RDPARTY_DIR}/libwebsockets/include" RECURSE)

    # Build to static library to save some time.
    add_library(
        afr_3rdparty_libwebsockets STATIC EXCLUDE_FROM_ALL
        ${libwebsockets_library}
        ${libwebsockets_include}
    )

    target_include_directories(
        afr_3rdparty_libwebsockets PUBLIC
        "${AFR_3RDPARTY_DIR}/libwebsockets/include"
        "${AFR_3RDPARTY_DIR}/libwebsockets/include/libwebsockets"
    )
    target_link_libraries(
        afr_3rdparty_libwebsockets
        PRIVATE AFR::kernel
    )
    add_library(3rdparty::libwebsockets ALIAS afr_3rdparty_libwebsockets)
endif()

# #YC_TBD, # #amazon-kinesis-video-streams-pic, kvspicUtils, kvspicState
if(EXISTS "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic")
    # common
    afr_glob_src(kvspicCommon_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/common/include" RECURSE)
    #client
    afr_glob_src(kvspicClient_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/client/include" RECURSE)
    afr_glob_src(kvspicClient_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/client/src" RECURSE)
    #duration
    afr_glob_src(kvspicDuration_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/duration/src" RECURSE)
    #heap
    afr_glob_src(kvspicHeap_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/heap/include" RECURSE)
    afr_glob_src(kvspicHeap_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/heap/src" RECURSE)
    #mkvgen
    afr_glob_src(kvspicMkvgen_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/mkvgen/include" RECURSE)
    afr_glob_src(kvspicMkvgen_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/mkvgen/src" RECURSE)
    #state
    afr_glob_src(kvspicState_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/state/include" RECURSE)
    afr_glob_src(kvspicState_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/state/src" RECURSE)
    #trace
    afr_glob_src(kvspicTrace_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/trace/include" RECURSE)
    afr_glob_src(kvspicTrace_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/trace/src" RECURSE)
    #utils
    afr_glob_src(kvspicUtils_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/utils/include" RECURSE)
    afr_glob_src(kvspicUtils_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/utils/src" RECURSE)
    #view 
    afr_glob_src(kvspicView_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/view/include" RECURSE)
    afr_glob_src(kvspicView_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/view/src" RECURSE)
    
    # #amazon-kinesis-video-streams-pic, kvspicClient
    add_library(
        afr_3rdparty_kvspicClient STATIC EXCLUDE_FROM_ALL
        ${kvspicClient_library}
        ${kvspicClient_include}
    )
    # #YC_TBD, 
    target_include_directories(
        afr_3rdparty_kvspicClient PUBLIC
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/client/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/utils/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/mkvgen/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/view/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/heap/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/state/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/common/include"
    )

    target_link_libraries(
        afr_3rdparty_kvspicClient
        PRIVATE AFR::kernel
    )
    add_library(3rdparty::kvspicClient ALIAS afr_3rdparty_kvspicClient)

    # #amazon-kinesis-video-streams-pic, kvspicUtils
    add_library(
        afr_3rdparty_kvspicUtils STATIC EXCLUDE_FROM_ALL
        ${kvspicUtils_library}
        ${kvspicUtils_include}
    )
    # #YC_TBD, 
    target_include_directories(
        afr_3rdparty_kvspicUtils PUBLIC
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/common/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/utils/include"
    )

    target_link_libraries(
        afr_3rdparty_kvspicUtils
        PRIVATE AFR::kernel
    )
    add_library(3rdparty::kvspicUtils ALIAS afr_3rdparty_kvspicUtils)

    # #amazon-kinesis-video-streams-pic, kvspicState
    
    # Build to static library to save some time.
    add_library(
        afr_3rdparty_kvspicState STATIC EXCLUDE_FROM_ALL
        ${kvspicState_library}
        ${kvspicState_include}
    )
    # #YC_TBD, 
    target_include_directories(
        afr_3rdparty_kvspicState PUBLIC
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/common/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/state/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/mkvgen/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/utils/include"
    )

    target_link_libraries(
        afr_3rdparty_kvspicState
        PRIVATE AFR::kernel
    )
    add_library(3rdparty::kvspicState ALIAS afr_3rdparty_kvspicState)

endif()



# #YC_TBD, # #amazon-kinesis-video-streams-producer-c, kvsCommonLws
if(EXISTS "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-producer-c")
    # #amazon-kinesis-video-streams-producer-c, kvsCommonLws
    afr_glob_src(kvsCommon_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-producer-c/src/source/Common" RECURSE)
    afr_glob_src(kvsCommonLws_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-producer-c/src/source/Common/Lws" RECURSE)
    afr_glob_src(kvsCommonLws_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-producer-c/src/include" RECURSE)

    # Build to static library to save some time.
    add_library(
        afr_3rdparty_kvsCommonLws STATIC EXCLUDE_FROM_ALL
        ${kvsCommon_library}
        ${kvsCommonLws_library}
        ${kvsCommonLws_include}
    )

    target_compile_options(afr_3rdparty_kvsCommonLws PUBLIC -DKVS_USE_MBEDTLS -DKVS_BUILD_WITH_LWS)
    target_include_directories(
        afr_3rdparty_kvsCommonLws PUBLIC
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-producer-c/src/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-pic/src/client/include"## #YC_TBD, 
    )

    target_link_libraries(
        afr_3rdparty_kvsCommonLws
        PRIVATE AFR::kernel
                3rdparty::mbedtls
                3rdparty::libwebsockets
                3rdparty::kvspicUtils
    )

    add_library(3rdparty::kvsCommonLws ALIAS afr_3rdparty_kvsCommonLws)
endif()

# #YC_TBD, # #amazon-kinesis-video-streams-webrtc-sdk-c, kvsWebrtcClient, kvsWebrtcSignalingClient
if(EXISTS "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-webrtc-sdk-c")
    # #amazon-kinesis-video-streams-webrtc-sdk-c, kvsWebrtcSignalingClient
    afr_glob_src(kvsWebrtcSignalingClient_library DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-webrtc-sdk-c/src/source/Signaling" RECURSE)
    afr_glob_src(kvsWebrtcSignalingClient_include DIRECTORY "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-webrtc-sdk-c/src/include" RECURSE)

    # Build to static library to save some time.
    add_library(
        afr_3rdparty_kvsWebrtcSignalingClient STATIC EXCLUDE_FROM_ALL
        ${kvsWebrtcSignalingClient_library}
        ${kvsWebrtcSignalingClient_include}
    )

    target_include_directories(
        afr_3rdparty_kvsWebrtcSignalingClient PUBLIC
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-webrtc-sdk-c/src/include"
        "${AFR_3RDPARTY_DIR}/amazon-kinesis-video-streams-webrtc-sdk-c/src/source/Signaling"
    )

    target_link_libraries(
        afr_3rdparty_kvsWebrtcSignalingClient
        PRIVATE AFR::kernel
                3rdparty::mbedtls
                3rdparty::libwebsockets
                3rdparty::kvspicUtils
                3rdparty::kvspicState
                3rdparty::kvsCommonLws
    )

    add_library(3rdparty::kvsCommonLws ALIAS afr_3rdparty_kvsCommonLws)
endif()