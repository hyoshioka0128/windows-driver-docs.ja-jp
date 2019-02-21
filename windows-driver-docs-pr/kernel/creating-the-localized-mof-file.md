---
title: ローカライズされた MOF ファイルを作成します。
description: ローカライズされた MOF ファイルを作成します。
ms.assetid: 1cc99e43-b09a-445d-abb6-4a3d73b6d7ed
keywords:
- MOF ファイルの WDK WMI
- MOF ファイルをローカライズします。
- プロパティ修飾子 WDK WMI
- 修正済みクラス WDK WMI
- 複数の MOF ファイルの WDK WMI
- WDK の WMI の言語
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9585b6a44f07154a7a09ed41c19c3a0ba713a43a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549717"
---
# <a name="creating-the-localized-mof-file"></a>ローカライズされた MOF ファイルを作成します。





Windows XP およびそれ以降のバージョンのオペレーティング システム、ドライバーはことで WMI スキーマをローカライズする*修正*各クラスのバージョン。 クラスの修正版では、ロケールに依存するプロパティ修飾子を更新します。

クラスの修正版が続く、クラスの宣言と同じ形式、**契約**修飾子。 修正済みのクラス宣言にも含まれています、<strong>ロケール (</strong>0 x<em>XXX</em>**)** 修飾子、場所*XXX*ロケール識別子 (LCID) を指定しますロケール。

修正済みの宣言には、変更されたプロパティの宣言が含まれています。 各ローカライズされたプロパティの修飾子が、 **: 修正**修飾子がアタッチされています。 たとえば、ローカライズされたバージョンの**説明 ("**<em>説明文字列</em>**")** なります**説明 ("** <em>ローカライズされた説明文字列</em>**"): 修正**します。

米国英語の修正契約書でその後に、基本クラスの宣言の例を示します。

```cpp
[guid(xxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx)]
class MyClass
{
    [key] sint32 KeyProp;
    string Name;
    uint64 Timestamp;
}

[amendment, locale(0x409)
 Description("Localized version of MyClass for American English"):amended]

class MyClass
{
    [DisplayName("Key Property"):amended,
     Description("The description of KeyProp"):amended]
    sint32 KeyProp;

    [DisplayName("User Name"):amended,
     Description("The description of Name"):amended]
    string Name;
}
```

変更されたプロパティのみを修正したクラスに含まれる必要があります。 クラスおよびプロパティの名前をローカライズすることはできません。 プロパティ修飾子のみをローカライズすることができます。

ローカライズされたクラスは、元のクラスを含む名前空間の子名前空間で構成されます。 特定のロケールのクラスは、MS\_*XXX*子名前空間、 *XXX*そのロケールの LCID で 16 進数を表します。 たとえば、ドライバーはでは、\\ルート\\既定では wmi 名前空間。 英語 (米国) 用にローカライズされて、修正したクラスがある、\\ルート\\wmi\\MS\_409 名前空間。

WMI のローカリゼーションの概要の詳細については、次を参照してください。、 [WMI のインターナショナル サポート](https://go.microsoft.com/fwlink/p/?linkid=8774)web サイト。

 

 




