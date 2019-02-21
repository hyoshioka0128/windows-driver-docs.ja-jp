---
title: デバイス コンテナーの競合を避ける
description: デバイス コンテナーの競合を避ける
ms.assetid: 1c752333-8776-4c5e-bc2f-47ffde60c931
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7de14da7c4ff993b4925377b9ea924b18047182
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538824"
---
# <a name="avoiding-device-container-conflicts"></a>デバイス コンテナーの競合を避ける


同じコンテナー ID を共有するコンピューターへの 2 つまたは複数のデバイス (Microsoft オペレーティング システム (OS) を使用して明示的に定義された**ContainerID**記述子または同じの USB シリアル番号) デバイス コンテナーになります競合しています。 オペレーティング システムでは、1 台のデバイスから発信されているデバイスの機能を解釈し、1 つのデバイスのコンテナーが作成されます。 Windows 内のデバイスで予期しない動作が生じます。

この問題を回避するように Microsoft OS **ContainerID**記述子の値との USB シリアル番号は 1 つの物理デバイスに固有です。 製品ライン内のデバイス間でこれらの値を共有しないでください。

USB デバイスが USB シリアル番号に基づくコンテナー ID を生成するオペレーティング システムに依存している場合に、次のように、コンテナー ID が生成されます。

1.  オペレーティング システムでは、USB デバイスのシリアル番号、ベンダーの ID、製品 ID、および文字列を生成するリビジョン番号を連結します。

2.  結果の文字列は、USB に固有の名前空間の下の UUID Version 5 (sha-1) ハッシュ アルゴリズムを使用して、GUID にハッシュされます。 生成されたコンテナー ID は、独立系ハードウェア ベンダー (IHV) は、各デバイスで一意のシリアル番号を提供する指定、一意になります。

 

 





