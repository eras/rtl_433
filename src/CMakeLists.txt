# Copyright 2012 OSMOCOM Project
#
# This file is part of rtl-sdr
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
# Setup library
########################################################################
add_library(rtlsdr SHARED
    rtl-sdr.c
    tuner_e4000.c
    tuner_fc0012.c
    tuner_fc0013.c
)

target_link_libraries(rtlsdr
    ${LIBUSB_LIBRARIES}
)

set_target_properties(rtlsdr PROPERTIES DEFINE_SYMBOL "rtlsdr_EXPORTS")

########################################################################
# Install built library files
########################################################################
install(TARGETS rtlsdr
    LIBRARY DESTINATION lib${LIB_SUFFIX} # .so/.dylib file
    ARCHIVE DESTINATION lib${LIB_SUFFIX} # .lib file
    RUNTIME DESTINATION bin              # .dll file
)

########################################################################
# Build utility
########################################################################
add_executable(rtl_sdr main.c)
target_link_libraries(rtl_sdr rtlsdr ${LIBUSB_LIBRARIES})