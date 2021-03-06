---
title: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS は、関連付けの結果のパラメーターを含む TLV です。
ms.assetid: A6F29084-EF36-43C4-B646-E071E755E110
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESULT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 923874a59e22656858ea1cfa202c84395e494bb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357333"
---
# <a name="wditlvassociationresultparameters"></a>WDI\_TLV\_アソシエーション\_結果\_パラメーター


WDI\_TLV\_アソシエーション\_結果\_パラメーターは、関連付けの結果のパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x2D

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                        | 説明                                                                                                                                                                                                                                         |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                                      | 定義されている、関連付けの試行の完了ステータスを指定します[ **WDI\_ASSOC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status)します。                                                                                                                       |
| UINT32                                                      | このポートからの認証またはアソシエーション要求への応答でピアによって送信された 802.11 ステータス コード。                                                                                                                                     |
| UINT8                                                       | ポートが、ap、802.11 アソシエーションまたは 802.11 の再関連付けの要求を送信するかどうかを指定します。 再関連付け要求を使用した場合、この値を 1 に設定する必要があります。                                                                              |
| [**WDI\_AUTH\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)     | ポートが関連付けの際にピアとのネゴシエート認証アルゴリズム。                                                                                                                                                             |
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | ポートが関連付けの際にピアとのネゴシエート ユニキャスト暗号アルゴリズム。                                                                                                                                                             |
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | ポートが関連付けの際にピアとのネゴシエート マルチキャスト データの暗号アルゴリズム。                                                                                                                                                      |
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | ポートが関連付けの際にピアとのネゴシエート マルチキャスト管理暗号アルゴリズム。                                                                                                                                                |
| UINT8                                                       | かどうか、ポートに関連付けられている配布システムをサポートしているモバイル ステーションと Ap を含め、BSS ネットワークですべてのステーションで ISO のレイヤー 2 をブリッジするため (DS) のサービスを指定します。 これはサポートされている場合、この値を 1 に設定する必要があります。 |
| UINT8                                                       | ポートが関連付け操作中にポートの承認を実行するかどうかを指定します。                                                                                                                                                       |
| UINT8                                                       | このアソシエーションの 802.11 WMM QoS プロトコルがネゴシエートされているかどうかを指定します。 ネゴシエートされた場合、この値を 1 に設定する必要があります。                                                                                                        |
| [**WDI\_DS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ds_info)                   | ポートがその前のアソシエーションとして同じ DS に接続されているかどうかを指定します。                                                                                                                                                                 |
| UINT32                                                      | (Re) との関連付けが 30 の 802.11 理由コードで失敗した場合、この値は、ピアから要求されたアソシエーション復活時間の値を示します。                                                                                               |
| WDI\_バンド\_ID (UINT32)                                      | 関連付けが確立されているバンドの ID。                                                                                                                                                                                                |
| UINT32                                                      | IHV アソシエーションの状態。 関連付けに失敗した場合、IHV で定義されたステータス コードを含めることができますこのします。 これは、デバッグのためにのみ使用します。                                                                                                        |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




