---
title: ミニポートドライバーの表示機能の DriverEntry
description: DriverEntry 関数は、ディスプレイミニポートドライバーによって実装されている関数へのポインターのセットを使用して、Microsoft DirectX graphics カーネルサブシステムを提供します。
ms.assetid: 64b4e9d5-eb6e-48ab-95bf-a237ec32a54b
keywords:
- DriverEntry 関数のディスプレイデバイス
topic_type:
- apiref
api_name:
- DriverEntry
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c3172528cbd203a2154f1c45ea6c3a75005e95f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838984"
---
# <a name="driverentry-of-display-miniport-driver-function"></a>ミニポートドライバーの表示機能の DriverEntry


**Driverentry**関数は、ディスプレイミニポートドライバーによって実装されている関数へのポインターのセットを使用して、Microsoft DirectX graphics カーネルサブシステムを提供します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>パラメーター
----------

*Driverobject* \[、(表示ミニポート、ディスプレイポート) ドライバーのペアによって形成されたドライバーを表すドライバー [ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造へのポインター\] ます。

*RegistryPath* \[、ドライバーのレジストリキーへのパスを指定する[**UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)構造体へのポインター\] ます。

<a name="return-value"></a>戻り値
------------

**Driverentry**は[**dxgkinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)を呼び出し、 **dxgkinitialize**によって返された値を返す必要があります。

<a name="remarks"></a>注釈
-------

**Driverentry**では、次の手順を実行する必要があります。

1.  [**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)構造体を割り当て、その**バージョン**メンバーを dxgkddi\_INTERFACE\_version に設定します。これは、dispmprt. h で定義されています。

2.  ドライバーの残りのメンバーに、 [ **\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)構造を入力します。これらの関数は、ディスプレイミニポートドライバーによって実装されています。

    -   [*DxgkDdiAcquireSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_acquireswizzlingrange)
    -   [*DxgkDdiAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_add_device)
    -   [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)
    -   [*DxgkDdiCalibrateGpuClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WDDM1\_3)
    -   [*DxgkDdiCancelCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_cancelcommand) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiCheckMultiPlaneOverlaySupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiCloseAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_closeallocation)
    -   [*DxgkDdiCollectDbgInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_collectdbginfo)
    -   [*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)
    -   [*DxgkDdiControlEtwLogging*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_control_etw_logging)
    -   [*DxgkDdiControlInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_controlinterrupt)
    -   [*DxgkDdiCreateAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)
    -   [*DxgkDdiCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)
    -   [*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)
    -   [*DxgkDdiCreateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createoverlay)
    -   [*DxgkDdiDescribeAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_describeallocation)
    -   [*DxgkDdiDestroyAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyallocation)
    -   [*DxgkDdiDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroycontext)
    -   [*DxgkDdiDestroyDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroydevice)
    -   [*DxgkDdiDestroyOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_destroyoverlay)
    -   [*DxgkDdiDispatchIoRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dispatch_io_request)
    -   [*DxgkDdiDpcRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_dpc_routine)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)
    -   [*DxgkDdiEscape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_escape)
    -   [*DxgkDdiFlipOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_flipoverlay)
    -   [*DxgkDdiFormatHistoryBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetChildContainerId*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_get_child_container_id) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetNodeMetadata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getnodemetadata) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetScanLine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getscanline)
    -   [*DxgkDdiGetStandardAllocationDriverData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)
    -   [*DxgkDdiInterruptRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)
    -   [*DxgkDdiIsSupportedVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)
    -   [*DxgkDdiLinkDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_link_device)
    -   [*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) (省略可能)
    -   [*DxgkDdiNotifySurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_surprise_removal) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiOpenAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_openallocationinfo)
    -   [*DxgkDdiPatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)
    -   [*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiPreemptCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_preemptcommand)
    -   [*DxgkDdiPresent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)
    -   [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)
    -   [*DxgkDdiQueryChildRelations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)
    -   [*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)
    -   [*DxgkDdiQueryCurrentFence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querycurrentfence)
    -   [*DxgkDdiQueryDependentEngineGroup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_querydependentenginegroup) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)
    -   [*DxgkDdiQueryEngineStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryenginestatus) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)
    -   [*DxgkDdiQueryVidPnHWCapability*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN7)
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)
    -   [*DxgkDdiRecommendMonitorModes*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendmonitormodes)
    -   [*DxgkDdiRecommendVidPnTopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)
    -   [*DxgkDdiReleaseSwizzlingRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange)
    -   [*DxgkDdiRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_remove_device)
    -   [*DxgkDdiRender*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)
    -   [*DxgkDdiRenderKm*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN7)
    -   [*DxgkDdiResetDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_reset_device)
    -   [*DxgkDdiResetEngine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetengine) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiResetFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)
    -   [*DxgkDdiRestartFromTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout)
    -   [*DxgkDdiSetDisplayPrivateDriverFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setdisplayprivatedriverformat)
    -   [*DxgkDdiSetPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpalette)
    -   [*DxgkDdiSetPointerPosition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)
    -   [*DxgkDdiSetPointerShape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)
    -   [*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)
    -   [*DxgkDdiSetVidPnSourceAddress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560767(v=vs.85))
    -   [*DxgkDdiSetVidPnSourceVisibility*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourcevisibility)
    -   [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)
    -   [*DxgkDdiStopCapture*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)
    -   [*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)
    -   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSubmitCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)
    -   [*DxgkDdiSystemDisplayEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_enable) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSystemDisplayWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_write) (dxgkddi\_INTERFACE\_version &gt;= dxgkddi\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_unload)
    -   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateactivevidpnpresentpath)
    -   [*DxgkDdiUpdateOverlay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updateoverlay)


3.  *Driverobject*、 *RegistryPath*、および入力された[**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)構造を[**dxgkinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)に渡します。

4.  [**Dxgkinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)によって返された値を返します。

**Driverentry**が返された後、[**ドライバー\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)構造をメモリ内に保持する必要はありません。

**Driverentry**は、ページング可能にする必要があります。

カーネルモード表示専用ドライバー (KMDOD) インターフェイスの場合、 [KMDDOD_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_kmddod_initialization_data)構造体には、KMDOD によって実装できるすべての関数が一覧表示されます。 [DxgkDdiPresentDisplayOnly](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_presentdisplayonly)関数を除くこれらのすべての関数は、フルディスプレイミニポートドライバーによって実装することもできます。  カーネルモード表示専用ドライバー (KMDOD) の DriverEntry 関数は、KMDDOD_INITIALIZATION_DATA 構造体のすべてのメンバーを入力し、その構造体を次のように渡すことによって、[ディスプレイポートドライバーへの関数ポインターを提供します。DxgkInitializeDisplayOnlyDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitializedisplayonlydriver)関数。

KMDOD で垂直コントロール機能がサポートされていない場合は、特定の関数を実装しないようにする必要があります。「垂直コントロールを使用してエネルギーを節約する」を参照してください。

カーネルモードの表示専用ドライバーでは、次の構造と列挙も使用されます。

* [D3DKMT_MOVE_RECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmt_move_rect)
* [D3DKMT_PRESENT_DISPLAY_ONLY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_d3dkmt_present_display_only_flags)
* [DXGK_PRESENT_DISPLAY_ONLY_PROGRESS_ID](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_present_display_only_progress_id)
* [DXGKARG_PRESENT_DISPLAYONLY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_present_displayonly)
* [DXGKARGCB_PRESENT_DISPLAYONLY_PROGRESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_present_displayonly_progress)


<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">Ntoskrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DxgkInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nf-dispmprt-dxgkinitialize)

[*DxgkDdiUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_unload)

 

 






