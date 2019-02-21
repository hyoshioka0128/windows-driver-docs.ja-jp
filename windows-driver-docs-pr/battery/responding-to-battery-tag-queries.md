---
title: バッテリのタグのクエリに応答してください。
description: バッテリのタグのクエリに応答してください。
ms.assetid: ac22a1d3-413c-4991-ac9c-fbfb2c6f16c6
keywords:
- バッテリ タグ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 676e5b55603f5749d5ee3422a9e44f3dceca276a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532057"
---
# <a name="responding-to-battery-tag-queries"></a>バッテリのタグのクエリに応答してください。


## <span id="ddk_responding_to_battery_tag_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_TAG_QUERIES_DG"></span>


バッテリのタグは、初期化し、miniclass ドライバーによってインクリメント ULONG カウンターです。 バッテリのクラス ドライバー呼び出し[ *BatteryMiniQueryTag* ](https://msdn.microsoft.com/library/windows/hardware/ff536275)タグの現在の値を要求します。

この miniclass ドライバー ルーチンに次のように宣言されます。

```cpp
typedef
NTSTATUS
(*BCLASS_QUERY_TAG)(
    IN PVOID Context,
    OUT PULONG BatteryTag
    );
```

*コンテキスト*パラメーター miniclass ドライバーによって割り当てられ、バッテリのクラス ドライバーに渡されるコンテキスト領域へのポインターは、\_ミニポート\_でデバイスの初期化 (情報構造体[**BatteryClassInitializeDevice**](https://msdn.microsoft.com/library/windows/hardware/ff536266))。 *BatteryTag*値が作成され、miniclass ドライバーによって維持されます。

バッテリが挿入されるたびに、miniclass ドライバーかどうかに関係なく、タグの値を増やす必要がありますこれは、新しいバッテリまたは同じのバッテリが以前存在でします。

バッテリが存在しないか miniclass ドライバーが状態を返す場合は、miniclass ドライバーでは、バッテリが存在するかどうかを判断できない、\_ありません\_かかる\_デバイスとバッテリのタグの値を設定する\_タグ\_無効です。

クラス ドライバー タグを使用してバッテリ内部および miniclass ドライバーへの呼び出しで、バッテリの特定のインスタンスを識別します。 Miniclass ドライバーでは、現在のバッテリに対応していることを確認する標準のルーチンに渡されるバッテリ タグの値を確認する必要があります。 タグが正しくない場合、miniclass ドライバーが状態を返す必要があります\_いいえ\_かかる\_デバイス。

 

 




