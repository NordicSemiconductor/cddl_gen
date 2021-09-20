#
# Copyright (c) 2021 Nordic Semiconductor ASA
#
# SPDX-License-Identifier: Apache-2.0
#

cmake_minimum_required(VERSION 3.13.1)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(NONE)

set(BUILD_WITH_ZEPHYR ON)

add_subdirectory(../../.. ${PROJECT_BINARY_DIR}/cddl_gen)

FILE(GLOB app_sources src/*.c)
target_sources(app PRIVATE
  ${app_sources}
  ../../fuzz/fuzz_manifest12.c)

target_cddl_source(app ../../cases/manifest12.cddl ENTRY_TYPES
  SUIT_Envelope_Tagged SUIT_Command_Sequence SUIT_Envelope
  DECODE
  ${VERBOSE}
  ${CANONICAL}
  )

zephyr_compile_options(-Werror)
