---
title: WDDM 1.2 以降でのプラグ アンド プレイ (PnP)
description: すべての Windows Display Driver Model (WDDM) 1.2 以降では、開始および停止要求に応答して、次の動作がサポートされている必要があります。
ms.assetid: A95DCFEA-BC1B-4A13-9850-13814725D53E
keywords:
- 表示ドライバーの WDK 表示でのプラグアンドプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80ea42a66045234737739b32eab3949b18f9dd32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829795"
---
# <a name="plug-and-play-pnp-in-wddm-12-and-later"></a>WDDM 1.2 以降でのプラグ アンド プレイ (PnP)


すべての Windows Display Driver Model (WDDM) 1.2 以降では、プラグアンドプレイ (PnP) インフラストラクチャによる開始および停止要求に応答して、次の動作がサポートされている必要があります。 動作は、ドライバーが成功または失敗のコードを返すかどうか、またはシステムハードウェアが基本入出力システム (BIOS) と Unified Extensible Firmware Interface (UEFI) のどちらに基づいているかによって異なります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 WDDM バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装-完全なグラフィックスと表示のみ</td>
<td align="left">Mandatory</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">必要条件</a>とテスト</td>
<td align="left"><p><strong>PnpStopStartSupport (WDDM12. 表示)</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddisplay_miniport_driver_pnp_ddispanspan-iddisplay_miniport_driver_pnp_ddispanspan-iddisplay_miniport_driver_pnp_ddispandisplay-miniport-driver-pnp-ddi"></a><span id="Display_miniport_driver_PnP_DDI"></span><span id="display_miniport_driver_pnp_ddi"></span><span id="DISPLAY_MINIPORT_DRIVER_PNP_DDI"></span>ミニポートドライバーの PnP DDI を表示する


Windows 8 以降、Microsoft DirectX graphics カーネルサブシステムは、ディスプレイデバイスが起動または休止状態から再開された場合にドライバーが呼び出すことができるこの機能を提供します。

-   [**DxgkCbAcquirePostDisplayOwnership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_acquire_post_display_ownership)

これらの関数と構造体は、WDDM 1.2 以降の PnP 要件を実装するために、ディスプレイミニポートドライバーで使用できます。

-   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)
-   [*DxgkDdiSystemDisplayEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_enable)
-   [*DxgkDdiSystemDisplayWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_system_display_write)
-   [**DXGK\_表示\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information)

## <a name="span-idpnp_start_operationspanspan-idpnp_start_operationspanspan-idpnp_start_operationspanpnp-start-operation"></a><span id="PnP_start_operation"></span><span id="pnp_start_operation"></span><span id="PNP_START_OPERATION"></span>PnP の開始操作


ディスプレイデバイスでのプラグアンドプレイ (PnP) 開始プロセスは、ブート中、またはディスプレイドライバー間でのアップグレード中に発生します。 この場合、ドライバーは、フレームバッファーに関する情報を取得し、表示の同期を維持するために、 [*DxgkCbAcquirePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_acquire_post_display_ownership)関数を呼び出す必要があります。 フレームバッファー情報は、ファームウェア、またはシステムに読み込まれた以前の WDDM 1.2 以降のドライバーから提供されます。

呼び出し時に、オペレーティングシステムは[*DxgkDdiSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)関数に対して D0 の電源状態に戻り、 [*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device) 1.2 関数に対して、ソースの可視性を false に設定する必要があります ([**dxgkarg\_SETVIDPNSOURCEVISIBILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourcevisibility)。すべてのアクティブな video present network (VidPN) ターゲットに対して**表示** = **FALSE**)。 この場合、ディスプレイパイプラインハードウェアはモニターとの同期信号を維持する必要がありますが、現在スキャンされているサーフェイスにどのピクセルデータが存在するかに関係なく、パイプラインは引き続き黒いピクセルデータをモニターに送信する必要があります。つまり、ピクセルパイプラインは、すべての黒いピクセルでモニターを消していることが保証されます。 その後、最初のフレームがフレームバッファーにレンダリングされると、オペレーティングシステムはソースの可視性を true に設定します。

これらのすべての手順でモニターの同期を維持し、ユーザーが画面上で点滅したりちらつきたりしないようにします。

これらは、PnP 開始プロセス後にドライバーが返すリターンコードです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーのリターンコード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success"></span><span id="success"></span><span id="SUCCESS"></span>ブランド</p></td>
<td align="left"><p>動作は、Windows 7 の場合と同じです。</p>
<p>BIOS ベースのシステムでは、ドライバーが正常に起動した場合でも、フレームバッファーはアクティブのままであり、ドライバーを有効なモードに設定する準備ができている必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>不具合</p></td>
<td align="left"><p>BIOS ベースのシステムの場合、ドライバーはシステムを BIOS と互換性のある状態のままにする必要があります。</p>
<p>UEFI ベースのシステムの場合、ドライバーは、基本ディスプレイドライバーがディスプレイを使用できるように、UEFI グラフィックス出力プロトコル (GOP) によって設定されたのと同じモードでディスプレイを残しておく必要があります。 ドライバーは、有効なエラーコードを返す必要があります。 ドライバーが、GOP を基本表示ドライバーで使用できる状態にすることができない場合、ドライバーは<strong>STATUS_GRAPHICS_STALE_MODESET</strong>エラーコードを Ntstatus から返す必要があり、オペレーティングシステムによってシステムのバグチェックが発生します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idpnp_stop_operationspanspan-idpnp_stop_operationspanspan-idpnp_stop_operationspanpnp-stop-operation"></a><span id="PnP_stop_operation"></span><span id="pnp_stop_operation"></span><span id="PNP_STOP_OPERATION"></span>PnP 停止操作


