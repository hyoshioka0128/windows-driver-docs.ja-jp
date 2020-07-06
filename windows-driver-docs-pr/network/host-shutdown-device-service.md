---
title: ホスト シャットダウン デバイス サービス
description: このトピックでは、CID_MBIM_DEVICE_SERVICES によって照会されたときに、説明されているデバイスサービスを実装してレポートするためのモバイルブロードバンドインターフェイスモデル (MBIM) 準拠デバイスのガイドラインを示します。
ms.assetid: 62BFC796-EDB2-489E-B487-65E2DD7C4256
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46de4fa87a5b0731f114e4ff80583e457db8b80e
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968252"
---
# <a name="host-shutdown-device-service"></a>ホスト シャットダウン デバイス サービス


このトピックでは、CID mbim デバイスサービスによって照会された場合に、説明されているデバイスサービスを実装してレポートするためのモバイルブロードバンドインターフェイスモデル (MBIM) 準拠デバイスに関するガイドラインを提供し \_ \_ \_ ます。

このトピックの情報は、Windows 8 以降に適用されます。

## <a name="microsoft-host-shutdown"></a>Microsoft ホストのシャットダウン


MBIM に準拠しているデバイスは、CID mbim デバイスサービスによって照会されたときに、次のデバイスサービスを実装して報告し \_ \_ \_ ます。 既知の既存のサービスは、 [USB NCM Mobile ブロードバンドインターフェイスモデル (MBIM) v1.0 仕様](https://go.microsoft.com/fwlink/p/?linkid=320791)のセクション10.1 で定義されています。 Microsoft はこれを拡張して次のサービスを定義します。

サービス名 = **Microsoft ホストのシャットダウン**

UUID = **UUID \_ MS \_ HOSTSHUTDOWN**

UUID 値 = **883b7c26-985f-43fa-9804-27d7fb80959c**

## <a name="defined-cids-for-uuid_ms_hostshutdown-device-service"></a>UUID \_ MS \_ hostshutdown デバイスサービス用に定義された cid


| CID                          | 最小 OS バージョン       |
|------------------------------|--------------------------|
| CID \_ MBIM \_ MSHOSTSHUTDOWN    | Windows 8                |
| CID \_ MBIM \_ MSHOSTPRESHUTDOWN | Windows 10 バージョン1511 |

 

## <a name="cid_mbim_mshostshutdown"></a>CID \_ MBIM \_ MSHOSTSHUTDOWN


このコマンドは、ホストがシャットダウンしていることをデバイスに通知します。 MB のデバイスで電力が失われる可能性があります。

**CID**: CID \_ MBIM \_ MSHOSTSHUTDOWN

**コマンドコード**: 1

**設定**: はい

**クエリ**: いいえ

**イベント**: いいえ

**InformationBuffer ペイロードの設定**: N/A

**クエリ情報バッファーペイロード**: N/A

**入力候補の情報バッファーのペイロード**: N/A


 

**設定**: mbim コマンドの informationbuffer が \_ 使用されて \_ いません。 MBIM コマンドの InformationBuffer が \_ \_ 使用されませんでした。

**クエリ**: サポートされていません

**一方的なイベント**: サポートされていません


 

### <a name="remarks"></a>注釈

モバイルブロードバンドクラスドライバーは、このデバイスサービスをサポートするモバイルブロードバンドデバイスにホストのシャットダウン通知を送信します。各ホストの状態は、S4 と S5 の状態に移行されます。

この通知は、モバイルブロードバンドデバイスに、モバイルネットワークの登録解除メッセージを開始して、SIM の電気的な初期化を開始できるようにするための早期通知を提供するためのものです。

次の情報は、さまざまなシステム遷移とデバイスの電源状態の移行のためにデバイスに Cid/数を送信したホストの一覧をまとめたものです。

-   MSHOSTSHUTDOWN CID は、S4 と S5 に移行するホスト状態のデバイスに送信されます。
-   MBIM \_ CMD \_ CLOSE は、ホストによってデバイスが D3 モードになったときにデバイスに送信されます。

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
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
</tr>
<tr class="even">
<td align="left"><p>D1</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D2</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>MBIM_CMD_CLOSE</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
</tr>
</tbody>
</table>

 

## <a name="cid_mbim_mshostpreshutdown"></a>CID \_ MBIM \_ MSHOSTPRESHUTDOWN


このコマンドは、システムが事前シャットダウンされていることを MBIM モデムに通知し、そのすべての操作を完了し、ネットワークから登録を解除して、必要な情報を flashless modem のケース用のホストに保存する必要があります。 プリシャットダウン通知は、ホストが S4 および S5 状態に移行する準備をしていて、すべてのサービスが適切にシャットダウンされるのを待機しているときに送信されます。

**CID**: CID \_ MBIM \_ MSHOSTPRESHUTDOWN

**コマンドコード**: 2

**設定**: はい

**クエリ**: いいえ

**通知**: いいえ

**InformationBuffer ペイロードの設定**: N/A

**クエリ情報バッファーペイロード**: N/A

**入力候補の情報バッファーのペイロード**: N/A


 

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
<th align="left">オン</th>
<th align="left">クエリ</th>
<th align="left">通知</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">コマンド</td>
<td align="left">CID_MBIM_SET_MSHOSTPRESHUTDOWN</td>
<td align="left">N/A</td>
<td align="left">N/A</td>
</tr>
<tr class="even">
<td align="left">[応答]</td>
<td align="left">空</td>
<td align="left">N/A</td>
<td align="left">N/A</td>
</tr>
</tbody>
</table>

 

設定操作では、InformationBuffer と InformationBufferLength が空です。

状態コード:

| 状態コード                       | 説明                                                                         |
|-----------------------------------|-------------------------------------------------------------------------------------|
| MBIM \_ ステータス \_ 成功             | モデムによって完了された事前シャットダウン操作。                                     |
| MBIM \_ ステータス \_ \_ デバイス \_ サポートなし | デバイスは、事前シャットダウンをサポートしていないため、事前シャットダウン操作は必要ありません。 |

 

 

 





