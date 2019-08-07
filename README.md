# Jenkins MATLAB Plugin

## Description
The Jenkins plugin for MATLAB&reg; enables you to easily run your MATLAB tests and generate test artifacts in formats such as JUnit, TAP, and Cobertura code coverage reports. 
## Build Step Configuration
To invoke this plugin, select "Run MATLAB Tests" from the Add build step list.

  ![new_add_build_step](https://user-images.githubusercontent.com/47204011/55624172-be54a100-57c2-11e9-9596-52d3a60ee467.png)
  
  ![new_default_plugin_page](https://user-images.githubusercontent.com/47204011/55624213-dcba9c80-57c2-11e9-85e6-abb6ae03534e.png)

Use the plugin as part of the Jenkins build step to run MATLAB tests in two distinct modes:
* Automatic
* Custom

Enter the value returned by “matlabroot” in the field named “MATLAB root”.

  ![new_enter_matlabroot](https://user-images.githubusercontent.com/47204011/55624374-45097e00-57c3-11e9-96e1-5fa0fc966767.png)
  
#### Configuring “Automatic” Option
This option finds tests written using the MATLAB unit testing framework and/or Simulink Test and runs them. If the code is organized using projects, it will locate all test files in the project that have been classified as "Test". If the code does not leverage projects or uses a MATLAB version prior to R2019a, the plugin will discover all tests in the current Jenkins workspace including subfolders. 

If you are using a source code management (SCM) system such as Git, then the job must include an appropriate SCM configuration to check out the code before running the MATLAB plugin. If you do not use any SCM systems to manage your code, then an additional build step is required to ensure the code is available in the workspace before running the MATLAB plugin.

The automatic test running feature enables you to generate different types of test artifacts. They could be used with other Jenkins plugins as part of a post-build action to publish the test results. To configure the Jenkins build for running MATLAB tests automatically, follow these steps.

1) Select the Test mode as Automatic to run tests (Automatic is the default mode).
  
  ![new_select_automatic_option](https://user-images.githubusercontent.com/47204011/55624469-a0d40700-57c3-11e9-8811-32892ccbe673.png)
  
2) Select the desired test artifacts. You can also choose not to generate any test artifacts.

  ![new_select_all_test_artifacts](https://user-images.githubusercontent.com/47204011/55624765-7f274f80-57c4-11e9-8a15-ebdef19ebd3d.png)

  The selected test artifact(s) will be stored in the “matlabTestArtifacts” folder of the Jenkins workspace.

  ![Workspace01](https://user-images.githubusercontent.com/47204011/55470859-1e621080-5626-11e9-98f2-044144272643.JPG)
  
  ![Test_artifacts](https://user-images.githubusercontent.com/47204011/55470863-21f59780-5626-11e9-9765-4d79a6fd4061.JPG)
  
  If the user does not select any test artifact generation checkboxes, this folder will not be created under the workspace and no test artifacts will be generated. However, test execution still occurs and test failures will fail the build. 

  The Automatic test run mode generates a MATLAB script file named “runMatlabTests.m” in the Jenkins workspace. The plugin uses this file to run tests and generate test artifacts. You may review the MATLAB script to understand the test workflow.

  ![Workspace01](https://user-images.githubusercontent.com/47204011/55470859-1e621080-5626-11e9-98f2-044144272643.JPG)


#### Configuring “Custom” Option
This option enables you to develop your custom MATLAB commands for running tests.

1) From the "Test mode" dropdown list, select “Custom” option.

  ![new_select_custom](https://user-images.githubusercontent.com/47204011/55624858-d0cfda00-57c4-11e9-8366-45edbc9ba83f.png)

2) In "MATLAB command” text box, enter your MATLAB command. Separate multiple commands by commas or semicolons.

  ![new_custom_runtest_command](https://user-images.githubusercontent.com/47204011/55624949-096fb380-57c5-11e9-8711-98baf91816c0.png)

  Note: If you require several MATLAB commands to execute your test session, consider writing a MATLAB script or function as part of your repository and executing the script or function instead. Test artifacts are not autogenerated if you choose to run tests using your custom MATLAB commands. You can generate these and other artifacts by configuring a test runner in the script or function invoked by the command. The build will fail if the execution of any MATLAB command causes an error.

  ![new_custom_script_example](https://user-images.githubusercontent.com/47204011/55625021-32904400-57c5-11e9-86b7-478b930796c0.png)

## Configuring "Multi-configuration"(matrix) project.
The Jenkins plugin for MATLAB can be used inside of "Multi-configuration" (matrix) projects. Matrix projects allow jobs to be repeated with different configurations, such as testing on multiple platforms or testing against multiple MATLAB versions.

#### Matrix build for "Automatic" option.

1) Create a "Multi-configuration" project.

![image](https://user-images.githubusercontent.com/47204011/62458632-0e586a00-b79b-11e9-8611-3671adb8c289.png)

2) Add User-defined axis for different MATLAB versions as shown below.

![image](https://user-images.githubusercontent.com/47204011/62459358-c6d2dd80-b79c-11e9-90dc-37891b8179ea.png)

3) Replace the user defined axis variable in MATLAB root appropriately.

![image](https://user-images.githubusercontent.com/47204011/62459137-3c8a7980-b79c-11e9-9bee-305b4cabfd42.png)

4) Save and run the build.

#### Matrix build for "Custom" option.

1) Create a "Multi-configuration" project.

![image](https://user-images.githubusercontent.com/47204011/62458632-0e586a00-b79b-11e9-8611-3671adb8c289.png)

2) Add User-defined axis for different MATLAB versions as shown below.

![image](https://user-images.githubusercontent.com/47204011/62459358-c6d2dd80-b79c-11e9-90dc-37891b8179ea.png)

3) Add another User-defined axis for custom commands as shown below.

![image](https://user-images.githubusercontent.com/47204011/62517774-b6c30880-b845-11e9-86a0-8344a281fb27.png)

4) Replace the user defined axis variable in MATLAB root appropriately.

![image](https://user-images.githubusercontent.com/47204011/62459137-3c8a7980-b79c-11e9-9bee-305b4cabfd42.png)

5) Select "Custom" option from "Test mode" drop-down and replace user defined axis variable for custom command appropriately.

![image](https://user-images.githubusercontent.com/47204011/62518329-f3dbca80-b846-11e9-911f-82dfc3fcdd32.png)

4) Save and run the build.


Note: Axis variables can be replaced in either "$VAR" or "${VAR}" formats. Do not use complete MATLAB root path as axis values. Multi-configuration project creates separate workspace folder for each user defined axis values with same name, and file separators in complete path will cause Jenkins build to fail as folder creation fails.

## Contact Us
If you have any questions or suggestions, please feel free to contact MathWorks.

support@mathworks.com

## License
MIT © 2019 The MathWorks, Inc.


## Build Results


| Overall  | Linux  | Windows  | Mac  |
|---|---|---|---|
| [![Build Status](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_apis/build/status/mathworks.jenkins-matlab-plugin?branchName=master)](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_build/latest?definitionId=6&branchName=master) |[![Build Status](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_apis/build/status/mathworks.jenkins-matlab-plugin?branchName=master&jobName=Job&configuration=linux)](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_build/latest?definitionId=6&branchName=master) |[![Build Status](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_apis/build/status/mathworks.jenkins-matlab-plugin?branchName=master&jobName=Job&configuration=windows)](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_build/latest?definitionId=6&branchName=master) |[![Build Status](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_apis/build/status/mathworks.jenkins-matlab-plugin?branchName=master&jobName=Job&configuration=mac)](https://dev.azure.com/iat-ci/jenkins-matlab-plugin/_build/latest?definitionId=6&branchName=master) |
