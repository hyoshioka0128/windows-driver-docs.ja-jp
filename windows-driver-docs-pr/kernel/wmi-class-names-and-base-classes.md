---
title: WMI クラス名と基本クラス
description: WMI クラス名と基本クラス
ms.assetid: 6c3f74a3-e596-4694-8619-db38d67e030c
keywords:
- WDK の WMI の基本クラス
- WDK の WMI の名前
- WDK の WMI クラス
- WMI の WDK カーネルでは、クラス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff351f5606a65786c69fb4b635229e30dd5c581
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380926"
---
# <a name="wmi-class-names-and-base-classes"></a>WMI クラス名と基本クラス





WMI クラス名は大文字、する必要があります先頭は英字、およびできません先頭や末尾をアンダー スコア。 残りのすべての文字は、アルファベット、数字、またはアンダー スコアである必要があります。

WMI クライアント アプリケーションでは、ドライバーの WMI クラス名にアクセスでき、それらをユーザーに表示することができます。 クラスのわかりやすい名前を使用するより直感的なクラスの作成に役立ちます。

WMI クラス名は、WMI 名前空間内で一意である必要があります。 その結果、ドライバーの WMI クラス名では、別のドライバーで定義されている複製できません。

名前の競合を防ぐため、ドライバー ライターはドライバー固有の基本クラスを定義し、すべてのドライバーの WMI クラスを基本クラスから派生できます。 まとめて基底クラスの名前とクラス名、一意の名前を生成する可能性が高くなりますが。 たとえば、次に示しますシリアル ドライバーのデータ ブロックの抽象基本クラス。

```cpp
// Serial driver's base class for data blocks
[abstract]
class MSSerial {
}
 
// Example class definition for a data block
[
    //Class qualifiers 
]
class MSSerial_StandardSerialInformation : MSSerial 
{
    //Data items
}
```

デバイスに固有のカスタム データ ブロックが基底クラス名では、製造元、モデル、およびドライバーまたはデバイスの種類を含める必要があります。 次に、例を示します。

```cpp
[abstract]
class Adaptec1542 {
}
 
class Adaptec1542_Bandwidth : Adaptec1542 {
    //Data items
}
 
class Adaptec1542_Speed : Adaptec1542 {
    //Data items
}
```

WMI は、特定のクラス階層内の 1 つだけの抽象基本クラスをできます。 イベント ブロックを定義するクラスがから派生する必要があります**WmiEvent**、抽象基本クラスであるため、**抽象**イベント ブロックのドライバーの定義の基本クラスで修飾子は使用できません。 代わりに、非抽象基本クラスから派生させる**WmiEvent**、基本クラスから個々 のイベント クラスを派生します。 次に、例を示します。

```cpp
//Serial driver's base class for event blocks
class MSSerialEvent : WmiEvent 
{
}
 
//Example class definition for an event block
[
    //Class qualifiers 
]
class MSSerial_SendEvent : MSSerialEvent 
{
    //Data items
}
```

MOF の形式で基底クラスを定義する詳細については、Microsoft Windows SDK を参照してください。

 

 




