catkin_install_python(PROGRAMS
  scripts/detect.py
  scripts/extract_images.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
