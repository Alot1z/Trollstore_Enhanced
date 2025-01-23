THEOS_PACKAGE_SCHEME = rootless
THEOS_DEVICE_IP = 127.0.0.1
THEOS_DEVICE_PORT = 22

ARCHS = arm64 arm64e
TARGET = iphone:17.0:14.0

# SDK Configuration
SDK = iphoneos
SYSROOT = $(THEOS)/sdks/iPhoneOS17.0.sdk

# Build Settings
DEBUG = 0
FINALPACKAGE = 1
GO_EASY_ON_ME = 0

# Optimization and Security
OPTIMIZATION_LEVEL = 3
STRIP = 1
SEPARATE_STRIP = 0

# Code Signing
CODESIGN_IPA = 0
FAKE_CODE_SIGN = 1

# Include Theos Rules
include $(THEOS)/makefiles/common.mk

# Project Configuration
TWEAK_NAME = TrollStoreEnhanced
TrollStoreEnhanced_FILES = Core/Tweak.x Core/TSEnvironmentManager.m
TrollStoreEnhanced_CFLAGS = -fobjc-arc
TrollStoreEnhanced_FRAMEWORKS = UIKit Foundation Security
TrollStoreEnhanced_PRIVATE_FRAMEWORKS = MobileCoreServices

# Include Project Settings
include Makefile.common

# Build Rules
include $(THEOS_MAKE_PATH)/tweak.mk

# Post Build Actions
after-stage::
	@echo "Applying entitlements..."
	@ldid -S$(THEOS_STAGING_DIR)/entitlements.plist $(THEOS_STAGING_DIR)/Library/MobileSubstrate/DynamicLibraries/TrollStoreEnhanced.dylib

after-install::
	install.exec "killall -9 SpringBoard"

# Clean Rules
clean::
	rm -rf packages/*
	rm -rf .theos
