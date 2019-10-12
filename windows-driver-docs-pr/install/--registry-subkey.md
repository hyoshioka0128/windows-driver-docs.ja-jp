---
title: '* レジストリ サブキー'
description: '* レジストリ サブキー'
ms.assetid: 19b72c64-5a64-4655-b922-4a4bca162b32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 992657e051c8896d383dc906b01f52d9d733f4f2
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038099"
---
# <a name="-registry-subkey"></a>\* レジストリサブキー


Windows 7 以降では、 **\*** (アスタリスク) のレジストリサブキーによって、 [HardwareID](hardwareid-registry-subkey.md)またはのいずれかで識別されるデバイス用に列挙されたすべてのデバイスノード (*devnodes*) に、リムーバブルデバイスの機能の上書きが適用されることが指定されています。[互換 id](compatibleid-registry-subkey.md)レジストリサブキー。 リムーバブルデバイスの機能の上書きの詳細については、「 [Deviceoverrides レジストリキー](deviceoverrides-registry-key.md)」を参照してください。

**\*** レジストリサブキーは、 **HardwareID**または**CompatibleID** [LocationPaths](locationpaths-registry-subkey.md) レジストリサブキーによって指定されたすべての devnodes に、locationpaths の規則に基づいてリムーバブルデバイスの機能オーバーライドを適用します。Override に指定された [ChildLocationPaths](childlocationpaths-registry-subkey.md) レジストリサブキー。 たとえば、 **\*** レジストリサブキーが**locationpaths**サブキー内に指定されている場合、親**HardwareID**または**によって識別されるデバイスのすべての親 devnodes に、リムーバブルデバイスの機能の上書きが適用されます。互換 Id**レジストリサブキー。

次の表は、 **\*** レジストリサブキーの形式と要件を定義しています。

| レジストリサブキー名 | 必須/省略可能 | 形式の要件 | 親サブキー                                                                                                      | 子サブキー |
|----------------------|-------------------|---------------------|--------------------------------------------------------------------------------------------------------------------|---------------|
| \*                   | 省略可能          | なし                | [Locationpaths](locationpaths-registry-subkey.md)または[childlocationpaths](childlocationpaths-registry-subkey.md) | なし          |

 

リムーバブルデバイスの機能の上書きのスコープを示すには、 [Locationpath](locationpath-registry-subkey.md)または **\*** レジストリサブキーが存在している必要があります。

@No__t 0 レジストリサブキーには、デバイスがリムーバブルかどうかを指定する**リムーバブル**DWORD 値を含める必要があります。 次の表では、有効な**リムーバブル**値を定義します。

| リムーバブル値 | 説明                                                 |
|-----------------|-------------------------------------------------------------|
| 0               | 適用可能な devnodes は、リムーバブルでないと見なされます。 |
| 1               | 適用可能な devnodes は、リムーバブルと見なす必要があります。     |
