---
UID: NF:ndis.NdisMResetComplete
title: NdisMResetComplete macro (NDIS 5.x)
description: The NdisMResetComplete function returns the final status of a reset request for which the miniport driver previously returned NDIS_STATUS_PENDING.
old-location: netvista\ndismresetcomplete.htm
tech.root: netvista
ms.date: 05/02/2018
keywords: ["NdisMResetComplete macro"]
ms.keywords: NdisMResetComplete, NdisMResetComplete function [Network Drivers Starting with Windows Vista], miniport_ndis_functions_ref_cea3e0dd-c6cb-49a7-86e3-68b779a355d2.xml, ndis/NdisMResetComplete, netvista.ndismresetcomplete
req.header: ndis.h
req.include-header: Ndis.h
req.target-type: Universal
req.target-min-winverclnt: Supported in NDIS 5.1, and NDIS 6.0 and later. For NDIS 5.1 drivers, see    NdisMResetComplete (NDIS 5.1).
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.ddi-compliance: Irql_Miniport_Driver_Function
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: Ndis.lib
req.dll: 
req.irql: DISPATCH_LEVEL
targetos: Windows
req.typenames: 
f1_keywords:
 - NdisMResetComplete
 - ndis/NdisMResetComplete
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - LibDef
api_location:
 - ndis.lib
 - ndis.dll
api_name:
 - NdisMResetComplete
---

# NdisMResetComplete macro (NDIS 5.x)


## -description

> [!NOTE]
> For NDIS 6.x (Windows Vista and later), use the [NdisMResetComplete function (NDIS 6.x)](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete-r1) instead.

The 
  <b>NdisMResetComplete</b> function returns the final status of a reset request for which the miniport driver
  previously returned NDIS_STATUS_PENDING.

## -parameters

### -param _M

The miniport adapter handle that NDIS originally passed to the 
     <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize">MiniportInitializeEx</a> function.

### -param _S

The final status of the reset operation just completed. The return values are the same as those listed for the [MINIPORT_RESET callback function](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset).

### -param _A

A Boolean value that is <b>TRUE</b> if NDIS is responsible for restoring the settings for multicast
     addresses, packet filters, and task offload information. In this case, the miniport driver is
     responsible for restoring the rest of the configuration settings for the network interface card (NIC)
     referenced by 
     <i>MiniportAdapterHandle</i> . 
     

If 
     <i>AddressingReset</i> is <b>FALSE</b>, the miniport driver is responsible for restoring all of the
     configuration settings for the NIC.

For more information, see 
     <a href="/windows-hardware/drivers/network/hardware-reset">Hardware Reset</a>.

## -remarks

If the 
    <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset">MiniportResetEx</a> function returns
    NDIS_STATUS_PENDING, the miniport driver must call 
    <b>NdisMResetComplete</b> when it completes the reset operation.

Protocol drivers cannot initiate a reset operation in NDIS 6.0 and later versions.

Some NICs lose all multicast address, packet filter, or functional address information when a soft
    reset is issued. The driver of such a NIC sets 
    <i>AddressingReset</i> to <b>TRUE</b> when it calls 
    <b>NdisMResetComplete</b>, causing NDIS to call its 
    <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request">MiniportOidRequest</a> function to
    restore the addressing state. For more information, see 
    <a href="/windows-hardware/drivers/network/hardware-reset">Hardware Reset</a>.

A miniport driver must release any spin lock that it is holding before calling 
    <b>NdisMResetComplete</b>.

In NDIS 6.0 and later, callers of 
    <b>NdisMResetComplete</b> must run at IRQL <= DISPATCH_LEVEL. Otherwise, callers of 
    <b>NdisMResetComplete</b> must run at IRQL = DISPATCH_LEVEL.

## -see-also

<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize">MiniportInitializeEx</a>



<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request">MiniportOidRequest</a>



<a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset">MiniportResetEx</a>

[NdisMResetComplete function (NDIS 6.x)](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete-r1)