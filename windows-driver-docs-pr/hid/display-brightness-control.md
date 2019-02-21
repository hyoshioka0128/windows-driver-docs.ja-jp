---
title: ディスプレイの明るさコントロール
description: キーボード (外部またはラップトップで埋め込み)、hid のラップトップやタブレットの画面の明るさを制御するために使用できます。
ms.assetid: B22BA244-C5C6-4A50-AFE6-4E773194F18C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f4277b52857efe36a1c17c484521cc95be19d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528965"
---
# <a name="display-brightness-control"></a>ディスプレイの明るさコントロール


Windows 8 以降、標準化されたソリューションが追加されましたキーボード (外部またはラップトップで埋め込み)、hid のラップトップやタブレットの画面の明るさの制御を許可します。

このソリューションは、「HID 委員会の承認された最近[レビュー要求 41 の HID](http://www.usb.org/developers/hidpage#approved-usage-table-review-requests)します。

## <a name="architecture-and-overview"></a>アーキテクチャと概要


Windows 8 では、画面の明るさ拡大/縮小コンシューマー コントロールの最上位レベル コレクションの一部としてのサポートを提供します。 Windows 8 には、次の表に示す HID の使用がサポートされています。

| 使用状況 ID | 使用法の名前           | 使用法の種類               |
|----------|----------------------|--------------------------|
| 0x006F   | 明るさの増分値 | 再トリガー コントロール (RTC) |
| 0x0070   | 明るさデクリメント | 再トリガー コントロール (RTC) |

 

**注**  これら HID の使用は、モバイル システム (電源バッテリ使用時) でのみ動作し、Windows 8 が必要です。

 

## <a name="sample-report-descriptor"></a>サンプル レポート記述子


次のセクションで、サンプル レポート記述子の PC の製造元を活用する必要があります。 上位レベルのコレクションが別の上位レベルのコレクションに既にレポート記述子の一部である場合は、必要がありますレポート ID 含まれること (以下のサンプルでは表示されません) に注意してください。

``` syntax
Usage Page (Consumer)
Usage (Consumer Control)
Collection (Application)
   Logical Minimum (0x00)
   Logical Maximum (0x3FF)
   Usage Minimum (0x00)
   Usage Maximum (0x3FF)
   Report Size (16)
   Report Count (1)
   Input (Data, Array, Absolute)
End Collection
```

*重要な注意事項*

-   ユーザーは、キーを押すと、キーを識別するために、入力のレポートが生成されます。 キーが解放されるときに入力のレポートの使用法値を = 0 が発行されます。
-   1 つだけ使用状況は一度にアクティブおよび送信します。 コンシューマー コントロールには、さまざまなボタンが同時に押すことはできません。 新しい使用量が送信されるときに、前のキーの使用法が解放されると見なされます。
-   明るさアップ/スケール ダウンがキーを retriggering と繰り返しの速度は、Windows によって処理されます。 ハードウェアする必要がありますいないの送信を続ける、使用状況と、これらのキーはユーザーによって押されている保持されます。 ハードウェアには、入力のレポート ボタンが押されている場合、もうのみを送信するキーが離されたとき。

## <a name="troubleshooting-common-errors"></a>一般的なエラーのトラブルシューティング


ヒント: \#1。のみ明るさインクリメント/デクリメント HID の使用は、モバイル システム (電源バッテリ使用時) でのみ動作し、Windows 8 が必要です。

ヒント: \#2。システムが外部モニターに接続されている監視 (レガシ) トランスポートは HID メッセージに/からそれらをチャネルする機能をサポートしていないので、明るさインクリメント/デクリメントは機能しません。

 

 




