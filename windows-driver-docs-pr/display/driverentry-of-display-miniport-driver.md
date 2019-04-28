---
title: ディスプレイ ミニポート ドライバーの DriverEntry 関数
description: DriverEntry 関数は、Microsoft DirectX グラフィックス ディスプレイのミニポート ドライバーによって実装される関数へのポインターのセットでのカーネルのサブシステムを提供します。
ms.assetid: 64b4e9d5-eb6e-48ab-95bf-a237ec32a54b
keywords:
- DriverEntry 関数ディスプレイ デバイス
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
ms.openlocfilehash: 16f7b2c43dc21a2cf24a0cde9349b926a20805c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361255"
---
# <a name="driverentry-of-display-miniport-driver-function"></a>ディスプレイ ミニポート ドライバーの DriverEntry 関数


**DriverEntry**関数は Microsoft DirectX グラフィックスの一連のディスプレイのミニポート ドライバーによって実装される関数へのポインターのカーネルのサブシステムを提供します。

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

*DriverObject* \[で\]へのポインターを[**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174) (表示のミニポート、表示して、ドライバーを表す構造が形成されました。ポート) ドライバーのペア。

*RegistryPath* \[で\]へのポインターを[ **UNICODE\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff564879)ドライバーのレジストリ キーへのパスを提供する構造体。

<a name="return-value"></a>戻り値
------------

**DriverEntry**呼び出し[ **DxgkInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff560824)によって返される値を返す必要がありますと**DxgkInitialize**します。

<a name="remarks"></a>注釈
-------

**DriverEntry**次の手順を実行する必要があります。

1.  割り当て、 [**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169)構造体、および設定の**バージョン**DXGKDDI メンバー\_インターフェイス\_Dispmprt.h で定義されているのバージョン。

