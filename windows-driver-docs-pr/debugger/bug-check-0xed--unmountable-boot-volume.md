---
title: バグ チェック 0xED マウントできないブート ボリューム
description: マウントできないブート ボリュームのバグ チェックでは、0x000000ED の値を持ちます。 これは、I/O サブシステムが、ブート ボリュームをマウントしようとしています。 し、失敗したことを示します。
ms.assetid: 7c4ab301-f110-4fc8-9ff8-242e0d2155fd
keywords:
- バグ チェック 0xED マウントできないブート ボリューム
- UNMOUNTABLE_BOOT_VOLUME
ms.date: 06/26/2017
topic_type:
- apiref
api_name:
- UNMOUNTABLE_BOOT_VOLUME
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9475bc8977c055dd5b3ec4042f0c612ea56e3705
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518779"
---
# <a name="bug-check-0xed-unmountablebootvolume"></a>バグ チェック 0xED:ベーシック\_ブート\_ボリューム


UNMOUNTABLE\_ブート\_ボリュームのバグ チェックが 0x000000ED の値を持ちます。 これは、I/O サブシステムが、ブート ボリュームをマウントしようとしています。 し、失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="unmountablebootvolume-parameters"></a>ベーシック\_ブート\_ボリューム パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>ブート ボリュームのデバイス オブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ボリュームのマウントに失敗した理由を説明するファイル システムからのステータス コード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>解決方法
----------

このエラーをデバッグしている場合は、使用、! v 拡張機能を分析します。 この拡張機能では、エラーに関連するデータの特定のエラーが表示されます。

このバグ チェックは通常、ハード ドライブなど、OS ブート ストレージ デバイスの障害に関連します。 ファイル システムと、回復を検証しようとするには、ブート レコード、次のトラブルシューティング手順よいでしょう。  

1. Windows 10 でトラブルシューティングを使用して、> オプション > スタートアップ修復します。 USB ドライブまたは DVD を Windows 回復環境を実行するから起動可能なリカバリ メディアやブートを作成する必要があります。
2. Windows 回復環境でコマンド プロンプトから、CHKDSK/r を使用して、ファイル システムを修復しようとしてください。  
3. マスターおよびブート レコードを修正するのにには、bootrec コマンドを使用します。    

次の手順に失敗した場合は、ハード ドライブが失敗したことができます。 一部のハード ドライブ ベンダーは、ハードウェア障害を確認するために役立つ診断ツールを提供します。




 

 

 




