---
UID: NE:wdm._POWER_REQUEST_TYPE
title: _POWER_REQUEST_TYPE (wdm.h)
description: The POWER_REQUEST_TYPE enumeration indicates the power request type.
old-location: kernel\power_request_type.htm
tech.root: kernel
ms.date: 04/30/2018
keywords: ["POWER_REQUEST_TYPE enumeration"]
ms.keywords: "*PPOWER_REQUEST_TYPE, POWER_REQUEST_TYPE, POWER_REQUEST_TYPE enumeration [Kernel-Mode Driver Architecture], PPOWER_REQUEST_TYPE, PPOWER_REQUEST_TYPE enumeration pointer [Kernel-Mode Driver Architecture], PowerRequestAwayModeRequired, PowerRequestDisplayRequired, PowerRequestExecutionRequired, PowerRequestSystemRequired, _POWER_REQUEST_TYPE, kernel.power_request_type, sysenum_2d1a5da5-2541-4db1-bfde-2bd06f38b17c.xml, wdm/POWER_REQUEST_TYPE, wdm/PPOWER_REQUEST_TYPE, wdm/PowerRequestAwayModeRequired, wdm/PowerRequestDisplayRequired, wdm/PowerRequestExecutionRequired, wdm/PowerRequestSystemRequired"
req.header: wdm.h
req.include-header: Wdm.h, Ntddk.h, Ntifs.h, Ntpoapi.h
req.target-type: Windows
req.target-min-winverclnt: Supported starting with Windows 7.
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: 
req.dll: 
req.irql: 
targetos: Windows
req.typenames: POWER_REQUEST_TYPE, *PPOWER_REQUEST_TYPE
f1_keywords:
 - _POWER_REQUEST_TYPE
 - wdm/_POWER_REQUEST_TYPE
 - PPOWER_REQUEST_TYPE
 - wdm/PPOWER_REQUEST_TYPE
 - POWER_REQUEST_TYPE
 - wdm/POWER_REQUEST_TYPE
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - HeaderDef
api_location:
 - Wdm.h
api_name:
 - _POWER_REQUEST_TYPE
 - PPOWER_REQUEST_TYPE
 - POWER_REQUEST_TYPE
---

# _POWER_REQUEST_TYPE enumeration (wdm.h)


## -description

The <b>POWER_REQUEST_TYPE</b> enumeration indicates the power request type.

## -enum-fields

### -field PowerRequestDisplayRequired

Not used by drivers. For more information, see Remarks.

### -field PowerRequestSystemRequired

Prevents the computer from automatically entering sleep mode after a period of user inactivity.

### -field PowerRequestAwayModeRequired

Not used by drivers. For more information, see Remarks.

### -field PowerRequestExecutionRequired

Not used by drivers. For more information, see Remarks.

## -remarks

This enumeration is used by the kernel-mode <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poclearpowerrequest">PoClearPowerRequest</a> and <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerrequest">PoSetPowerRequest</a> routines. Drivers that call these routines must specify the <b>PowerRequestSystemRequired</b> enumeration value.

The other three enumeration values—<b>PowerRequestDisplayRequired</b>, <b>PowerRequestAwayModeRequired</b>, and <b>PowerRequestExecutionRequired</b>—are not used by drivers. Applications specify these power request types in calls to the <a href="/windows/win32/api/winbase/nf-winbase-powersetrequest">PowerSetRequest</a> and <a href="/windows/win32/api/winbase/nf-winbase-powerclearrequest">PowerClearRequest</a> functions.

A <b>PowerRequestDisplayRequired</b> power request has the following effects:

<ul>
<li>
After a period of user inactivity, the session display stays on and will not automatically turn off. If the display is already turned off, the power request turns the display on.
</li>

<li>
<div class="alert"><b>Note</b>  A <b>PowerRequestSystemRequired</b> must be taken in addition to a <b>PowerRequestDisplayRequired</b> to ensure the display stays on and the system does not enter sleep for the duration of the request.</div>
<div> </div>
</li>

<li>
A screensaver will not automatically start after a period of user inactivity. If a screensaver is already running, the power request stops the screensaver.

</li>
<li>
The session will not be automatically locked after a period of user inactivity. If the session is already locked when the driver sends the power request, the session remains locked.

</li>
</ul>
While a <b>PowerRequestAwayModeRequired</b> power request is in effect, if the user tries to put the computer into sleep mode (for example, by clicking <b>Start</b> and then clicking <b>Sleep</b>), the <a href="/windows-hardware/drivers/kernel/power-manager">power manager</a> turns off audio and video so that the computer appears to be in sleep mode, but the computer continues to run. This is only applicable on Traditional Sleep (S3) systems.

While a <b>PowerRequestExecutionRequired</b> power request is in effect, the calling process continues to run instead of being suspended or terminated by process lifetime management (PLM) mechanisms. When and how long the process is allowed to run depends on the operating system and power policy settings. This type of power request is supported starting with Windows 8.

On Modern Standby systems on DC power, power requests are terminated after 5 minutes.

Except for <b>PowerRequestAwayModeRequired</b> on Traditional Sleep (S3) systems, power requests are terminated upon user-initiated system sleep entry (power button, lid close or selecting Sleep from the Start menu).

## -see-also

<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poclearpowerrequest">PoClearPowerRequest</a>



<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerrequest">PoSetPowerRequest</a>



<a href="/windows/win32/api/winbase/nf-winbase-powerclearrequest">PowerClearRequest</a>



<a href="/windows/win32/api/winbase/nf-winbase-powersetrequest">PowerSetRequest</a>

