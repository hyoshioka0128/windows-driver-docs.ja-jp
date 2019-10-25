---
title: ファイル システム オブジェクトのクエリと設定ルーチン
description: ファイル システム オブジェクトのクエリと設定ルーチン
ms.assetid: 34b97a6e-a155-443c-94dd-4d8f1fc4b430
keywords:
- ミニリダイレクター WDK、クエリ操作
- ミニリダイレクター WDK、set 操作
- クエリ操作 WDK ネットワークリダイレクター
- 設定操作 WDK ネットワークリダイレクター
- ファイルオブジェクト WDK ミニリダイレクター
- オブジェクト WDK ミニリダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f23d20d472be023b566f5ba8d81ac6532fddb1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841405"
---
# <a name="file-system-object-query-and-set-routines"></a>ファイル システム オブジェクトのクエリと設定ルーチン


ネットワークミニリダイレクターによって実装できるルーチンの多くは、ファイルシステムオブジェクトに対するクエリ操作と設定操作です。 RDBSS は、IRP を受信してファイルオブジェクトの情報を照会または設定することに応答して、ほとんどの呼び出しを発行します。 そのため、RDBSS が受信する IRP と、RDBSS が呼び出す MRx クエリまたは set 操作との間に直接対応しています。

次の表に、ファイルシステムオブジェクトのクエリおよび設定操作を行うためにネットワークミニリダイレクターで実装できるルーチンを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、パスが有効なディレクトリであるかどうかをネットワークミニリダイレクターが示すことを要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerydirectory" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerydirectory)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルディレクトリシステムオブジェクトの情報を照会するように要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryeainfo" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryeainfo)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトの拡張属性情報を照会するように要求します。 RDBSS は、IRP_MJ_QUERY_EA の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトのファイル情報を照会するように要求します。 RDBSS は、IRP_MJ_QUERY_INFORMATION の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryquotainfo" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryquotainfo)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトのクォータ情報を照会するように要求します。 RDBSS は、IRP_MJ_QUERY_QUOTA の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerysdinfo" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerysdinfo)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトのセキュリティ記述子情報を照会するように要求します。 RDBSS は、IRP_MJ_QUERY_SECURITY の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryvolumeinfo" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryvolumeinfo)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがボリューム情報を照会するように要求します。 RDBSS は、IRP_MJ_QUERY_VOLUME_INFORMATION の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxseteainfo" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxseteainfo)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトに拡張属性情報を設定するように要求します。 RDBSS は、IRP_MJ_SET_EA の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfo" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfo)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトのファイル情報を設定するように要求します。 RDBSS は、IRP_MJ_SET_INFORMATION の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、クリーンアップ時にファイルシステムオブジェクトのファイル情報を設定するようにネットワークミニリダイレクターに要求します。 RDBSS は、アプリケーションがハンドルを閉じてから閉じる前に、この呼び出しをクリーンアップ中に発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetquotainfo" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetquotainfo)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトのクォータ情報を設定するように要求します。 RDBSS は、IRP_MJ_SET_QUOTA の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetsdinfo" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetsdinfo)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトのセキュリティ記述子情報を設定するように要求します。 RDBSS は、IRP_MJ_SET_SECURITY の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetvolumeinfo" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetvolumeinfo)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがボリューム情報を設定するように要求します。 RDBSS は、IRP_MJ_SET_VOLUME_INFORMATION の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
</tbody>
</table>

 

 

 




