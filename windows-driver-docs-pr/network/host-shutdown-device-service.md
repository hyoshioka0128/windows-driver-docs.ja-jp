---
title: ホストのシャット ダウン デバイス サービス
description: このトピックではモバイル ブロード バンド インターフェイス モデル (MBIM) ためのガイドラインを提供します-CID_MBIM_DEVICE_SERVICES によりクエリされるときにサービスの準拠デバイスを実装して、デバイスをレポートします。
ms.assetid: 62BFC796-EDB2-489E-B487-65E2DD7C4256
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 708a9460279773e71816242146b1f2c44a4564d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552633"
---
# <a name="host-shutdown-device-service"></a>ホストのシャット ダウン デバイス サービス


このトピックではモバイル ブロード バンド インターフェイス モデル (MBIM) ためのガイドラインを提供します-準拠デバイスを実装して、デバイスのレポート サービスの CID が照会すると\_MBIM\_デバイス\_サービス。

このトピックの情報には、Windows 8 以降が適用されます。

## <a name="microsoft-host-shutdown"></a>Microsoft のホストのシャット ダウン


MBIM 準拠のデバイスを実装し、CID が照会すると、次のデバイス サービス\_MBIM\_デバイス\_サービス。 10.1 でよく知られている既存のサービスが定義されている、 [USB NCM モバイル ブロード バンド インターフェイス モデル (MBIM) V1.0 仕様](https://go.microsoft.com/fwlink/p/?linkid=320791)します。 Microsoft は、これを次のサービスの定義を拡張します。

サービス名 = **Microsoft ホストのシャット ダウン**

UUID = **UUID\_MS\_HOSTSHUTDOWN**

UUID 値 = **883b7c26-985f-43fa-9804-27d7fb80959c**

## <a name="defined-cids-for-uuidmshostshutdown-device-service"></a>UUID の Cid が定義されている\_MS\_HOSTSHUTDOWN デバイス サービス


| CID                          | 最小 OS バージョン       |
|------------------------------|--------------------------|
| CID\_MBIM\_MSHOSTSHUTDOWN    | Windows 8                |
| CID\_MBIM\_MSHOSTPRESHUTDOWN | Windows 10 バージョン 1511 |

 

## <a name="cidmbimmshostshutdown"></a>CID\_MBIM\_MSHOSTSHUTDOWN


このコマンドは、ホストがシャット ダウンしているデバイスに伝えます。 MB デバイスの電源を失う可能性があります。

|                                      |                           |
|--------------------------------------|---------------------------|
| CID                                  | CID\_MBIM\_MSHOSTSHUTDOWN |
| コマンド コード                         | 1                         |
| 設定                                  | 〇                       |
| クエリ                                | X                        |
| イベント                                | X                        |
| InformationBuffer ペイロードを設定します。        | なし                       |
| クエリ InformationBuffer ペイロード      | なし                       |
| 完了 InformationBuffer ペイロード | なし                       |

 

|                   |                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------|
| 設定               | MBIM で InformationBuffer\_コマンド\_MSG は使用されません。 MBIM の InformationBuffer\_コマンド\_DONE 使用されません。 |
| クエリ             | サポートされません                                                                                          |
| 要請されていないイベント | サポートされません                                                                                          |

 

### <a name="remarks"></a>注釈

モバイル ブロード バンド クラス ドライバーでは、各ホストの状態遷移を S4 および S5 状態でこのデバイス サービスをサポートしているモバイル ブロード バンドのデバイスに、ホストのシャット ダウンの通知を送信します。

この通知は、モバイル ネットワークを開始できるように事前を示す値を使用してモバイル ブロード バンド デバイスの登録解除して、メッセージと SIM 電気の初期化を開始を提供します。

次の情報は、さまざまなシステムの切り替え効果およびデバイスの電源の状態遷移のデバイスに Cid/コマンドを送信するホストの一覧をまとめたものです。

-   MSHOSTSHUTDOWN CID は S4 および S5 に状態遷移はホスト上のデバイスに送信されます。
-   MBIM\_CMD\_ホスト D3 モードにデバイスを配置する場合、閉じるがデバイスに送信されます。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">S0</th>
<th align="left">S1/S2/S3</th>
<th align="left">S4</th>
<th align="left">S5</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D0</p></td>
<td align="left"><p>MBIM_CMD_OPEN</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>D1</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D2</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>MBIM_CMD_CLOSE</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
</tr>
</tbody>
</table>

 

## <a name="cidmbimmshostpreshutdown"></a>CID\_MBIM\_MSHOSTPRESHUTDOWN


このコマンドは、システムはプレシャット ダウン中であることとそのすべての操作を完了、ネットワークから登録解除および flashless モデムの場合、ホストに必要な情報を格納する必要があります、MBIM モデムを通知します。 ホスト S4 および S5 の状態を入力する準備が待機しているときのすべてのサービスを適切にシャット ダウン プレシャット ダウン通知が送信されます。

|                                      |                              |
|--------------------------------------|------------------------------|
| CID                                  | CID\_MBIM\_MSHOSTPRESHUTDOWN |
| コマンド コード                         | 2                            |
| 設定                                  | 〇                          |
| クエリ                                | X                           |
| 通知                         | X                           |
| InformationBuffer ペイロードを設定します。        | なし                          |
| クエリ InformationBuffer ペイロード      | なし                          |
| 完了 InformationBuffer ペイロード | なし                          |

 

パラメーター:

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">設定</th>
<th align="left">クエリ</th>
<th align="left">通知</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">コマンド</td>
<td align="left">CID_MBIM_SET_MSHOSTPRESHUTDOWN</td>
<td align="left">なし</td>
<td align="left">なし</td>
</tr>
<tr class="even">
<td align="left">応答</td>
<td align="left">空</td>
<td align="left">なし</td>
<td align="left">なし</td>
</tr>
</tbody>
</table>

 

設定操作の InformationBuffer と InformationBufferLength が空です。

状態コード:

| 状態コード                       | 説明                                                                         |
|-----------------------------------|-------------------------------------------------------------------------------------|
| MBIM\_状態\_成功             | モデムが完了したプレシャット ダウン操作。                                     |
| MBIM\_状態\_いいえ\_デバイス\_サポート | デバイスはプレシャット ダウンをサポートしていないと、事前シャット ダウン操作は必要ありません。 |

 

 

 





