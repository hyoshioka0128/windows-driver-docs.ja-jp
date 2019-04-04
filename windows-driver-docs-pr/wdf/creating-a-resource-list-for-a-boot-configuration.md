---
title: ブート構成のリソースの一覧を作成します。
description: ブート構成のリソースの一覧を作成します。
ms.assetid: 8b78cbac-b547-45a1-a49c-f5543bf5ffed
keywords:
- ハードウェア リソース WDK KMDF、ブート構成リソースの一覧
- ブート構成のリソースには、WDK KMDF が一覧表示されます。
- ブート構成リソースの作成の WDK KMDF を一覧表示します。
- リソースには、WDK KMDF が一覧表示されます。
- リソースの作成の WDK KMDF を一覧表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08a519d3b3c0cfffc8b84694ab1e43228a4440e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538845"
---
# <a name="creating-a-resource-list-for-a-boot-configuration"></a>ブート構成のリソースの一覧を作成します。


ドライバーのフレームワーク バス ドライバーでは、デバイスを列挙する後[ *EvtDeviceResourcesQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540895)コールバック関数。 このコールバック関数を空のリソースの一覧を表すリソース リスト オブジェクトを識別するハンドルを受け取ります。 ドライバーは、次を情報をデバイスのブート構成が必要なハードウェア リソースの種類ごとに、一覧に追加するを実行しする必要があります。

1.  ドライバーによって提供される入力[ **CM\_部分\_リソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541977)構造体は、特定のリソースの有効な値を指定します。

2.  呼び出す[ **WdfCmResourceListAppendDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff545683)または[ **WdfCmResourceListInsertDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff545698) CMの内容を追加するには\_部分的な\_リソース\_リソース リストに記述子構造体。

ドライバーの後に*EvtDeviceResourcesQuery*コールバック関数が返す、フレームワーク、リソース リストを渡します PnP マネージャー。

デバイスのインストーラーは、追加のリソースの一覧を指定できます。 その他のリソースの一覧の詳細については、[ハードウェア リソース](https://msdn.microsoft.com/library/windows/hardware/ff547012)を参照してください。

 

 





