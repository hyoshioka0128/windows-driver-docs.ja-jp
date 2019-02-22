---
title: 存在のデバイスの親を判断します。
description: 存在のデバイスの親を判断します。
ms.assetid: 2d5948db-5844-4f78-b3a6-2f9f88ee1b24
keywords:
- SetupAPI 関数 WDK、保護者の方を決定します。
- 存在デバイス WDK
- WDK SetupAPI を決定する親デバイス
- デバイスの親 WDK
- WDK の親子関係
- 親子のリレーションシップを保存しています
- 親子リレーションシップを取得します。
- WDK の先祖の接続されているシーケンス
- WDK の先祖
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c035b398accb563efca4635424e0e0f8f690aba1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551564"
---
# <a name="determining-the-parent-of-a-nonpresent-device"></a>存在のデバイスの親を判断します。





このセクションで説明したアプローチを使用するには、親を判断する、*存在デバイス*存在デバイスと親の間のリレーションシップが固定されている場合にのみです。 (存在デバイスと親の間のリレーションシップが固定されていない場合は使用できませんこのメソッド存在のデバイスに、特定の親があるないため)。

たとえば、このメソッドは、多機能プリンターなどを 1 つまたは複数のインターフェイスを持つ子デバイスとして表される各 USB 複合デバイスに適用されます。 子インターフェイスのすべてのデバイスは、その親として、特定の複合デバイスの存在に依存しているため、デバイスと親の間のリレーションシップが固定されています。

次のトピックでは、このメソッドについて説明します。

[親/子リレーションシップを保存しています](#saving-the-parent-child-relationship)

[親/子リレーションシップを取得します。](#retrieving-the-parent-child-relationship)

[存在のデバイスの親のチェーンの処理](#handling-a-chain-of-ancestors-for-a-nonpresent-device)

### <a href="" id="saving-the-parent-child-relationship"></a> 親/子リレーションシップを保存しています

デバイスの親/子リレーションシップを保存するを指定する、*デバイスの共同インストーラー*デバイスのハードウェアのレジストリ キーの下のユーザーが作成したエントリの値で、デバイスの親のデバイス インスタンス ID を保存します。 デバイスのインスタンス ハンドルにはないシステムを再起動し、システムのプロセス間定数残っているために、デバイスのインスタンス ID を使用する必要があります。 処理する場合、 [ **DIF_INSTALLDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff543692)共同インストーラーで要求、デバイス インスタンス ID を保存する次の手順

***<em>直接の親のデバイス インスタンス ID をレジストリに保存するには</em>***

1.  呼び出す[ **CM_Get_Parent** ](https://msdn.microsoft.com/library/windows/hardware/ff538610)デバイスの親のデバイスのインスタンス ハンドルを取得します。

2.  親デバイスのデバイスのインスタンス ハンドルを使用して、呼び出す[ **CM_Get_Device_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff538405)親デバイスのデバイス インスタンス ID を取得します。

3.  呼び出す[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079) DIREG_DEV フラグを使用して、デバイスのハードウェアのレジストリ キーを識別するハンドルを取得しています。

4.  呼び出す**RegSetValueEx**デバイスのハードウェアのレジストリ キーの下のユーザーが作成したエントリの値で、親デバイスのデバイス インスタンス ID を保存します。

### <a href="" id="retrieving-the-parent-child-relationship"></a> 親/子リレーションシップを取得します。

デバイス インスタンス ID を取得するにはデバイスの共同インストーラーがデバイスのハードウェアのレジストリ キー エントリの値で、親デバイスのデバイス インスタンス ID を保存後

***<em>レジストリから親のデバイス インスタンス ID を取得するには</em>***

1.  呼び出す**SetupDiOpenDevRegKey** DIREG_DEV フラグを使用して、デバイスのハードウェアのレジストリ キーを識別するハンドルを取得します。

2.  呼び出す**RegQueryValueEx**をデバイスの共同インストーラーを設定するエントリの値で保存した親デバイスのデバイス インスタンス ID を取得します。

親デバイスのデバイス インスタンス ID を取得した後に呼び出す[ **SetupDiOpenDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff552071)を取得する、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)親デバイスの構造体。

### <a href="" id="handling-a-chain-of-ancestors-for-a-nonpresent-device"></a> 存在のデバイスの親のチェーンの処理

特定のデバイスの先祖の接続された一連のデバイス インスタンス Id が必要な場合に取得できる方法でレジストリにある各先祖のデバイス インスタンス ID を保存する必要があります。 これは、デバイスとすべての先祖間のリレーションシップが固定されている場合にのみ有効です。 ことに注意します。

デバイスの共同インストーラーを使用するはこれを行う方法の 1 つ**CM_Get_Parent**すべての先祖のすべてのデバイスのインスタンス Id を取得し、デバイスのハードウェアのレジストリ キーの下のさまざまな入力値をそれぞれのインスタンス ID を保存します。 説明されているメソッドを使用する[、親/子リレーションシップを保存](#saving-the-parent-child-relationship)先祖のデバイス インスタンス ID を保存します。 ID を取得する各デバイス インスタンスと同じ方法でに説明されている[親/子リレーションシップを取得する](#retrieving-the-parent-child-relationship)します。

 

 





