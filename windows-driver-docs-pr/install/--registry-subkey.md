---
title: '* レジストリ サブキー'
description: '* レジストリ サブキー'
ms.assetid: 19b72c64-5a64-4655-b922-4a4bca162b32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f34b955081f2fd62faa72727f98bc5c74ca84755
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375768"
---
# <a name="-registry-subkey"></a>\* レジストリのサブキー


Windows 7 以降、 **\\*** (アスタリスク) レジストリ サブキーでは、リムーバブル デバイス機能のオーバーライドがデバイスのすべてのノードに適用されることを指定します (*devnode*) デバイスの列挙いずれかで識別される、 [HardwareID](hardwareid-registry-subkey.md)または[CompatibleID](compatibleid-registry-subkey.md)レジストリ サブキー。 リムーバブル デバイスの機能の詳細を上書きするを参照してください。 [DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)します。

**\\*** レジストリ サブキーで指定されたすべての devnode をリムーバブル デバイスの機能の上書きを適用する、 **HardwareID**または**CompatibleID**レジストリ サブキーがの規則に基づいた、 [LocationPaths](locationpaths-registry-subkey.md)または[ChildLocationPaths](childlocationpaths-registry-subkey.md)レジストリのサブキーのオーバーライドを指定します。 たとえば場合、 **\\*** 内のレジストリ サブキーが指定されて、 **LocationPaths**サブキー、識別されたデバイスのすべての親 devnode にリムーバブル デバイスの機能の上書きが適用されます親を**HardwareID**または**CompatibleID**レジストリ サブキー。

次の表形式およびの要件の定義、 **\\*** レジストリ サブキー。

| レジストリ サブキーの名前 | 必須/省略可能 | 形式の要件 | 親のサブキー                                                                                                      | 子のサブキー |
|----------------------|-------------------|---------------------|--------------------------------------------------------------------------------------------------------------------|---------------|
| \*                   | 省略可能          | なし                | [LocationPaths](locationpaths-registry-subkey.md)または[ChildLocationPaths](childlocationpaths-registry-subkey.md) | なし          |

 

いずれか、 [LocationPath](locationpath-registry-subkey.md)または**\\*** レジストリ サブキーをリムーバブル デバイスの機能のスコープのオーバーライドを示すために存在する必要があります。

\*レジストリ サブキーを含める必要があります、**リムーバブル**かどうか、デバイスがリムーバブルであるかどうかを指定する DWORD の値。 次の表は、有効な定義**リムーバブル**値。

| リムーバブル値 | 説明                                                 |
|-----------------|-------------------------------------------------------------|
| 0               | 該当する devnode 削除不可と見なされます |
| 1               | 該当する devnode をリムーバブルと見なす     |

 

 

 





