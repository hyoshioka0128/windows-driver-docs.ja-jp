---
title: 1 つのみのターゲット オペレーティング システム用のサンプルの INF モデル セクション
description: 1 つのみのターゲット オペレーティング システム用のサンプルの INF モデル セクション
ms.assetid: 4cad05f6-ec88-4bc8-b69a-0d6b06dfeec0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1923a5f23f3e4176f8ad8585c9a2c112d01d508
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574978"
---
# <a name="sample-inf-models-sections-for-only-one-target-operating-system"></a>1 つのみのターゲット オペレーティング システム用のサンプルの INF モデル セクション


ことは装飾[ **INF*モデル*セクション**](inf-models-section.md)該当する対象のオペレーティング システムの範囲を制限します。

次の例は、 [ **INF 製造元セクション**](inf-manufacturer-section.md)と各種[ **INF*モデル*セクション**](inf-models-section.md)Windows Vista を実行していない x86 ベースのシステムで、デバイスのインストールから Windows が妨げるされます。

```cpp
[Manufacturer]
%Msft% = Msft, NTx86.6.0, NT.6.1

;For Windows Vista only

[Msft.NTx86.6.0]
%NetVMini.DeviceDesc%    = NetVMini.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%    = NetVMini.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

;For Windows 7 and later

[Msft.NT.6.1]
```

この例で、 [ **INF 製造元セクション**](inf-manufacturer-section.md)が次[ **INF*モデル*セクション**](inf-models-section.md):

-   完全な INF*モデル*デバイスの説明とハードウェア識別子 (Id) を含む x86 ベースのシステムで Windows Vista のセクション。 Windows は選択し、Windows Vista を実行している x86 ベースのシステムで、デバイスをインストールするときは、このセクションを使用します。

-   空の INF*モデル*Windows 7 と Windows の任意のハードウェア プラットフォームでの以降のバージョンについてのセクション。 Windows では、これらのプラットフォームでデバイスのインストールは、このセクションを選択します。 ただし、セクションが含まれないため、特定のデバイスの説明またはハードウェア Id は Windows にこの INF ファイルからのすべてのデバイスはインストールされません。

 

 





