---
title: WDM デバイスオブジェクトの例
description: WDM デバイスオブジェクトの例
ms.assetid: 8da56415-5018-468c-99c7-3969e5c00285
keywords:
- デバイスオブジェクト WDK カーネル、例
- マウスの WDK カーネル
- キーボード WDK カーネル
- 機能デバイスオブジェクト WDK カーネル
- FDO WDK カーネル
- 物理デバイスオブジェクト WDK カーネル
- PDOs WDK カーネル
- DOs WDK カーネルをフィルター処理する
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fb50153d4b9d9d1ccf335d49639cad07b28290f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838704"
---
# <a name="example-wdm-device-objects"></a>WDM デバイスオブジェクトの例





次の図は、[キーボードとマウスのハードウェア構成](sample-device-and-driver-configuration.md#keyboard-and-mouse-hardware-configurations)を示す、前に示したキーボードとマウスのデバイスを表すデバイスオブジェクトを示しています。 次の図に示すように、キーボードとマウスのドライバーは、i/o サポートルーチン ([**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)) を呼び出すことによって、これらのデバイスオブジェクト[を作成し](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers)ます。

![キーボードおよびマウスデバイスオブジェクト](images/2sampdos.png)

キーボードとマウスデバイスの場合、それぞれのポートとクラスのドライバーがデバイスオブジェクトを作成します。 ポートドライバーは、物理ポートを表す物理デバイスオブジェクト (PDO) を作成します。 各クラスドライバーは、i/o 要求のターゲットとしてキーボードまたはマウスデバイスを表す独自の機能デバイスオブジェクト (FDO) を作成します。

各クラスドライバーは、次の下位レベルのドライバーのデバイスオブジェクトへのポインターを取得するために i/o サポートルーチンを呼び出します。そのため、クラスドライバーは、そのドライバー (ポートドライバー) を上にチェーンすることができます。 次に、クラスドライバーは、物理デバイスを表すターゲット PDO のポートドライバーに i/o 要求を送信できます。

構成に追加されるオプションのフィルタードライバーによって、フィルターデバイスオブジェクト (フィルター処理) が作成されます。 クラスドライバーと同様に、オプションのフィルタードライバーは、デバイススタック内の次の下位のドライバーにそれ自体をチェーンし、ターゲット PDO の i/o 要求を次の下位のドライバーに送信します。

前に[キーボードおよびマウスドライバーレイヤー](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers)の図に示したように、各ポートドライバーはバス (最低レベル) のドライバーであるため、割り込みを生成するデバイスのすべてのポートドライバーは、割り込みオブジェクトを設定し、ISR を登録する必要があります。

デュアルデバイスポートドライバー。各デバイスが別の割り込みベクターを使用している場合、キーボードおよびマウスのハードウェア構成に表示される、キーボードおよび補助デバイスコントローラー用の i8042 ドライバーなどです。 このようなドライバーを作成する場合は、デバイスごとに個別の Isr を実装するか、両方のデバイスに対して単一の ISR を実装することができます。

 

 




