# Copyright 2017 The TensorFlow Lattice Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# ==============================================================================
licenses(["notice"])  # Apache 2.0 License

exports_files(["LICENSE"])

package(
    default_visibility = [
        "//tensorflow_lattice:__subpackages__",
    ],
)

load(
    "//tensorflow_lattice:tensorflow.bzl",
    "tf_cc_test",
    "tf_gen_op_libs",
    "tf_custom_op_library",
)

tf_custom_op_library(
    name = "ops/_lattice_ops.so",
    srcs = [
        ":ops/lattice_interpolation_ops.cc",
        ":ops/monotone_lattice_ops.cc",
    ],
    deps = [
        "//tensorflow_lattice/cc/kernels:lattice_kernels",
        "//tensorflow_lattice/cc/lib:lattice_structure",
    ],
)

tf_custom_op_library(
    name = "ops/_pwl_calibration_ops.so",
    srcs = [
        ":ops/monotonic_projection_op.cc",
        ":ops/pwl_indexing_calibrator_ops.cc",
    ],
    deps = [
        "//tensorflow_lattice/cc/kernels:pwl_calibration_kernels",
    ],
)

cc_library(
    name = "lattice_ops",
    deps = [
        ":lattice_interpolation_ops_op_lib",
        ":monotone_lattice_ops_op_lib",
    ],
    alwayslink = 1,
)

cc_library(
    name = "pwl_calibration_ops",
    deps = [
        ":monotonic_projection_op_op_lib",
        ":pwl_indexing_calibrator_ops_op_lib",
    ],
    alwayslink = 1,
)

# Collection of operators.
tf_gen_op_libs(
    op_lib_names = ["pwl_indexing_calibrator_ops"],
    deps = [
        "//tensorflow_lattice/cc/kernels:pwl_indexing_calibrator_kernels",
        "@org_tensorflow//tensorflow/core:lib",
    ],
)

tf_gen_op_libs(
    op_lib_names = ["monotonic_projection_op"],
    deps = [
        "//tensorflow_lattice/cc/kernels:monotonic_projection_kernel",
        "@org_tensorflow//tensorflow/core:lib",
    ],
)

tf_gen_op_libs(
    op_lib_names = ["lattice_interpolation_ops"],
    deps = [
        "//tensorflow_lattice/cc/kernels:hypercube_interpolation_kernels",
        "//tensorflow_lattice/cc/kernels:lattice_interpolation_base",
        "//tensorflow_lattice/cc/kernels:simplex_interpolation_kernels",
        "//tensorflow_lattice/cc/lib:lattice_structure",
        "@org_tensorflow//tensorflow/core:lib",
    ],
)

tf_gen_op_libs(
    op_lib_names = ["monotone_lattice_ops"],
    deps = [
        "//tensorflow_lattice/cc/kernels:monotone_lattice_kernels",
        "//tensorflow_lattice/cc/lib:lattice_structure",
        "@org_tensorflow//tensorflow/core:lib",
    ],
)

# C++ tests.
cc_library(
    name = "test_main",
    testonly = 1,
    srcs = ["test_tools/test_main.cc"],
    deps = [
        "@org_tensorflow//tensorflow/core:test",
    ],
)

tf_cc_test(
    name = "pwl_indexing_calibrator_ops_test",
    size = "small",
    srcs = ["ops/pwl_indexing_calibrator_ops_test.cc"],
    deps = [
        ":pwl_indexing_calibrator_ops_op_lib",
        ":test_main",
        "@org_tensorflow//tensorflow/core:framework",
        "@org_tensorflow//tensorflow/core:lib",
        "@org_tensorflow//tensorflow/core:test",
        "@org_tensorflow//tensorflow/core:testlib",
        "@org_tensorflow//tensorflow/core/kernels:ops_testutil",
    ],
)

tf_cc_test(
    name = "hypercube_interpolation_ops_test",
    size = "small",
    srcs = ["ops/hypercube_interpolation_ops_test.cc"],
    deps = [
        ":lattice_interpolation_ops_op_lib",
        ":test_main",
        "@org_tensorflow//tensorflow/core:framework",
        "@org_tensorflow//tensorflow/core:lib",
        "@org_tensorflow//tensorflow/core:test",
        "@org_tensorflow//tensorflow/core:testlib",
        "@org_tensorflow//tensorflow/core/kernels:ops_testutil",
    ],
)

tf_cc_test(
    name = "simplex_interpolation_ops_test",
    size = "small",
    srcs = ["ops/simplex_interpolation_ops_test.cc"],
    deps = [
        ":lattice_interpolation_ops_op_lib",
        ":test_main",
        "@org_tensorflow//tensorflow/core:framework",
        "@org_tensorflow//tensorflow/core:lib",
        "@org_tensorflow//tensorflow/core:test",
        "@org_tensorflow//tensorflow/core:testlib",
        "@org_tensorflow//tensorflow/core/kernels:ops_testutil",
    ],
)

tf_cc_test(
    name = "monotonic_projection_op_test",
    size = "small",
    srcs = ["ops/monotonic_projection_op_test.cc"],
    deps = [
        ":monotonic_projection_op_op_lib",
        ":test_main",
        "@org_tensorflow//tensorflow/core:framework",
        "@org_tensorflow//tensorflow/core:lib",
        "@org_tensorflow//tensorflow/core:test",
        "@org_tensorflow//tensorflow/core:testlib",
        "@org_tensorflow//tensorflow/core/kernels:ops_testutil",
    ],
)
