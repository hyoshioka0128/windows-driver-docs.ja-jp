---
title: 再初期化ルーチンの記述
description: 再初期化ルーチンの記述
ms.assetid: 47a7dd3f-e474-49c7-adf2-11f6e788c261
keywords:
- 標準のドライバー ルーチン WDK カーネルの再初期化ルーチン
- ドライバーのルーチンの WDK カーネル、再初期化ルーチン
- ルーチンの WDK カーネル、再初期化ルーチン
- 再初期化します。
- ドライバー WDK 再初期化します。
- ドライバーの再初期化の WDK カーネル
- ドライバーの初期化の WDK カーネル
- ドライバー WDK カーネルの初期化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 635d8141bc16c872d49447681242dd92bb721d16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574734"
---
# <a name="writing-a-reinitialize-routine"></a>再初期化ルーチンの記述





段階的に初期化する必要がある任意のドライバーを含めることができます、 [*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)ルーチン。 A*を再初期化*ルーチンが呼び出された後、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンにコントロールとその他のドライバーが初期化自体が返されます。 通常、*を再初期化*ルーチンが別のドライバーが開始した後に行う必要があるタスクを実行します。

たとえば、システムのキーボード クラス ドライバー、 **kbdclass**、PnP と従来のキーボードの両方のポートをサポートしています。 システムには、検出できない、PnP マネージャー 1 つまたは複数のレガシ ポートが含まれている場合キーボード クラス ドライバーが各ポートおよびポートの下位レベルのドライバーよりも層自体のデバイス オブジェクトを作成それでもする必要があります。 そのため、クラス ドライバーは、*を再初期化*後に呼び出されるルーチンをその**DriverEntry**と[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンがあります。されて呼び出されるとその他のドライバーが読み込まれていません。 *を再初期化*ルーチンがポートを検出、デバイス オブジェクトを作成し、デバイスの他の下位レベルのドライバーをドライバーをレイヤーします。

ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンの呼び出し[ **IoRegisterDriverReinitialization** ](https://msdn.microsoft.com/library/windows/hardware/ff549511)キューに、*を再初期化*ルーチンを実行します。 *を再初期化*ルーチンを呼び出すことも**IoRegisterDriverReinitialization**自体がキューに再登録するルーチンを発生します。 1 つのパラメーターの*を再初期化*が呼び出された回数を示します。

呼び出し**IoRegisterDriverReinitialization**への入力として、システムが提供するコンテキストのドライバーによるデータへのポインターを含めることができます*を再初期化*します。 場合、*を再初期化*ルーチンは、レジストリを使用して、コンテキスト データを含める必要があります、 *RegistryPath*に渡されたポインター、 **DriverEntry**ルーチンのためこれポインターへの入力パラメーターでない、*を再初期化*ルーチン。

*を再初期化*場合、ルーチンは呼び出されません**DriverEntry**状態を返さない\_成功します。

ドライバー、通常、*を再初期化*ルーチンは PnP と従来の両方のデバイスを制御する高度なドライバーです。 PnP マネージャーを検出するデバイスのデバイス オブジェクトを作成するだけでなく (、PnP マネージャーを呼び出し、ドライバーの*AddDevice*ルーチン)、ドライバー作成する必要がありますもレガシ デバイスのデバイス オブジェクトを PnPマネージャーは列挙されません。 *を再初期化*ルーチンを作成しますデバイス オブジェクトとレイヤー ドライバーを基になるデバイスの次の下位ドライバー。

ドライバーがある場合、*を再初期化*で説明されている同じ基本的な手順で初期化ルーチンを[DriverEntry ルーチンを記述](writing-a-driverentry-routine.md)と同じ基本的な要件があるその**DriverEntry**ルーチン。

 

 




