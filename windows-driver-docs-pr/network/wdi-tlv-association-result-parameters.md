---
title: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS は、アソシエーションの結果のパラメーターを含む TLV です。
ms.assetid: A6F29084-EF36-43C4-B646-E071E755E110
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESULT_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: aedcbf118aa03268071231892b590e06a96f20e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842884"
---
# <a name="wdi_tlv_association_result_parameters"></a>WDI\_TLV\_ASSOCIATION\_RESULT\_PARAMETERS


WDI\_TLV\_ASSOCIATION\_RESULT\_PARAMETERS は、アソシエーションの結果のパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x2D

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                        | 説明                                                                                                                                                                                                                                         |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                                      | [**WDI\_ASSOC\_status**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status)に定義されているアソシエーション試行の完了ステータスを指定します。                                                                                                                       |
| UINT32                                                      | このポートからの認証またはアソシエーション要求への応答としてピアによって送信された802.11 ステータスコード。                                                                                                                                     |
| UINT8                                                       | ポートが AP に802.11 アソシエーションまたは802.11 再関連付け要求を送信したかどうかを指定します。 再関連付け要求が使用された場合は、この値を1に設定する必要があります。                                                                              |
| [**WDI\_AUTH\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)     | アソシエーション中にポートがピアとネゴシエートした認証アルゴリズム。                                                                                                                                                             |
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | アソシエーション中にポートがピアとネゴシエートしたユニキャスト暗号アルゴリズム。                                                                                                                                                             |
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | アソシエーション中にポートがピアとネゴシエートしたマルチキャストデータ暗号アルゴリズム。                                                                                                                                                      |
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | アソシエーション中にポートがピアとネゴシエートしたマルチキャスト管理暗号アルゴリズム。                                                                                                                                                |
| UINT8                                                       | モバイルステーションや Ap など、BSS ネットワーク内の任意のステーションで、ISO レイヤー2ブリッジング用の配布システム (DS) サービスをサポートするピアにポートが関連付けられているかどうかを指定します。 この値がサポートされている場合は、この値を1に設定する必要があります。 |
| UINT8                                                       | アソシエーション操作中にポートがポート承認を実行したかどうかを指定します。                                                                                                                                                       |
| UINT8                                                       | 802.11 WMM QoS プロトコルがこの関連付けに対してネゴシエートされているかどうかを指定します。 ネゴシエートされている場合は、この値を1に設定する必要があります。                                                                                                        |
| [**WDI\_DS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ds_info)                   | ポートが以前の関連付けと同じ DS に接続されているかどうかを指定します。                                                                                                                                                                 |
| UINT32                                                      | (Re) の関連付けが802.11 の理由コード30で失敗した場合、この値は、ピアによって要求された association カムバック time の値を示します。                                                                                               |
| WDI\_バンド\_ID (UINT32)                                      | 関連付けが確立されているバンド ID。                                                                                                                                                                                                |
| UINT32                                                      | IHV 関連付けステータス。 関連付けが失敗した場合、これには IHV が定義したステータスコードを含めることができます。 これは、デバッグ目的でのみ使用されます。                                                                                                        |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