2.  入力の残りのメンバー、 [**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169)表示ミニポートによって実装される次の関数へのポインターを含む構造体ドライバー。

    -   [*DxgkDdiAcquireSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559582)
    -   [*DxgkDdiAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559586)
    -   [*DxgkDdiBuildPagingBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff559587)
    -   [*DxgkDdiCalibrateGpuClock*](https://msdn.microsoft.com/library/windows/hardware/dn467321) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WDDM1\_3)
    -   [*DxgkDdiCancelCommand* ](https://msdn.microsoft.com/library/windows/hardware/hh451344) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiCheckMultiPlaneOverlaySupport* ](https://msdn.microsoft.com/library/windows/hardware/dn282642) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiCloseAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559592)
    -   [*DxgkDdiCollectDbgInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559595)
    -   [*DxgkDdiCommitVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559597)
    -   [*DxgkDdiControlEtwLogging*](https://msdn.microsoft.com/library/windows/hardware/ff559599)
    -   [*DxgkDdiControlInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559602)
    -   [*DxgkDdiCreateAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559606)
    -   [*DxgkDdiCreateContext*](https://msdn.microsoft.com/library/windows/hardware/ff559612)
    -   [*DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)
    -   [*DxgkDdiCreateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559616)
    -   [*DxgkDdiDescribeAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559620)
    -   [*DxgkDdiDestroyAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559630)
    -   [*DxgkDdiDestroyContext*](https://msdn.microsoft.com/library/windows/hardware/ff559636)
    -   [*DxgkDdiDestroyDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559639)
    -   [*DxgkDdiDestroyOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559642)
    -   [*DxgkDdiDispatchIoRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559643)
    -   [*DxgkDdiDpcRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559645)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://msdn.microsoft.com/library/windows/hardware/ff559649)
    -   [*DxgkDdiEscape*](https://msdn.microsoft.com/library/windows/hardware/ff559653)
    -   [*DxgkDdiFlipOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559655)
    -   [*DxgkDdiFormatHistoryBuffer*](https://msdn.microsoft.com/library/windows/hardware/dn439360) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetChildContainerId* ](https://msdn.microsoft.com/library/windows/hardware/hh451349) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiGetNodeMetadata*](https://msdn.microsoft.com/library/windows/hardware/dn265415) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiGetScanLine*](https://msdn.microsoft.com/library/windows/hardware/ff559668)
    -   [*DxgkDdiGetStandardAllocationDriverData*](https://msdn.microsoft.com/library/windows/hardware/ff559673)
    -   [*DxgkDdiInterruptRoutine*](https://msdn.microsoft.com/library/windows/hardware/ff559680)
    -   [*DxgkDdiIsSupportedVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559684)
    -   [*DxgkDdiLinkDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559687)
    -   [*DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695) (省略可能)
    -   [*DxgkDdiNotifySurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/hh780297) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiOpenAllocation*](https://msdn.microsoft.com/library/windows/hardware/ff559699)
    -   [*DxgkDdiPatch*](https://msdn.microsoft.com/library/windows/hardware/ff559737)
    -   [*DxgkDdiPowerRuntimeControlRequest* ](https://msdn.microsoft.com/library/windows/hardware/hh451396) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiPreemptCommand*](https://msdn.microsoft.com/library/windows/hardware/ff559741)
    -   [*DxgkDdiPresent*](https://msdn.microsoft.com/library/windows/hardware/ff559743)
    -   [*DxgkDdiQueryAdapterInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559746)
    -   [*DxgkDdiQueryChildRelations*](https://msdn.microsoft.com/library/windows/hardware/ff559750)
    -   [*DxgkDdiQueryChildStatus*](https://msdn.microsoft.com/library/windows/hardware/ff559754)
    -   [*DxgkDdiQueryCurrentFence*](https://msdn.microsoft.com/library/windows/hardware/ff559758)
    -   [*DxgkDdiQueryDependentEngineGroup* ](https://msdn.microsoft.com/library/windows/hardware/hh451407) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiQueryDeviceDescriptor*](https://msdn.microsoft.com/library/windows/hardware/ff559761)
    -   [*DxgkDdiQueryEngineStatus* ](https://msdn.microsoft.com/library/windows/hardware/hh451411) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiQueryInterface*](https://msdn.microsoft.com/library/windows/hardware/ff559764)
    -   [*DxgkDdiQueryVidPnHWCapability*](https://msdn.microsoft.com/library/windows/hardware/ff559771) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN7)
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://msdn.microsoft.com/library/windows/hardware/ff559775)
    -   [*DxgkDdiRecommendMonitorModes*](https://msdn.microsoft.com/library/windows/hardware/ff559780)
    -   [*DxgkDdiRecommendVidPnTopology*](https://msdn.microsoft.com/library/windows/hardware/ff559782)
    -   [*DxgkDdiReleaseSwizzlingRange*](https://msdn.microsoft.com/library/windows/hardware/ff559786)
    -   [*DxgkDdiRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559789)
    -   [*DxgkDdiRender*](https://msdn.microsoft.com/library/windows/hardware/ff559793)
    -   [*DxgkDdiRenderKm* ](https://msdn.microsoft.com/library/windows/hardware/ff559800) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN7)
    -   [*DxgkDdiResetDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559808)
    -   [*DxgkDdiResetEngine* ](https://msdn.microsoft.com/library/windows/hardware/hh451418) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiResetFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559815)
    -   [*DxgkDdiRestartFromTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff559820)
    -   [*DxgkDdiSetDisplayPrivateDriverFormat*](https://msdn.microsoft.com/library/windows/hardware/ff560751)
    -   [*DxgkDdiSetPalette*](https://msdn.microsoft.com/library/windows/hardware/ff560754)
    -   [*DxgkDdiSetPointerPosition*](https://msdn.microsoft.com/library/windows/hardware/ff560757)
    -   [*DxgkDdiSetPointerShape*](https://msdn.microsoft.com/library/windows/hardware/ff560762)
    -   [*DxgkDdiSetPowerComponentFState* ](https://msdn.microsoft.com/library/windows/hardware/hh451422) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiSetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff560764)
    -   [*DxgkDdiSetVidPnSourceAddress*](https://msdn.microsoft.com/library/windows/hardware/ff560767)
    -   [*DxgkDdiSetVidPnSourceVisibility*](https://msdn.microsoft.com/library/windows/hardware/ff560771)
    -   [*DxgkDdiStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560775)
    -   [*DxgkDdiStopCapture*](https://msdn.microsoft.com/library/windows/hardware/ff560776)
    -   [*DxgkDdiStopDevice*](https://msdn.microsoft.com/library/windows/hardware/ff560781)
    -   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451415) (DXGKDDI\_インターフェイス\_バージョン&gt;= DXGKDDI\_インターフェイス\_バージョン\_WIN8)
    -   [*DxgkDdiSubmitCommand*](https://msdn.microsoft.com/library/windows/hardware/ff560790)
    -   [*DxgkDdiSystemDisplayEnable*](https://msdn.microsoft.com/library/windows/hardware/hh451426) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiSystemDisplayWrite*](https://msdn.microsoft.com/library/windows/hardware/hh451429) (DXGKDDI\_INTERFACE\_VERSION &gt;= DXGKDDI\_INTERFACE\_VERSION\_WIN8)
    -   [*DxgkDdiUnload*](https://msdn.microsoft.com/library/windows/hardware/ff560801)
    -   [*DxgkDdiUpdateActiveVidPnPresentPath*](https://msdn.microsoft.com/library/windows/hardware/ff560803)
    -   [*DxgkDdiUpdateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff560804)


3.  渡す*DriverObject*、 *RegistryPath*、および、塗りつぶされたで[**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169)構造体を[ **DxgkInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff560824)します。

4.  によって返される値を返す[ **DxgkInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff560824)します。

[**ドライバー\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff556169)構造が後にメモリ内に存在する必要はありません**DriverEntry**を返します。

**DriverEntry**ページング可能な行う必要があります。

カーネル モードの表示専用ドライバー (KMDOD) インターフェイス、 [KMDDOD_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_kmddod_initialization_data)構造体には、KMDOD によって実装できるすべての関数が一覧表示されます。 これらの関数のすべてを除く、 [DxgkDdiPresentDisplayOnly](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_presentdisplayonly)関数を完全な表示のミニポート ドライバーで実装することもできます。  カーネル モード表示専用ドライバー (KMDOD) の DriverEntry 関数では、ポートのディスプレイ ドライバーへの関数ポインターを提供 KMDDOD_INITIALIZATION_DATA 構造体のすべてのメンバーを入力し、その構造に渡すことによって、 [DxgkInitializeDisplayOnlyDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nf-dispmprt-dxgkinitializedisplayonlydriver)関数。

KMDOD が、垂直同期の制御機能をサポートしていない場合は特定の機能を実装しているいない必要がありますに注意してください: コントロールの垂直同期と保存のエネルギーを参照してください。

次の構造と列挙型はカーネル モードの表示専用ドライバーにも使用されます。

* [D3DKMT_MOVE_RECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmt_move_rect)
* [D3DKMT_PRESENT_DISPLAY_ONLY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_d3dkmt_present_display_only_flags)
* [DXGK_PRESENT_DISPLAY_ONLY_PROGRESS_ID](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_present_display_only_progress_id)
* [DXGKARG_PRESENT_DISPLAYONLY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_present_displayonly)
* [DXGKARGCB_PRESENT_DISPLAYONLY_PROGRESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_present_displayonly_progress)


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
<td align="left"><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="even">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DxgkInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff560824)

[*DxgkDdiUnload*](https://msdn.microsoft.com/library/windows/hardware/ff560801)

 

 






