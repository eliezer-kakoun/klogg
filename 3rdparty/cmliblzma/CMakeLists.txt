PROJECT(CMLIBLZMA C)

include(CheckCSourceCompiles)
include(CheckIncludeFile)
include(CheckSymbolExists)
include(CheckTypeSize)
include(TestBigEndian)

CHECK_INCLUDE_FILE(byteswap.h HAVE_BYTESWAP_H)
CHECK_INCLUDE_FILE(inttypes.h HAVE_INTTYPES_H)
CHECK_INCLUDE_FILE(limits.h HAVE_LIMITS_H)
CHECK_INCLUDE_FILE(memory.h HAVE_MEMORY_H)
CHECK_INCLUDE_FILE(strings.h HAVE_STRINGS_H)
CHECK_INCLUDE_FILE(string.h HAVE_STRING_H)
CHECK_INCLUDE_FILE(sys/sysctl.h HAVE_SYS_SYSCTL_H)

CHECK_INCLUDE_FILE(stdbool.h HAVE_STDBOOL_H)
if(NOT HAVE_STDBOOL_H)
  CHECK_TYPE_SIZE(_Bool _BOOL)
endif()

CHECK_C_SOURCE_COMPILES (
  "#include<byteswap.h>\nint main(void){bswap_16(0);return 0;}"
  HAVE_BSWAP_16)
CHECK_C_SOURCE_COMPILES (
  "#include<byteswap.h>\nint main(void){bswap_32(0);return 0;}"
  HAVE_BSWAP_32)
CHECK_C_SOURCE_COMPILES (
  "#include<byteswap.h>\nint main(void){bswap_64(0);return 0;}"
  HAVE_BSWAP_64)

TEST_BIG_ENDIAN(WORDS_BIGENDIAN)

set(HAVE_CHECK_CRC64 1)
set(HAVE_CHECK_SHA256 1)

set(HAVE_DECODER_ARM 1)
set(HAVE_DECODER_ARMTHUMB 1)
set(HAVE_DECODER_DELTA 1)
set(HAVE_DECODER_IA64 1)
set(HAVE_DECODER_LZMA1 1)
set(HAVE_DECODER_LZMA2 1)
set(HAVE_DECODER_POWERPC 1)
set(HAVE_DECODER_SPARC 1)
set(HAVE_DECODER_X86 1)

set(HAVE_ENCODER_ARM 1)
set(HAVE_ENCODER_ARMTHUMB 1)
set(HAVE_ENCODER_DELTA 1)
set(HAVE_ENCODER_IA64 1)
set(HAVE_ENCODER_LZMA1 1)
set(HAVE_ENCODER_LZMA2 1)
set(HAVE_ENCODER_POWERPC 1)
set(HAVE_ENCODER_SPARC 1)
set(HAVE_ENCODER_X86 1)

set(HAVE_MF_BT2 1)
set(HAVE_MF_BT3 1)
set(HAVE_MF_BT4 1)
set(HAVE_MF_HC3 1)
set(HAVE_MF_HC4 1)

CHECK_TYPE_SIZE(int16_t INT16_T)
CHECK_TYPE_SIZE(int32_t INT32_T)
CHECK_TYPE_SIZE(int64_t INT64_T)
CHECK_TYPE_SIZE(intmax_t INTMAX_T)
CHECK_TYPE_SIZE(uint8_t UINT8_T)
CHECK_TYPE_SIZE(uint16_t UINT16_T)
CHECK_TYPE_SIZE(uint32_t UINT32_T)
CHECK_TYPE_SIZE(uint64_t UINT64_T)
CHECK_TYPE_SIZE(uintmax_t UINTMAX_T)

CHECK_TYPE_SIZE("short" SIZE_OF_SHORT)
CHECK_TYPE_SIZE("int" SIZE_OF_INT)
CHECK_TYPE_SIZE("long" SIZE_OF_LONG)
CHECK_TYPE_SIZE("long long" SIZE_OF_LONG_LONG)

CHECK_TYPE_SIZE("unsigned short" SIZE_OF_UNSIGNED_SHORT)
CHECK_TYPE_SIZE("unsigned" SIZE_OF_UNSIGNED)
CHECK_TYPE_SIZE("unsigned long" SIZE_OF_UNSIGNED_LONG)
CHECK_TYPE_SIZE("unsigned long long" SIZE_OF_UNSIGNED_LONG_LONG)
CHECK_TYPE_SIZE("size_t" SIZEOF_SIZE_T)

