cmake_minimum_required(VERSION 3.0)

set(SRC_C_FILES
    arraylist.c
    avl-tree.c
    binary-heap.c
    binomial-heap.c
    bloom-filter.c
    compare-int.c
    compare-pointer.c
    compare-string.c
    hash-int.c
    hash-pointer.c
    hash-string.c
    hash-table.c
    list.c
    queue.c
    rb-tree.c
    set.c
    slist.c
    sortedarray.c
    trie.c
)

set(SRC_H_MASTER_FILE libcalg.h)

set(SRC_H_FILES
    arraylist.h
    avl-tree.h
    binary-heap.h
    binomial-heap.h
    bloom-filter.h
    compare-int.h
    compare-pointer.h
    compare-string.h
    hash-int.h
    hash-pointer.h
    hash-string.h
    hash-table.h
    list.h
    queue.h
    rb-tree.h
    set.h
    slist.h
    sortedarray.h
    trie.h
)

set(SRC_FILES ${SRC_C_FILES} ${SRC_H_FILES} ${SRC_C_H_MASTER_FILE})
add_library(calg-shared SHARED ${SRC_FILES})
set_target_properties(calg-shared PROPERTIES OUTPUT_NAME calg)
add_library(calg-static STATIC ${SRC_FILES})
set_target_properties(calg-static PROPERTIES OUTPUT_NAME calg)

target_include_directories(calg-shared PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)

target_include_directories(calg-static PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)

install(TARGETS calg-shared calg-static
        EXPORT calg-config
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
install(FILES ${SRC_H_MASTER_FILE} DESTINATION include/libcalg-1.0)
install(FILES ${SRC_H_FILES} DESTINATION include/libcalg-1.0/libcalg)

install(EXPORT calg-config DESTINATION lib/cmake/CAlg)
export(TARGETS calg-shared calg-static FILE calg-config.cmake)
