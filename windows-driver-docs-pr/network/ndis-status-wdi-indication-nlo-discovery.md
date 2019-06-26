---
title: NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY を使用して、ネットワークの一覧のオフロード (NLO) の検出を示します。
ms.assetid: 1a789bd8-8601-45f3-a9bf-5220c20379cb
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_NLO_DISCOVERY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d96a1b4a5e730f63fa41e82b55fa27700fd70b9f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384915"
---
# <a name="ndisstatuswdiindicationnlodiscovery"></a>NDIS\_状態\_WDI\_INDICATION\_NLO\_検出


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_NLO\_をネットワークの一覧のオフロード (NLO) の検出を示すために検出します。

| オブジェクト |
|--------|
| ポート   |

 

ファームウェアでは、Ssid NLO でプッシュ ダウンの Ap を検出します。 NLO は、システムのスリープ状態から再開するときに、高速接続の AOAC 以外のシステムで使用されます。 ファームウェアにプッシュされる Ssid の Ap をスキャンする AOAC システムにも使用されます。

OS は定期的なバック グラウンドが CS にスキャンを要求しません。 NLO スキャンは、CS に推奨される方法なので、画面がオフ、ときにユーザーが表示されているすべてのアクセス ポイントを表示する必要はありませんが、ユーザーが Ssid の自動接続を自動プロファイルに接続します。 OS から負荷を軽減する Ssid の一覧が推奨される認証および暗号ペアと、最大 4 つのチャネルのヒント。 ファームウェアは一覧に 1 つ以上の SSID がある場合は、自律的に次の高速スキャンと低速スキャン フェーズのスケジュール、NLO スキャンを開始する必要があります。 クラスのドライバーでは、ファームウェアの要求に OS の要求を変換します。 NLO スキャンが推奨される認証をサポートする暗号ペア Ssid に関連付けられているアクセス ポイントのスケジュールに従って実行するには、ファームウェアが必要です。

各スキャンの期間中、チャネルの一覧に制約は必要ありませんが、チャネルのリストの条件に一致する Ssid のファームウェアをスキャンします。 検出された AP 情報を示す値をキャッシュする必要があります。

任意の一致が見つかったときに、ファームウェアは NLO 検出を示し、検出された AP 情報を取得するホストの一覧をキャッシュします。

NLO 検出の指標は、次の 2 つのケースで行われます。

-   NIC が Dx の場合です。
    1.  ウェイク割り込みをトリガーし、セットの電力 D0 を次の手順を続行するために待機します。
    2.  NLO 検出を指定します。
    3.  ファームウェアが NLO 検出の理由でスタックを再開したことを示します。
-   NIC が D0 の場合です。
    -   NLO 検出を指定します。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                      |
|--------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BSS\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry) | x                              |          | Bssid の一覧。 一覧には、この探索の状態を発生させたエントリが含まれる少なくとも必要があります。 |

 

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

 

 




