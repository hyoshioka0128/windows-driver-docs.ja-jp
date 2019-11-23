---
title: WSK_TDI_DEVICENAME_MAPPING
description: WSK_TDI_DEVICENAME_MAPPING
ms.assetid: 7636fa80-3908-4808-8fb8-6227ec6e023b
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの WSK_TDI_DEVICENAME_MAPPING
ms.localizationpriority: medium
ms.openlocfilehash: 60fc5c3785c25c0e58b60f504bde2680c0489525
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844419"
---
# <a name="wsk_tdi_devicename_mapping"></a>WSK\_TDI\_DEVICENAME\_のマッピング


WSK アプリケーションは、WSK\_TDI\_DEVICENAME\_マッピングクライアントコントロール操作を使用して、アドレスファミリ、ソケットの種類、およびプロトコルの組み合わせを[tdi](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))トランスポートのデバイス名にマップします。 WSK アプリケーションでは、TDI トランスポートのサポートが必要な場合にのみ、このクライアントコントロール操作を使用します。 WSK アプリケーションでソケットを作成する場合、wsk サブシステムは、WSK アプリケーションで指定されたアドレスファミリ、ソケットの種類、およびプロトコルの組み合わせに対するネイティブサポートがない場合にのみ、マッピングの一覧を参照します。

WSK アプリケーションで WSK\_TDI\_DEVICENAME\_を使用している場合は、クライアントコントロール操作をマップして、アドレスファミリ、ソケットの種類、およびプロトコルの組み合わせを TDI トランスポートのデバイス名にマップします。これは、ソケットを作成する前に行う必要があります。

アドレスファミリ、ソケットの種類、およびプロトコルの組み合わせを TDI トランスポートのデバイス名にマップするために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出します。

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
<td><p>sizeof (WSK_TDI_MAP_INFO)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>アドレスファミリ、ソケットの種類、およびプロトコルと<a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85)" data-raw-source="[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565091(v=vs.85))">TDI</a>デバイス名の組み合わせのマッピングの一覧を含む<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_tdi_map_info" data-raw-source="[&lt;strong&gt;WSK_TDI_MAP_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_tdi_map_info)"><strong>WSK_TDI_MAP_INFO</strong></a>構造体へのポインター。</p></td>
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

TDI トランスポートの使用方法の詳細については、「 [Tdi トランスポートの使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-tdi-transports)」を参照してください。

このクライアントコントロール操作では、 *Irp*パラメーターは**NULL**である必要があります。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

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
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




