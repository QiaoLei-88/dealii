## ------------------------------------------------------------------------
##
## SPDX-License-Identifier: LGPL-2.1-or-later
## Copyright (C) 2012 - 2025 by the deal.II authors
##
## This file is part of the deal.II library.
##
## Part of the source code is dual licensed under Apache-2.0 WITH
## LLVM-exception OR LGPL-2.1-or-later. Detailed license information
## governing the source code and code contributions can be found in
## LICENSE.md and CONTRIBUTING.md at the top level directory of deal.II.
##
## ------------------------------------------------------------------------

set(_unity_include_src
  data_out.cc
  data_out_faces.cc
  data_out_rotation.cc
  data_out_stack.cc
  data_postprocessor.cc
  dof_output_operator.cc
  histogram.cc
  matrix_tools_once.cc
  matrix_tools.cc
  time_dependent.cc
  vector_tools_boundary.cc
  vector_tools_constraints.cc
  vector_tools_mean_value.cc
  vector_tools_point_gradient.cc
  vector_tools_rhs.cc
  )

set(_separate_src
  cell_data_transfer.cc
  data_out_dof_data_inst1.cc
  data_out_dof_data_inst2.cc
  data_out_dof_data_codim.cc
  data_out_resample.cc
  derivative_approximation.cc
  error_estimator_1d.cc
  error_estimator_inst1.cc
  error_estimator_inst2.cc
  fe_field_function.cc
  matrix_creator_inst1.cc
  matrix_creator_inst2.cc
  matrix_creator_inst3.cc
  point_value_history.cc
  smoothness_estimator.cc
  solution_transfer_inst1.cc
  solution_transfer_inst2.cc
  solution_transfer_inst3.cc
  solution_transfer_inst4.cc
  vector_tools_integrate_difference.cc
  vector_tools_interpolate.cc
  vector_tools_point_value.cc
  vector_tools_project.cc
  vector_tools_project_hp.cc
  vector_tools_project_codim.cc
  vector_tools_project_qp.cc
  vector_tools_project_qpmf.cc
  )

# determined by profiling
set(_n_includes_per_unity_file 8)

setup_source_list("${_unity_include_src}"
  "${_separate_src}"
  ${_n_includes_per_unity_file}
  _src
  )

set(_inst
  cell_data_transfer.inst.in
  data_out_dof_data.inst.in
  data_out_dof_data_codim.inst.in
  data_out_faces.inst.in
  data_out.inst.in
  data_out_resample.inst.in
  data_out_rotation.inst.in
  data_out_stack.inst.in
  data_postprocessor.inst.in
  derivative_approximation.inst.in
  dof_output_operator.inst.in
  error_estimator_1d.inst.in
  error_estimator.inst.in
  fe_field_function.inst.in
  matrix_creator.inst.in
  matrix_tools.inst.in
  point_value_history.inst.in
  smoothness_estimator.inst.in
  solution_transfer.inst.in
  time_dependent.inst.in
  vector_tools_boundary.inst.in
  vector_tools_constraints.inst.in
  vector_tools_integrate_difference.inst.in
  vector_tools_interpolate.inst.in
  vector_tools_mean_value.inst.in
  vector_tools_point_value.inst.in
  vector_tools_point_gradient.inst.in
  vector_tools_project.inst.in
  vector_tools_project_codim.inst.in
  vector_tools_project_hp.inst.in
  vector_tools_project_qp.inst.in
  vector_tools_project_qpmf.inst.in
  vector_tools_rhs.inst.in
  )

file(GLOB _header CONFIGURE_DEPENDS
  ${CMAKE_SOURCE_DIR}/include/deal.II/numerics/*.h
  )

define_object_library(object_numerics OBJECT ${_src} ${_header} ${_inst})
expand_instantiations(object_numerics "${_inst}")

collect_source_and_header_files("${_unity_include_src};${_separate_src}" "${_header}")
