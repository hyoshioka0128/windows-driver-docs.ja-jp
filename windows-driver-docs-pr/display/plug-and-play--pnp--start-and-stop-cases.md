---
title: WDDM 1.2 以降でのプラグ アンド プレイ (PnP)
description: すべての Windows 表示 Driver Model (WDDM) 1.2 およびそれ以降の表示のミニポート ドライバーは、開始および停止要求への応答で、次の動作をサポートする必要があります。
ms.assetid: A95DCFEA-BC1B-4A13-9850-13814725D53E
keywords:
- WDK の表示のディスプレイ ドライバーのプラグ アンド プレイします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f7ea04050b879a58e41dbb6a143e77dbd90756f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350117"
---
# <a name="plug-and-play-pnp-in-wddm-12-and-later"></a>WDDM 1.2 以降でのプラグ アンド プレイ (PnP)


すべての Windows 表示 Driver Model (WDDM) 1.2 以降ディスプレイ ミニポート ドライバーでは、開始およびプラグ アンド プレイ (PnP) インフラストラクチャによって要求を停止する応答で、次の動作をサポートする必要があります。 ドライバーは、成功または失敗コードを返すかどうか、またはシステムのハードウェアを基本入出力システム (BIOS) または Unified Extensible Firmware Interface (UEFI) に基づくかどうかによって動作が異なることができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">WDDM の最小バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装の完全なグラフィックスおよび表示のみ</td>
<td align="left">必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit" data-raw-source="[WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)">WHCK</a>要件とテスト</td>
<td align="left"><p><strong>Device.Graphics.WDDM12.Display.PnpStopStartSupport</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddisplayminiportdriverpnpddispanspan-iddisplayminiportdriverpnpddispanspan-iddisplayminiportdriverpnpddispandisplay-miniport-driver-pnp-ddi"></a><span id="Display_miniport_driver_PnP_DDI"></span><span id="display_miniport_driver_pnp_ddi"></span><span id="DISPLAY_MINIPORT_DRIVER_PNP_DDI"></span>ディスプレイのミニポート ドライバー PnP DDI


Windows 8 以降、Microsoft DirectX グラフィックスのカーネルのサブシステムには、ディスプレイ デバイスが開始または休止状態から再開された場合、ドライバーを呼び出すことができるこの機能が提供します。

