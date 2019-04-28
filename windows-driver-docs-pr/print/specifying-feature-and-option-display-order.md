---
title: 機能とオプションの表示順序を指定する
description: 機能とオプションの表示順序を指定する
ms.assetid: 51e18121-540b-40f0-85f8-eb2755a583f7
keywords:
- Unidrv、機能およびオプションの表示順序
- WDK Unidrv の機能やオプションの表示順序
- プロパティ シート ページ WDK 印刷、機能およびオプションの表示順序
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2acd8b8c621ce6c9822388c988778ff9dd59c7e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372067"
---
# <a name="specifying-feature-and-option-display-order"></a>機能とオプションの表示順序を指定する





Unidrv 生成プロパティ シートのページの機能とオプションが表示される順序を制御する空白を含める\*機能と\*GPD ファイル内のエントリのオプションします。 フルの前に、ファイルの先頭に向かってこれらのエントリを配置する必要があります\*機能と\*オプション エントリ、およびその他の機能またはオプションの名前参照の前にします。 空のエントリが表示される順序は、プロパティ シートのページで、機能とオプションが表示される順序です。 (ただし、PaperSize 機能のオプションは常にアルファベット順に一覧表示をこの順序を変更することはできません。)

空のセットの例を次に\*機能と\*エントリのオプションします。

```cpp
*Feature: EconoMode
{
    *Option: Off{}
    *Option: On{}
}
*Feature: Orientation
{
    *Option: PORTRAIT{}
    *Option: LANDSCAPE_CC90{}
}
*Feature: PaperSize
{
}
*Feature: Resolution
{
    *Option: Option1{}
    *Option: Option2{}
    *Option: Option3{}
}
```

この例では、エコノミー モード、向き、用紙サイズ、および解決の機能を表示する順序を指定します。 さらに、エコノミー モード、向き、および解決のオプションの表示順序を指定します。 用紙サイズのオプションは、アルファベット順に表示されます。

GPD ファイルを空にするには含めない場合\*機能と\*オプションの表示順序を指定するエントリ、GPD パーサーの表示順序を決定します。 一般に、パーサーと、機能と GPD ファイルに表示される順序で表示されるオプション、中に、この順序は保証されません。 さらに、既定では、パーサーが必ず InputBin 機能は、最初に表示されます。

空を含む\*機能と\*表示を明示的に指定するオプションのエントリで注文、注文を作成するパーサーを許可するよりも推奨されています。

 

 




