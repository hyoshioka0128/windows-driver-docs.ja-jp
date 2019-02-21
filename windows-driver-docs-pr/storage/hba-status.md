---
title: HBA\_状態
description: HBA\_状態
ms.assetid: 2fabfa86-7f8a-4c90-8aa0-53e42bd5c075
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 47421b11a79fdd3433cca28230e55831b7911376
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529216"
---
# <a name="hbastatus"></a>HBA\_状態


## <span id="ddk_hba_status_kr"></span><span id="DDK_HBA_STATUS_KR"></span>


HBA\_状態 WMI クラスの修飾子を WMI プロバイダー HBA に作成した WMI 要求の結果を示します。

次の表は、修飾子の名前と各名前の意味を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">修飾子</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_STATUS_OK</p></td>
<td align="left"><p>HBA で検出されたエラーはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR</p></td>
<td align="left"><p>HBA で検出されたエラーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_NOT_SUPPORTED</p></td>
<td align="left"><p>関数がサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INVALID_HANDLE</p></td>
<td align="left"><p>ハンドルが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_ARG</p></td>
<td align="left"><p>引数が正しくありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_ILLEGAL_WWN</p></td>
<td align="left"><p>世界中の名前が認識されません。 世界中の名前をに関する情報は、T11 委員会を参照してください。&#39;s<em>ファイバー チャネル HBA API</em>仕様。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_ILLEGAL_INDEX</p></td>
<td align="left"><p>インデックスは認識されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_MORE_DATA</p></td>
<td align="left"><p>大きなバッファーが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_STALE_DATA</p></td>
<td align="left"><p>情報は、前回の更新操作から変更されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_SCSI_CHECK_CONDITION</p></td>
<td align="left"><p>SCSI 条件の確認が報告されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_BUSY</p></td>
<td align="left"><p>ビジー状態または予約済みのアダプター、再試行が必要あります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TRY_AGAIN</p></td>
<td align="left"><p>要求がタイムアウト、再試行が必要になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_UNAVAILABLE</p></td>
<td align="left"><p>参照先の HBA が削除または非アクティブ化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_ELS_REJECT</p></td>
<td align="left"><p>要求された ELS は、ローカル アダプターによって拒否されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_INVALID_LUN</p></td>
<td align="left"><p>指定された LUN は、指定されたアダプターによって指定されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INCOMPATIBLE</p></td>
<td align="left"><p>非互換性が検出されました。 ライブラリとドライバーのモジュールは、HBA API 仕様の異なるバージョンを実装がある場合があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_AMBIGUOUS_WWN</p></td>
<td align="left"><p>複数のアダプターでは、一致するワールドワイド名 (WWN) があります。 これは、複数のアダプターの NodeWWN が同じ場合に発生する可能性があります。 一般に名前を世界中でに関する情報と NodeWWN 具体的には、T11 委員会を参照してください&#39;s<em>ファイバー チャネル HBA API</em>仕様。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_BUS</p></td>
<td align="left"><p>永続的なバインド要求には、無効なローカル SCSI バス番号が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_TARGET</p></td>
<td align="left"><p>永続的なバインド要求には、無効なローカルの SCSI ターゲット数が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_LUN</p></td>
<td align="left"><p>永続的なバインド要求には、無効なローカル SCSI LUN が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_LOCAL_SCSIID_BOUND</p></td>
<td align="left"><p>永続的なバインドのセットの要求には、既にバインドされていたローカルの SCSI ID が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_FCID</p></td>
<td align="left"><p>永続的なバインド要求には、無効な FCP ターゲット FCID が含まれています。 FCP ターゲット FCID の定義、T11 委員会を参照してください。&#39;s<em>ファイバー チャネル HBA API</em>仕様。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_NODE_WWN</p></td>
<td align="left"><p>永続的なバインド要求には、不適切な WWN FCP ターゲット ノードが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_PORT_WWN</p></td>
<td align="left"><p>永続的なバインド要求には、不適切な WWN FCP ターゲット ポートが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_LUN</p></td>
<td align="left"><p>永続的なバインド要求には、ターゲットが認識しない FCP LUN が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_LUID</p></td>
<td align="left"><p>永続的なバインド要求には、論理ユニットが定義されていないか、それ以外の場合にアクセスできない一意の識別子が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_NO_SUCH_BINDING</p></td>
<td align="left"><p>永続的なバインドの削除要求には、指定したポートを確立するバインディングとは一致しませんでしたが、バインドが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_NOT_A_TARGET</p></td>
<td align="left"><p>SCSI コマンドは、Nx_Port が SCSI ターゲット ポートに送信されました。 Nx_Port の定義、T11 委員会を参照してください。&#39;s<em>ファイバー チャネル HBA API</em>仕様。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_UNSUPPORTED_FC4</p></td>
<td align="left"><p>要求は、サポートされていない、FC 4 プロトコルに関するしました。 FC 4 プロトコルの詳細については、T11 委員会を参照してください。&#39;s<em>ファイバー チャネル HBA API</em>仕様。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_STATUS_ERROR_INCAPABLE</p></td>
<td align="left"><p>ポートに対して実装されていない機能を有効にするように要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_STATUS_ERROR_TARGET_BUSY</p></td>
<td align="left"><p>要求された SCSI コマンドを実行すると、オーバー ラップした SCSI コマンドの条件が生じる場合があります。</p></td>
</tr>
</tbody>
</table>

 

含めることによって*Hbaapi.h*ソフトウェアは、一連の前の表に、型名に対応するシンボリック定数へのアクセスになります。 シンボリック定数の定義が含まれていない*Hbapiwmi.h* (WMI ツールのスイートを生成、コンパイル時にファイル)。

 

 





