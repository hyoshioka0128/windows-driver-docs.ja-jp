---
title: OID_WDI_GET_BSS_ENTRY_LIST
description: OID_WDI_GET_BSS_ENTRY_LIST は、キャッシュされている BSS ネットワークの一覧を示すアダプターを要求するポートによって使用されます。
ms.assetid: 0eaa2b3a-6a1f-49e1-9556-81691892e666
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_BSS_ENTRY_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0d5b630e02fa85c5bc0769b64c15df2696844da9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353661"
---
# <a name="oidwdigetbssentrylist"></a>OID\_WDI\_取得\_BSS\_エントリ\_一覧


OID\_WDI\_取得\_BSS\_エントリ\_ポートによって一覧を使用して、キャッシュされている BSS ネットワークの一覧を示すアダプターを確認します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | Set はサポートされません。        | 1                               |

 

これは、BSS リストのキャッシュ処理を行うアダプターに対してのみ使用します。 クライアントとして動作しているときに、ポートは、アクセス ポイントの BSS エントリをレポートする必要があります。 さらに、ポートは、バック グラウンドのスキャンを実行して、そのスキャンで検出された BSS エントリを報告する必要があります。

アダプターで、この要求が受信したときに送信する必要があります[NDIS\_状態\_WDI\_INDICATION\_BSS\_エントリ\_一覧](ndis-status-wdi-indication-bss-entry-list.md)に問題、Microsoft コンポーネントです。 これらの問題は、Get のパラメーターと一致する BSS エントリを含める必要があります。 アダプターが 1 つまたは複数の NDIS を送信できる\_状態\_WDI\_INDICATION\_BSS\_エントリ\_プロパティが完了する前に、一覧の指示を完了する必要があります。

Microsoft コンポーネントは、オペレーティング システムに BSS の一覧を報告するのに指定されたエントリの一覧を使用します。 ローミングのパラメーターを設定し、タスクの接続にも使用されます。

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


| TLV                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                           |
|---------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI\_TLV\_SSID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ssid) |                                |          | ホストが、BSS 必要があること、SSID には、更新プログラムが一覧表示します。 |

 

## <a name="get-property-results"></a>プロパティの結果を得る


追加データがありません。 ヘッダー内のデータで十分です。
## <a name="unsolicited-indication"></a>要請されていないを示す値


[NDIS\_STATUS\_WDI\_INDICATION\_BSS\_ENTRY\_LIST](ndis-status-wdi-indication-bss-entry-list.md)

<a name="requirements"></a>必要条件
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




