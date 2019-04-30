---
title: 標準リソース マップの作成
description: 標準リソース マップの作成
ms.assetid: 97d95481-5290-41d3-a6e6-7cc142d4c2e8
keywords:
- 標準的なリソースは、WDK 多機能デバイスをマップします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0610e483cd324a8a16b76442e4213599489cc656
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323534"
---
# <a name="creating-standard-resource-maps"></a>標準リソース マップの作成





多機能デバイスの INF に含まれている場合、 [ **INF DDInstall.LogConfigOverride セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547339)、親リソースが暗黙的に番号が 00 ~ *nn*表示されます。INF ので*ログの構成] セクションで*セクション (を参照してください[ **INF LogConfig ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547448))。 たとえば、次の INF に多機能 PC カード*DDInstall*.**LogConfigOverride**セクション。

```cpp
[DDInstall.LogConfigOverride]
LogConfig = DDInstall.Override0
 
[DDInstall.Override0]    ;com2
IOConfig=2f8-2ff                      ; resource 00
IOConfig=20@100-FFFF%FFE0             ; resource 01
IRQConfig=3,4,5,7,9,10,11             ; resource 02
MemConfig=4000@0-FFFFFFFF%FFFFC000    ; resource 03
PcCardConfig=41:100000(W)             ; resource 04
```

この例ではデバイスには、04 から番号が 00 である 5 つのリソースがあります。 1 つ以上を使用する必要がある場合*DDInstall*.**LogConfigOverride**  セクションで、各セクションでは、同じ順序でリソースを一覧表示する必要があります。

1 つの子関数 (Child0000) は、上に示した最初と 3 番目のリソースを必要とする場合、この子リソース マップは次のようになります。00,02. もう 1 つの子関数 (Child00001) は、5 つすべてのリソースを必要とする場合、リソース マップがなります。00,01,02,03,04. この例では、リソース 00 (**IoConfig 2f8 2ff =**) 02 と (**IRQConfig = 3、4、5、7、9、10、11**) 共有されます。 これらのリソース マップは、INF でよう指定するとします。

```cpp
[DDInstall.RegHW]
    ; for each "child" function list hardware ID and resource map
HKR,Child0000,HardwareID,,child0000-hardware-ID
HKR,Child0000,ResourceMap,1,00,02                 ; map for Child0000
HKR,Child0001,HardwareID,,child0001-hardware-ID
HKR,Child0001,ResourceMap,1,00,01,02,03,04        ; map for Child0001
```

「1」の次の**ResourceMap**パラメーターは、レジストリ エントリが、レジストリを指定します\_BINARY データ型。 「1」に続く数字は、リソース マップ値です。

ある場合ありません*DDInstall*.**LogConfigOverride** INF でのセクションでは、親リソースは、リソース要件が基になるバスのドライバーによって構築されている順序で番号が。 PC カード、バス ドライバーは、この順序でリソースを報告します。IRQ、I/O ポート、メモリ アドレス。 複数の I/O、メモリの要件については、カード上の組と同じ順序で、番号が付けられます。 他バス ドライバーには、他の注文でリソースが一覧表示可能性があります。

 

 




