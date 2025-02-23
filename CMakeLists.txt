# Copyright 2018 Mike Dev
# Distributed under the Boost Software License, Version 1.0.
# See accompanying file LICENSE_1_0.txt or copy at https://www.boost.org/LICENSE_1_0.txt

if(NOT DEFINED IDF_TARGET)

cmake_minimum_required( VERSION 3.5...3.20 )
project( boost_mpl VERSION "${BOOST_SUPERPROJECT_VERSION}" LANGUAGES CXX )

add_library( boost_mpl INTERFACE )
add_library( Boost::mpl ALIAS boost_mpl )

target_include_directories( boost_mpl INTERFACE include )

target_link_libraries( boost_mpl
    INTERFACE
        Boost::config
        Boost::core
        Boost::predef
        Boost::preprocessor
        Boost::static_assert
        Boost::type_traits
        Boost::utility
)

else()

FILE(GLOB_RECURSE headers include/*.h include/*.hpp)

idf_component_register(
    SRCS
        ${headers}
    INCLUDE_DIRS
        include
    REQUIRES
        boost_config
        boost_core
        boost_predef
        boost_preprocessor
        boost_static_assert
        boost_type_traits
        boost_utility
)

endif()
