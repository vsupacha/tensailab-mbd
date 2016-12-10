# tensailab-mbd 
Collection of MATLAB scripts and Simulink models related to model-based development. 

## Contents
### Arduino directory
A collection of Simulink models that extend features of Simulink Support Package for Arduino Hardware.

### FRDM directory
A collection of Simulink models that extend features of NXP FRDM-KL25Z Microcontroller Support from Simulink Coder. 

### RPi directory
A collection of Simulink models that extend features of Hardware Support Package for Raspberry Pi.

### STM32 directory
A collection of Simulink models that extends features of ST Discovery Board Support from Embedded Coder.

## Device driver development
### Custom library 
1. Create new **Library**.
2. Make model that enclosed operations within **Subsystem** block.
3. Unlock library by clicking at bottom-left corner.
4. Copy **Subsystem** block into library.
5. To make sublibrary, add **Subsystem** block and delete input/output ports.
 
### MATLAB System block
1. Place **MATLAB System** block and create a new Simulink-extension m-file.
2. Add **coder.ExternalDependency** as another template class.
3. Modify class name at the first line and constructor.
4. Modify constructor method.
```Matlab
coder.allowpcode('plain');
```
5. Modify setupImpl(), stepImpl() and add releaseImpl() methods with C-code invocation.
```Matlab
if coder.target('Rtw')
    coder.cinclude('put C header file here');
    coder.ceval('put C source file here');
elseif ( coder.target('Sfun') )
    % Place simulation termination code here
end
```
6. Add getDescriptiveName(), isSupportedContext(context) and updateBuildInfo() methods for building information.

## References
1. [Create a Custom Library](https://www.mathworks.com/help/simulink/ug/creating-block-libraries.html).
2. [Structure of Device Driver System Object](https://www.mathworks.com/help/supportpkg/arduino/ug/introduction-to-device-drivers-and-system-objects.html).
3. 