-   [**DxgkCbAcquirePostDisplayOwnership**](https://msdn.microsoft.com/library/windows/hardware/hh451339)

これらの関数と構造体が表示のミニポート ドライバーおよび WDDM 1.2 と後での PnP 要件を実装するために使用できます。

-   [*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://msdn.microsoft.com/library/windows/hardware/hh451415)
-   [*DxgkDdiSystemDisplayEnable*](https://msdn.microsoft.com/library/windows/hardware/hh451426)
-   [*DxgkDdiSystemDisplayWrite*](https://msdn.microsoft.com/library/windows/hardware/hh451429)
-   [**DXGK\_表示\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh464017)

## <a name="span-idpnpstartoperationspanspan-idpnpstartoperationspanspan-idpnpstartoperationspanpnp-start-operation"></a><span id="PnP_start_operation"></span><span id="pnp_start_operation"></span><span id="PNP_START_OPERATION"></span>PnP 開始操作


ディスプレイ デバイスのプラグ アンド プレイ (PnP) の起動プロセスは起動中またはアップグレード中を別の 1 つのディスプレイ ドライバーから発生します。 この場合、ドライバーを呼び出す必要があります、 [ *DxgkCbAcquirePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451339)関数および表示の同期を維持するために、フレーム バッファーに関する情報を取得します。 フレーム バッファー情報は、ファームウェア、または以前の WDDM 1.2 およびシステムに読み込まれている以降のバージョンのドライバーから提供されます。

呼び出し中にオペレーティング システムは、 [ *DxgkDdiSetPowerState* ](https://msdn.microsoft.com/library/windows/hardware/ff560764) D0 電源の状態とを返す関数、 [ *DxgkDdiStartDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560775)関数、および WDDM 1.2 およびそれ以降のドライバーがソースの可視性を false に設定する必要があります ([**DXGKARG\_SETVIDPNSOURCEVISIBILITY**](https://msdn.microsoft.com/library/windows/hardware/ff559486).**表示される** = **FALSE**) すべてアクティブの存在するネットワーク (VidPN) のビデオ ターゲット。 ここでパイプラインされるディスプレイ ハードウェアが、モニターを使用して同期信号を維持する必要がありますが、黒のピクセル データをスキャンされている画面にどのようなピクセルのデータに関係なく、モニターを送信するパイプラインを続行する必要があります。これは、ピクセルのパイプラインがすべて黒ピクセルのモニターが非表示に保証されることを意味します。 後で、フレーム バッファーに最初のフレームがレンダリングされると、オペレーティング システムはソースの可視性を true に設定します。

すべての手順は、モニターの同期を維持し、こと、ユーザーに表示されない点滅やちらつき、画面を確認します。

これらは、リターン コードをドライバーは PnP 開始プロセスの後に返す必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーのリターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success"></span><span id="success"></span><span id="SUCCESS"></span>成功</p></td>
<td align="left"><p>動作は、Windows 7 と同様に同じです。</p>
<p>BIOS ベースのシステムでは、フレーム バッファーがアクティブのまま、ドライバーが正常に開始する場合と、ドライバーを有効なモードに設定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>エラー</p></td>
<td align="left"><p>BIOS ベースのシステムでは、ドライバーは、BIOS と互換性のある状態で、システムを残す必要があります。</p>
<p>UEFI ベースのシステムでは、ドライバーは、基本的なディスプレイ ドライバーが、表示に使用できるように、UEFI グラフィックス出力プロトコル (GOP) によって設定された同じモードで表示を残す必要があります。 ドライバーは、有効なエラー コードを返す必要があります。 かどうか、ドライバーは、基本的なディスプレイ ドライバーによって使用できる状態で GOP から出られません、ドライバーが返す必要があります、 <strong>STATUS_GRAPHICS_STALE_MODESET</strong> Ntstatus.h、およびオペレーティング システムからエラー コードにより、システムのバグチェックが発生するには.</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idpnpstopoperationspanspan-idpnpstopoperationspanspan-idpnpstopoperationspanpnp-stop-operation"></a><span id="PnP_stop_operation"></span><span id="pnp_stop_operation"></span><span id="PNP_STOP_OPERATION"></span>PnP 停止操作


ディスプレイ デバイスのプラグ アンド プレイ (PnP) 停止プロセスは、通常、ドライバーは、新しいバージョンにアップグレードされているときに発生します。 ここで、オペレーティング システムが、ドライバーを呼び出す[ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451415)正確なフレーム バッファー情報を提供するドライバーを必要とする関数。

[ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership* ](https://msdn.microsoft.com/library/windows/hardware/hh451415) active VidPn ターゲットのソースの可視性が true である呼び出し、ドライバーが確認する必要があります ([**DXGKARG\_SETVIDPNSOURCEVISIBILITY**](https://msdn.microsoft.com/library/windows/hardware/ff559486).**表示される** = **TRUE**)。 さらに、ドライバーが画面ピクセルのパイプラインがあるプログラムをスキャンすることを確認する必要がある WDDM 1.2 以降は黒ピクセルが格納されます。 ドライバーのソースの可視性を設定する前に黒のピクセルの表面の入力を完了する必要がありますを true にします。

実装も必ず[ *DxgkDdiStopDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff560781)ドライバー。 場合によっては、オペレーティング システムを呼び出すことができます*DxgkDdiStopDevice*の代わりに[ *DxgkDdiStopDeviceAndReleasePostDisplayOwnership*](https://msdn.microsoft.com/library/windows/hardware/hh451415)、または呼び出しの後に*DxgkDdiStopDeviceAndReleasePostDisplayOwnership*は失敗します。

これらは、リターン コードをドライバーは PnP 停止プロセスの後に返す必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーのリターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Success__and_driver_returns_mode_information"></span><span id="success__and_driver_returns_mode_information"></span><span id="SUCCESS__AND_DRIVER_RETURNS_MODE_INFORMATION"></span>成功した場合、およびドライバー モードの情報を返します</p></td>
<td align="left"><p>ドライバーを停止する前に、基本的なディスプレイ ドライバーが使用できる、現在の解像度を使用して、フレーム バッファーに設定する必要があり、オペレーティング システムを呼び出すと、ドライバーはこの情報を返す必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451415" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451415)"> <em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em> </a>関数。 保存モードの情報は、BIOS と互換性があるがないし、システムが再起動されるまで、基本的なディスプレイ ドライバーが BIOS モードを提供しません。</p>
<p>オペレーティング システムにより呼び出すことはありませんが、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560781" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560781)"> <em>DxgkDdiStopDevice</em> </a>場合<a href="https://msdn.microsoft.com/library/windows/hardware/hh451415" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451415)"> <em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em> </a>返します<strong>STATUS_SUCCESS</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Success__and_driver_sets_the_Width_and_Height_members_of_the_DXGK_DISPLAY_INFORMATION_structure_to_zero"></span><span id="success__and_driver_sets_the_width_and_height_members_of_the_dxgk_display_information_structure_to_zero"></span><span id="SUCCESS__AND_DRIVER_SETS_THE_WIDTH_AND_HEIGHT_MEMBERS_OF_THE_DXGK_DISPLAY_INFORMATION_STRUCTURE_TO_ZERO"></span>成功した場合、およびドライバーのセット、<strong>幅</strong>と<strong>高さ</strong>のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh464017" data-raw-source="[&lt;strong&gt;DXGK_DISPLAY_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh464017)"> <strong>DXGK_DISPLAY_INFORMATION</strong> </a>をゼロに構造体</p></td>
<td align="left"><p>このシナリオは、システムが 2 つのグラフィックス カード、モニターが、電源オン自己テスト (POST)、現在のデバイスに接続されていないおよびオペレーティング システムを呼び出す場合にのみ、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh451415" data-raw-source="[&lt;em&gt;DxgkDdiStopDeviceAndReleasePostDisplayOwnership&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451415)"> <em>DxgkDdiStopDeviceAndReleasePostDisplayOwnership</em> </a> POST デバイスを停止する関数。</p>
<p>2 番目のグラフィックス アダプターの実行は引き続きここで、現在の表示し、投稿デバイスをサポートするアダプターの基本的なディスプレイ ドライバーはヘッドレス モードで実行されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Failure"></span><span id="failure"></span><span id="FAILURE"></span>エラー</p></td>
<td align="left"><p>オペレーティング システムが Windows 7 スタイルの PnP 停止のドライバー インターフェイスを通じてを呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff560781" data-raw-source="[&lt;em&gt;DxgkDdiStopDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560781)"> <em>DxgkDdiStopDevice</em> </a>関数。</p>
<p>BIOS ベースのシステムでは、ドライバーは BIOS 互換モードに表示を設定する必要があります。</p>
<p>UEFI ベースのシステムの場合は、基本的なは、グラフィックス アダプターのヘッドレス モードでドライバーの実行を表示します。</p></td>
</tr>
</tbody>
</table>

 

PnP の要件についての詳細とその他の状態遷移は、[WDDM 1.2 以降のシームレスな状態遷移を提供する](seamless-state-transitions-in-wddm-1-2-and-later.md)を参照してください。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics.WDDM12.Display.PnpStopStartSupport**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





