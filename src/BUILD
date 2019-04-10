package(default_visibility = ["//visibility:public"])
load("//tools:cpplint.bzl", "cpplint")

cc_library(
    name = "libidriving_can",
    srcs = ["libidriving_can.so"],
    hdrs = ["idriving_api.h"],
)
cc_library(
    name = "libusbcan",
    srcs = [
        "libusbcan.so",
    ],
    hdrs = ["controlcan.h"],
)

cc_library(
    name = "ads_message",
    srcs = [
        "ads_message.cc",
    ],
    hdrs = [
        "ads_message.h",
        "message_define.h",
        "message_encrypt.h",
    ],
    deps = [":message_encrypt"],

)
cc_library(
    name = "api_test",
    srcs = [
        "api_test_autodrive.c",
        "api_test_get_demo.c",
        "api_test_get.c",
        "api_test_set_demo.c",
        "api_test_set.c",
        "api_test.c",
    ],
    hdrs = [
        "api_test.h",
        "idriving_api.h",
        "controlcan.h",
        "std_types.h",
    ],
    deps = [
        ":libidriving_can",
        ":libusbcan",
    ],

)

cc_library(
    name = "async_client",
    srcs = [
        "async_client.cc",
    ],
    hdrs = [
        "async_client.h",
    ],

)
cc_library(
    name = "byd_control_thread",
    srcs = [
        "byd_control_thread.cc",
    ],
    hdrs = [
        "byd_control_thread.h",
        "control.h",
        "api_test.h",
        "idriving_api.h",
        "controlcan.h",
        "std_types.h",
        
    ],
    deps = [
        ":api_test",
        ":libidriving_can",
        ":libusbcan",
        "//modules/drivers/gnss/stream:gnss_stream",
        "//modules/common:log",
        "@ros//:ros_common",
        "//modules/canbus/common:canbus_common",
        "//modules/common/adapters:adapter_manager",
        "//modules/canbus/vehicle:vehicle_factory",
        "//modules/common",
        "//modules/common:apollo_app",
        "//modules/common/monitor_log",
        "//modules/drivers/canbus/can_client:can_client_factory",
        "//modules/drivers/canbus/can_comm:can_receiver",
        "//modules/drivers/canbus/can_comm:can_sender",
    ],

)
cc_library(
    name = "control",
    srcs = [
        "control.cc",

    ],
    hdrs = [
        "control.h",
        "std_types.h",
        "api_test.h",
        "controlcan.h",

    ],
    deps = [
        ":libidriving_can",
        ":libusbcan",

    ],

)
cc_library(
    name = "message_encrypt",
    srcs = [
        "message_encrypt.cc",
    ],
    hdrs = [
        "message_encrypt.h",
    ],

)

cc_library(
    name = "TCP_callback",
    srcs = [
        "TCP_callback.cc",
    ],
    hdrs = [
        "TCP_callback.h",
        "async_client.h",
        "message_encrypt.h"
    ],
    deps = [":ads_message"],

)

cc_library(
    name = "thread_define",
    srcs = [
        "thread_define.cc",
    ],
    hdrs = [
        "thread_define.h",
    ],

)

cc_binary(
    name = "main",
    srcs = ["main.cc"],

    deps = [
        ":api_test",
        ":ads_message",
        ":async_client",
        ":byd_control_thread",
        ":control",
        ":message_encrypt",
        ":TCP_callback",
        ":thread_define",
        ":libidriving_can",
        ":libusbcan",
        "//modules/drivers/gnss/stream:gnss_stream",
        "//modules/common:log",
	    "@ros//:ros_common",
        "//modules/canbus/common:canbus_common",
        "//modules/common/adapters:adapter_manager",

    ],
    linkopts = [
        "-L/usr/lib",
        "-lboost_system",
        "-lboost_thread",
        "-lboost_filesystem",
        "-lpthread",
        "-lstdc++",
        "-lcrypto",
        "-lm",
        "-lrt",

    ],
    
)


