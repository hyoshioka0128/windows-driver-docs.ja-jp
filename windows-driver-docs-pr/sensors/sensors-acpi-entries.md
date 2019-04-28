---
title: センサーの ACPI エントリ
description: このトピックでは、高度な構成と Windows 10 でのセンサーに固有の電源管理 interface (ACPI) エントリについて説明します。
ms.assetid: DFDD5603-18F5-4F6C-8D09-D6905587F3CE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215ad91ae452a7ee55578701273a17eef2a4d500
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368770"
---
# <a name="sensors-acpi-entries"></a>センサーの ACPI エントリ


このトピックでは、高度な構成と Windows 10 Mobile のセンサーに固有の電源管理 interface (ACPI) エントリについて説明します。 これらのエントリでは、ACPI のソース言語 (ASL) ファイルに追加します。

## <a name="rotm"></a>ROTM


回転行列 (ROTM) は、(、OEM によって定義されている)、センサーの X、Y、Z 軸と、モバイル デバイスの X、Y、および Z 軸間のリレーションシップを説明するために使用する行列です。

各行は、それぞれの X、Y、Z 軸に適用される変換を表します。 各エントリは、-1 と 1、3 つの小数点以下桁数の最大値を持つ各数値の間の 10 進数です。

次の例では、**メソッド**マトリックスを示しますセンサー ハードウェアの X、Y、Z 軸に沿って、Y の X、およびモバイル デバイスの Z 軸それぞれします。

```cpp
Method(ROTM, 0x0, NotSerialized) {
                Name(RBUF, Package(){
                    "0 1 0",
                    "-1 0 0",
                    "0 0 -1"
                })
                Return (RBUF)
            }
```

## <a name="prim"></a>PRIM


次**メソッド**プライマリとして、センサーをマークします。

```cpp
Method(PRIM, 0x0, NotSerialized) {
                Name(RBUF, Buffer(){1})
                    Return (RBUF)
            }
```

>[!NOTE]
> モバイル デバイス (たとえば、複数計) で同じ種類の複数のセンサーがあるかどうかは、それらのいずれかを使用してプライマリとしてマークする必要があります、**プライマリ**キーワード。 センサーの GetDefault メソッドが呼び出されたときに、プライマリのセンサーは WinRT API によって使用されます。 プライマリのセンサーは、そのセンサーの種類に依存しているオペレーティング システムの機能によっても使用されます。








