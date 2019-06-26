---
title: バッテリ タグ クエリへの応答
description: バッテリ タグ クエリへの応答
ms.assetid: ac22a1d3-413c-4991-ac9c-fbfb2c6f16c6
keywords:
- バッテリ タグ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a6d55947ad46b05c3780241a7a998ade62017b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364720"
---
# <a name="responding-to-battery-tag-queries"></a>バッテリ タグ クエリへの応答


## <span id="ddk_responding_to_battery_tag_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_TAG_QUERIES_DG"></span>


バッテリのタグは、初期化し、miniclass ドライバーによってインクリメント ULONG カウンターです。 バッテリのクラス ドライバー呼び出し[ *BatteryMiniQueryTag* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)タグの現在の値を要求します。

この miniclass ドライバー ルーチンに次のように宣言されます。

```cpp
typedef
NTSTATUS
(*BCLASS_QUERY_TAG)(
    IN PVOID Context,
    OUT PULONG BatteryTag
    );
```

*コンテキスト*パラメーター miniclass ドライバーによって割り当てられ、バッテリのクラス ドライバーに渡されるコンテキスト領域へのポインターは、\_ミニポート\_でデバイスの初期化 (情報構造体[**BatteryClassInitializeDevice**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice))。 *BatteryTag*値が作成され、miniclass ドライバーによって維持されます。

バッテリが挿入されるたびに、miniclass ドライバーかどうかに関係なく、タグの値を増やす必要がありますこれは、新しいバッテリまたは同じのバッテリが以前存在でします。

バッテリが存在しないか miniclass ドライバーが状態を返す場合は、miniclass ドライバーでは、バッテリが存在するかどうかを判断できない、\_ありません\_かかる\_デバイスとバッテリのタグの値を設定する\_タグ\_無効です。

クラス ドライバー タグを使用してバッテリ内部および miniclass ドライバーへの呼び出しで、バッテリの特定のインスタンスを識別します。 Miniclass ドライバーでは、現在のバッテリに対応していることを確認する標準のルーチンに渡されるバッテリ タグの値を確認する必要があります。 タグが正しくない場合、miniclass ドライバーが状態を返す必要があります\_いいえ\_かかる\_デバイス。

 

 