ディスプレイデバイスでのプラグアンドプレイ (PnP) 停止プロセスは、通常、ドライバーを新しいバージョンにアップグレードするときに発生します。 この場合、オペレーティングシステムはドライバーの[*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)関数を呼び出します。これにより、ドライバーは正確なフレームバッファー情報を提供する必要があります。

[*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)の呼び出しでは、ドライバーは、アクティブな VidPn ターゲットのソースの可視性が true であることを確認する必要があります ([**Dxgkarg\_SETVIDPNSOURCEVISIBILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourcevisibility)。**表示** = **TRUE**)。 さらに、WDDM 1.2 以降では、ドライバーはピクセルパイプラインがプログラミングされているサーフェイスが黒いピクセルで塗りつぶされるようにする必要があります。 ドライバーは、ソースの可視性が true に設定される前に、黒いピクセルでサーフェイスの塗りつぶしを完了する必要があります。

[*DxgkDdiStopDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)もドライバーに実装してください。 場合によっては、オペレーティングシステムが[*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)ではなく*DxgkDdiStopDevice*を呼び出すか、 *DxgkDdiStopDeviceAndReleasePostDisplayOwnership*の呼び出しが失敗することがあります。

これらは、PnP 停止プロセスの後にドライバーが返すリターンコードです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーのリターンコード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success__and_driver_returns_mode_information"></span><span id="success__and_driver_returns_mode_information"></span><span id="SUCCESS__AND_DRIVER_RETURNS_MODE_INFORMATION"></span>成功、ドライバーはモード情報を返します</p></td>
<td align="left"><p>ドライバーが停止する前に、現在の解像度を使用して、基本ディスプレイドライバーが使用できるフレームバッファーを設定する必要があります。また、オペレーティングシステムが DxgkDdiStopDeviceAndReleasePostDisplayOwnership を呼び出したときに、ドライバーはこの情報を返す必要があります。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)"></a>関数。 保存されているモード情報は BIOS と互換性がありません。また、基本表示ドライバーは、システムが再起動されるまで BIOS モードを提供しません。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)"><em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em></a>から<strong>STATUS_SUCCESS</strong>が返された場合、オペレーティングシステムは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)"><em>DxgkDdiStopDevice</em></a>を呼び出さないことを保証します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Success__and_driver_sets_the_Width_and_Height_members_of_the_DXGK_DISPLAY_INFORMATION_structure_to_zero"></span><span id="success__and_driver_sets_the_width_and_height_members_of_the_dxgk_display_information_structure_to_zero"></span><span id="SUCCESS__AND_DRIVER_SETS_THE_WIDTH_AND_HEIGHT_MEMBERS_OF_THE_DXGK_DISPLAY_INFORMATION_STRUCTURE_TO_ZERO"></span>Success、および driver は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information" data-raw-source="[&lt;strong&gt;DXGK_DISPLAY_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_display_information)"><strong>DXGK_DISPLAY_INFORMATION</strong></a>構造体の<strong>Width</strong>および<strong>Height</strong>メンバーをゼロに設定します。</p></td>
<td align="left"><p>このシナリオが可能なのは、システムに2つのグラフィックスカードがあり、モニターが現在の電源オンセルフテスト (POST) デバイスに接続されておらず、オペレーティングシステムが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device_and_release_post_display_ownership)"><em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em></a>関数を呼び出してPOST デバイス。</p>
<p>この場合、現在のディスプレイは2番目のグラフィックスアダプターで引き続き実行され、基本の表示ドライバーは POST デバイスをサポートするアダプターでヘッドレスモードで実行されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>不具合</p></td>
<td align="left"><p>オペレーティングシステムは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_stop_device)"><em>DxgkDdiStopDevice</em></a>関数を介して Windows 7 スタイルの PnP ストップドライバーインターフェイスを呼び出します。</p>
<p>BIOS ベースのシステムの場合、ドライバーはディスプレイを BIOS 互換モードに設定する必要があります。</p>
<p>UEFI ベースのシステムでは、基本ディスプレイドライバーは、グラフィックスアダプターでヘッドレスモードで実行されます。</p></td>
</tr>
</tbody>
</table>

 

PnP とその他の状態遷移の詳細については、「 [WDDM 1.2 以降でのシームレスな状態遷移の提供](seamless-state-transitions-in-wddm-1-2-and-later.md)」を参照してください。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、 **PnpStopStartSupport**の関連する[whck のドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





