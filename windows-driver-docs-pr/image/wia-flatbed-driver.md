---
title: WIA ベッド ドライバー
description: WIA ベッド ドライバー
ms.assetid: 83c35b1f-10e0-47e1-97cc-5a7a79fb8088
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d3ba2f9affb0c05218ce660243561248cae846d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538265"
---
# <a name="wia-flatbed-driver"></a>WIA ベッド ドライバー





WIA ベッドのシステムによって提供されるドライバーとベンダーから提供された microdriver WIA ミニドライバーを結合します。 WIA ベッド ドライバーでは、WIA サービスから要求を受信し、microdriver 関数を使用して、WIA microdriver に要求をルーティングします。 WIA ベッド ドライバーでは、WIA microdriver、WIA ベッド ドライバーへの応答を送信する要求を送信します。 WIA ベッド ドライバーは、WIA サービスにこれらの応答を送信します。

WIA ベッドのドライバーの機能の説明を次に示します。

### <a name="minimum-whql-wia-properties"></a>最小 WHQL WIA プロパティ

WIA ベッド ドライバーでは、使用可能なプロパティのサブセットのみを実装し、仕入先別の任意の拡張機能は許可されません。 WHQL 仕様で必要なプロパティのみを実装します。 詳細については、WHQL 要件仕様を参照してください。

### <a name="supported-data-types"></a>サポートされるデータ型

次のデータ型がサポートされています。

-   1 ビットの白黒

-   8 ビットのグレースケール

-   24 ビット カラー

Microdriver には、デバイスでサポートされていないデータ型を除外できます。

### <a name="file-formats"></a>ファイル形式

既定のファイル形式は、ビットマップ (BMP) です。 使用して、他の形式のサポートを追加することができます、 [WIA microdriver の省略可能なコマンド](https://msdn.microsoft.com/library/windows/hardware/ff546016)CMD\_SETFORMAT します。

### <a name="supported-transfer-types"></a>サポートされている転送の種類

ファイル転送とコールバック転送の両方の種類がサポートされています。

### <a name="resolution"></a>解決方法

既定では、次の解決方法がサポートされています。75、100、150、200、300 および 600 dpi。

解像度の範囲は、デバイスによって異なります、ため、セットアップ情報 (INF) ファイルに次のようなエントリを追加することで、考えられる解決策の一覧を指定できます。

```INF
[DeviceData]
Resolutions="75, 100, 300, 600, 1200"
```

**注**  各コンマの後にスペースを挿入することに注意してください。
使用することは、 **IWiaItem::DeviceDlg**メソッド (Microsoft Windows SDK のドキュメントで説明) を"custom"の解像度を選択すると、ユーザー入力を取得します。

 

### <a name="adf"></a>ADF

単純な自動ドキュメント フィーダー (ADF) のコントロールのみがサポートされています。

 

 




