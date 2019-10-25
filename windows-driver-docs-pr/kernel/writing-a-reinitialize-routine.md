---
title: 再初期化ルーチンを記述する
description: 再初期化ルーチンを記述する
ms.assetid: 47a7dd3f-e474-49c7-adf2-11f6e788c261
keywords:
- 標準ドライバールーチン WDK カーネル、再初期化ルーチン
- ドライバールーチン WDK カーネル、再初期化ルーチン
- ルーチン WDK カーネル、再初期化ルーチン
- 初期化
- ドライバーの再初期化 (WDK)
- ドライバーの再初期化 WDK カーネル
- ドライバーの初期化 WDK カーネル
- ドライバーの初期化 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d038c38963eba02e6d78412bf928b182a3ad19d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835606"
---
# <a name="writing-a-reinitialize-routine"></a>再初期化ルーチンを記述する





ステージで自身を初期化する必要があるドライバーには、[*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)ルーチンを含めることができます。 *再初期化*ルーチンは、 [**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンが制御を返し、他のドライバーがそれ自体を初期化した後に呼び出されます。 通常、*再初期化*ルーチンは、別のドライバーの開始後に実行する必要があるタスクを実行します。

たとえば、システムのキーボードクラスドライバー **kbdclass**は、PnP と従来のキーボードポートの両方をサポートしています。 PnP マネージャーが検出できない従来のポートがシステムに1つ以上含まれている場合、キーボードクラスドライバーはポートごとにデバイスオブジェクトを作成する必要があり、ポートの下位レベルのドライバーに対してはレイヤー自体を作成する必要があります。 その結果、クラスドライバーには、 **Driverentry**ルーチンと[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが呼び出され、他のドライバーが読み込まれた後に呼び出される*再初期化*ルーチンがあります。 *再初期化*ルーチンは、ポートを検出し、そのデバイスオブジェクトを作成し、デバイスの他の下位レベルのドライバーを介してドライバーをレイヤー化します。

ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、 [**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)を呼び出して、実行の*再初期化*ルーチンをキューに登録します。 *再初期化*ルーチンは、 **IoRegisterDriverReinitialization**自体を呼び出すこともできます。これにより、ルーチンが再度キューに登録されます。 *再初期化*するパラメーターの1つは、呼び出された回数を示します。

**IoRegisterDriverReinitialization**の呼び出しには、ドライバー定義のコンテキストデータへのポインターを含めることができます。このデータは、システムによって*再初期化*の入力として提供されます。 *再初期化*ルーチンがレジストリを使用する場合、このポインターは*再初期化*ルーチンの入力パラメーターではないため、 **driverentry**ルーチンに渡された*RegistryPath*ポインターがコンテキストデータに含まれている必要があります。

**Driverentry**が正常\_状態を返さない場合、*再初期化*ルーチンは呼び出されません。

通常、*再初期化*ルーチンを使用するドライバーは、PnP デバイスとレガシデバイスの両方を制御する上位レベルのドライバーです。 Pnp マネージャーが検出したデバイス (および PnP マネージャーがドライバーの*AddDevice*ルーチンを呼び出すデバイス) のデバイスオブジェクトを作成するだけでなく、ドライバーは、pnp マネージャーが列挙しないレガシデバイス用のデバイスオブジェクトも作成する必要があります。 *再初期化*ルーチンは、基になるデバイスの次の下位のドライバーを使用して、これらのデバイスオブジェクトとレイヤーを作成します。

ドライバーに*再初期化*ルーチンがある場合は、「 [Driverentry ルーチンの記述](writing-a-driverentry-routine.md)」で説明されているのと同じ基本的な手順で初期化されます。また、 **driverentry**ルーチンと同じ基本要件もあります。

 

 




