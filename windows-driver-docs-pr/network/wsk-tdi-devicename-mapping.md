---
title: WSK_TDI_DEVICENAME_MAPPING
description: WSK_TDI_DEVICENAME_MAPPING
ms.assetid: 7636fa80-3908-4808-8fb8-6227ec6e023b
ms.date: 07/18/2017
keywords:
- WSK_TDI_DEVICENAME_MAPPING ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 626198cc16d0a30a644485fcf8e486cc31e48c36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530385"
---
# <a name="wsktdidevicenamemapping"></a>WSK\_TDI\_DEVICENAME\_マッピング


WSK アプリケーションの使用、WSK\_TDI\_DEVICENAME\_アドレス ファミリの組み合わせにマップするクライアント コントロールの操作をマッピングするには、ソケットの種類、およびプロトコルのデバイス名を[TDI](https://msdn.microsoft.com/library/windows/hardware/ff565094)トランスポート。 TDI トランスポートのサポートが必要な場合にのみ、WSK アプリケーションはこのクライアントの管理操作を使用します。 WSK アプリケーションでは、ソケットを作成するとき、WSK サブシステムは、アドレス ファミリ、ソケットの種類、および WSK アプリケーションによって指定されたプロトコルの組み合わせに対するネイティブ サポートがない場合にのみマッピングの一覧を参照します。

WSK アプリケーション、WSK を使用している場合\_TDI\_DEVICENAME\_アドレス ファミリ、ソケットの種類、およびプロトコルの組み合わせを TDI トランスポートのデバイス名にマップするクライアント コントロールの操作のマッピングを行う必要がありますいずれかの作成前にソケット。

アドレス ファミリ、ソケットの種類、およびプロトコルの組み合わせを TDI トランスポートのデバイス名をマップする WSK アプリケーションが呼び出す、 [ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)関数は次のパラメーター。

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
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff571192" data-raw-source="[&lt;strong&gt;WSK_TDI_MAP_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571192)"> <strong>WSK_TDI_MAP_INFO</strong> </a>アドレス ファミリの組み合わせのマッピングの一覧を含む構造体のソケットの種類、およびプロトコルを<a href="https://msdn.microsoft.com/library/windows/hardware/ff565091" data-raw-source="[TDI](https://msdn.microsoft.com/library/windows/hardware/ff565091)">TDI</a>デバイス名。</p></td>
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

TDI トランスポートの使用に関する詳細については、[TDI トランスポートを使用して](https://msdn.microsoft.com/library/windows/hardware/ff571015)を参照してください。

*Irp*パラメーターである必要があります**NULL**このクライアントのコントロールの操作。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://msdn.microsoft.com/library/windows/hardware/ff571068)または[Winsock Kernel](https://msdn.microsoft.com/library/windows/hardware/ff571083)代わりにします。

 

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

 

 




