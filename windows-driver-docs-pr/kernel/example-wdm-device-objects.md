---
title: WDM デバイス オブジェクトの例
description: WDM デバイス オブジェクトの例
ms.assetid: 8da56415-5018-468c-99c7-3969e5c00285
keywords:
- デバイス オブジェクトの WDK カーネル、例
- マウスの WDK カーネル
- キーボードの WDK カーネル
- 機能のデバイス オブジェクトの WDK カーネル
- FDO WDK カーネル
- 物理デバイス オブジェクトの WDK カーネル
- Pdo WDK カーネル
- フィルター DOs WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73cd60fc30e362259d8721461ba247c2ba264d1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582044"
---
# <a name="example-wdm-device-objects"></a>WDM デバイス オブジェクトの例





次の図は、前に示した図の説明でキーボードとマウス デバイスを表すデバイス オブジェクトを示しています。[キーボードとマウスのハードウェア構成](sample-device-and-driver-configuration.md#keyboard-and-mouse-hardware-configurations)します。 図の説明に示すようにキーボードとマウスのドライバー[キーボードとマウス ドライバー レイヤー](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers) I/O サポート ルーチンを呼び出すことによってこれらのデバイス オブジェクトを作成 ([**IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)).

![キーボードとマウス デバイス オブジェクト](images/2sampdos.png)

キーボードとマウス デバイスの場合、対応するポートとクラス ドライバーは、デバイス オブジェクトを作成します。 ポート ドライバーでは、物理ポートを表すための物理デバイス オブジェクト (PDO) を作成します。 各クラス ドライバーでは、I/O 要求のターゲットとしてキーボードまたはマウス デバイスを表す (FDO) 独自の機能のデバイス オブジェクトを作成します。

各クラス ドライバーは、クラス ドライバーはそのドライバーは、ポート、ドライバーは、上記自体を連結できますので、次の下位レベルのドライバーのデバイス オブジェクト、ポインターを取得する I/O サポート ルーチンを呼び出します。 クラス ドライバーは、ターゲットの物理デバイスを表す PDO ポート ドライバーまでの I/O 要求を送信できます。

構成に追加オプションのフィルター ドライバーは、フィルター デバイス オブジェクトを作成 (フィルター操作を行います)。 クラス ドライバーは、オプションのフィルター ドライバーは自体がデバイス スタックの次の下位ドライバーにチェーンし、次の下位ドライバー ターゲット PDO の I/O 要求を送信します。

以前に示すように、[キーボードとマウス ドライバー レイヤー](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers)図、割り込みを生成するデバイスのすべてのポート ドライバーが割り込みオブジェクトを設定し、ISR. を登録する必要がありますので、各ポート ドライバーはバス (最下位レベル) ドライバーでは、

キーボードおよびキーボードとマウスのハードウェア構成で各デバイスが複数の割り込みのベクターを使用している場合に表示される補助デバイス コント ローラーの i8042 ドライバーなどのデバイスのデュアル ポート ドライバー。 このようなドライバーを記述するときにデバイスごとに個別の isr を特定の実装か、両方のデバイスの 1 つの ISR を実装します。

 

 




