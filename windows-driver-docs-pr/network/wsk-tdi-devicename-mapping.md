---
title: WSK_TDI_DEVICENAME_MAPPING
description: WSK_TDI_DEVICENAME_MAPPING
ms.assetid: 7636fa80-3908-4808-8fb8-6227ec6e023b
ms.date: 07/18/2017
keywords:
- WSK_TDI_DEVICENAME_MAPPING ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 57851b9e6e76a0d889724b84e959c8fe03bbf8b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379712"
---
# <a name="wsktdidevicenamemapping"></a>WSK\_TDI\_DEVICENAME\_マッピング


WSK アプリケーションの使用、WSK\_TDI\_DEVICENAME\_アドレス ファミリの組み合わせにマップするクライアント コントロールの操作をマッピングするには、ソケットの種類、およびプロトコルのデバイス名を[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))トランスポート。 TDI トランスポートのサポートが必要な場合にのみ、WSK アプリケーションはこのクライアントの管理操作を使用します。 WSK アプリケーションでは、ソケットを作成するとき、WSK サブシステムは、アドレス ファミリ、ソケットの種類、および WSK アプリケーションによって指定されたプロトコルの組み合わせに対するネイティブ サポートがない場合にのみマッピングの一覧を参照します。

WSK アプリケーション、WSK を使用している場合\_TDI\_DEVICENAME\_アドレス ファミリ、ソケットの種類、およびプロトコルの組み合わせを TDI トランスポートのデバイス名にマップするクライアント コントロールの操作のマッピングを行う必要がありますいずれかの作成前にソケット。

アドレス ファミリ、ソケットの種類、およびプロトコルの組み合わせを TDI トランスポートのデバイス名をマップする WSK アプリケーションが呼び出す、 [ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_TDI_DEVICENAME_MAPPING</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_TDI_MAP_INFO)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ポインターを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_tdi_map_info" data-raw-source="[&lt;strong&gt;WSK_TDI_MAP_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_tdi_map_info)"> <strong>WSK_TDI_MAP_INFO</strong> </a>アドレス ファミリの組み合わせのマッピングの一覧を含む構造体のソケットの種類、およびプロトコルを<a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85)" data-raw-source="[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85))">TDI</a>デバイス名。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

TDI トランスポートの使用に関する詳細については、次を参照してください。 [TDI トランスポートを使用して](https://docs.microsoft.com/windows-hardware/drivers/network/using-tdi-transports)します。

*Irp*パラメーターである必要があります**NULL**このクライアントのコントロールの操作。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)または[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)代わりにします。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