CHECK_TYPE_SIZE("__int64" __INT64)
CHECK_TYPE_SIZE("unsigned __int64" UNSIGNED___INT64)

CHECK_TYPE_SIZE(uintptr_t UINTPTR_T)
IF(NOT HAVE_UINTPTR_T)
  IF("${CMAKE_SIZEOF_VOID_P}" EQUAL 8)
    SET(uintptr_t "uint64_t")
  ELSE()
    SET(uintptr_t "uint32_t")
  ENDIF()
ENDIF()


SET(LZMA_SRCS
  common/sysdefs.h
  common/tuklib_integer.h
  liblzma/check/check.c
  liblzma/check/crc32_fast.c
  liblzma/check/crc32_table.c
  liblzma/check/crc64_fast.c
  liblzma/check/crc64_table.c
  liblzma/check/sha256.c
  liblzma/common/alone_decoder.c
  liblzma/common/alone_encoder.c
  liblzma/common/auto_decoder.c
  liblzma/common/block_buffer_decoder.c
  liblzma/common/block_buffer_encoder.c
  liblzma/common/block_decoder.c
  liblzma/common/block_encoder.c
  liblzma/common/block_header_decoder.c
  liblzma/common/block_header_encoder.c
  liblzma/common/block_util.c
  liblzma/common/common.c
  liblzma/common/easy_buffer_encoder.c
  liblzma/common/easy_decoder_memusage.c
  liblzma/common/easy_encoder.c
  liblzma/common/easy_encoder_memusage.c
  liblzma/common/easy_preset.c
  liblzma/common/filter_buffer_decoder.c
  liblzma/common/filter_buffer_encoder.c
  liblzma/common/filter_common.c
  liblzma/common/filter_decoder.c
  liblzma/common/filter_encoder.c
  liblzma/common/filter_flags_decoder.c
  liblzma/common/filter_flags_encoder.c
  liblzma/common/index.c
  liblzma/common/index_decoder.c
  liblzma/common/index_encoder.c
  liblzma/common/index_hash.c
  liblzma/common/stream_buffer_decoder.c
  liblzma/common/stream_buffer_encoder.c
  liblzma/common/stream_decoder.c
  liblzma/common/stream_encoder.c
  liblzma/common/stream_flags_common.c
  liblzma/common/stream_flags_decoder.c
  liblzma/common/stream_flags_encoder.c
  liblzma/common/vli_decoder.c
  liblzma/common/vli_encoder.c
  liblzma/common/vli_size.c
  liblzma/delta/delta_common.c
  liblzma/delta/delta_decoder.c
  liblzma/delta/delta_encoder.c
  liblzma/lz/lz_decoder.c
  liblzma/lz/lz_encoder.c
  liblzma/lz/lz_encoder_mf.c
  liblzma/lzma/fastpos_table.c
  liblzma/lzma/lzma2_decoder.c
  liblzma/lzma/lzma2_encoder.c
  liblzma/lzma/lzma_decoder.c
  liblzma/lzma/lzma_encoder.c
  liblzma/lzma/lzma_encoder_optimum_fast.c
  liblzma/lzma/lzma_encoder_optimum_normal.c
  liblzma/lzma/lzma_encoder_presets.c
  liblzma/rangecoder/price_table.c
  liblzma/simple/arm.c
  liblzma/simple/armthumb.c
  liblzma/simple/ia64.c
  liblzma/simple/powerpc.c
  liblzma/simple/simple_coder.c
  liblzma/simple/simple_decoder.c
  liblzma/simple/simple_encoder.c
  liblzma/simple/sparc.c
  liblzma/simple/x86.c
  )

CONFIGURE_FILE(config.h.in config.h @ONLY)

ADD_LIBRARY(cmliblzma STATIC ${LZMA_SRCS})

target_include_directories(
  cmliblzma PUBLIC
  "${CMLIBLZMA_SOURCE_DIR}/common"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/api"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/check"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/common"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/delta"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/lz"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/lzma"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/rangecoder"
  "${CMLIBLZMA_SOURCE_DIR}/liblzma/simple"
  "${CMLIBLZMA_BINARY_DIR}"
  )

if (MSVC)
	target_compile_definitions(cmliblzma PRIVATE -D_SCL_SECURE_NO_WARNINGS)
else ()
        target_compile_options(cmliblzma PRIVATE
            -Wall
            -Wno-long-long -Wno-variadic-macros
            -Wno-pedantic -Wno-unused-parameter -Wno-shadow
            -Wno-implicit-fallthrough)
endif()
