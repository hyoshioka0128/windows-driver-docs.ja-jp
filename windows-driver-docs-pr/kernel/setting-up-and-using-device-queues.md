---
title: デバイス キューのセットアップと使用
description: デバイス キューのセットアップと使用
ms.assetid: 5221ffc0-0cb4-498b-9be2-4d240b5f2744
keywords:
- デバイスのキュー WDK Irp を設定します。
- デバイスは、WDK の Irp でオブジェクトをキューします。
- Irp をキューに挿入します。
- デバイスのキュー オブジェクトを保存します。
- 補足の IRP キュー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54294a7b37a30053b879193607d3dd8923029378
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325025"
---
# <a name="setting-up-and-using-device-queues"></a>デバイス キューのセットアップと使用





ドライバーがデバイスのキュー オブジェクトを呼び出すことによって設定[ **KeInitializeDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552126)ドライバーまたはデバイスの初期化時。 そのデバイスを起動した後、ドライバー Irp キューに挿入この呼び出して[ **KeInsertDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552180)または[ **KeInsertByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552178). 次の図は、これらの呼び出しを示しています。

![セットアップとデバイスのキューの使用](images/3devqobj.png)

この図に示すように、ドライバーは、常駐である必要がありますデバイスのキュー オブジェクトの記憶域を提供する必要があります。 通常はデバイスのキュー オブジェクトを設定するドライバーに必要な記憶域の提供、[デバイス拡張機能](device-extensions.md)ドライバーが作成したデバイスのオブジェクトが、記憶域にできるコント ローラーの拡張機能ドライバーを使用している場合、[コント ローラーオブジェクト](using-controller-objects.md)またはドライバーによって割り当てられた非ページ プール。

場合、ドライバーがデバイスの拡張機能でデバイスのキュー オブジェクトのストレージと、呼び出し**KeInitializeDeviceQueue**デバイス オブジェクトを作成したら、デバイスを開始する前にします。 つまり、ドライバーがからキューを初期化できますその[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンまたは PnP、処理[ **IRP\_MN\_の開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 呼び出しで**KeInitializeDeviceQueue**ドライバーがデバイスのキュー オブジェクトは、その記憶域へのポインターを渡します。

そのデバイスを起動した後、ドライバーに挿入できます IRP のデバイスのキューを呼び出して**KeInsertDeviceQueue**、キューの末尾に IRP を配置するか、 **KeInsertByKeyDeviceQueue**をIRP がドライバー決定に従って、キューに配置*SortKey*値、前の図に示すようにします。

これらの各サポート、ルーチンを返します。 は IRP がキューに挿入されたかどうかを示すブール値。 これらの各呼び出しもセット busy デバイスのキュー オブジェクトの状態キューが現在の場合 (Not ビジー) を空にします。 ただし場合は、キューが空の (Not ビジー状態)、どちらも**KeInsert*Xxx*DeviceQueue**ルーチンが IRP をキューに挿入します。 代わりに、デバイスのキュー オブジェクトの状態を Busy に設定し、返します**FALSE**します。 IRP がキュー登録されたされませんので、ドライバーする必要がありますに渡す他のドライバー ルーチンをさらに処理します。

**補足的なデバイスのキューを設定する場合は、この実装のガイドラインに従います。**

呼び出し時に**KeInsert*Xxx*DeviceQueue**返します**FALSE**、呼び出し元が別のドライバー ルーチンにさらに処理するためにキューに登録しようとした IRP を渡す必要があります。
ただし、呼び出し**KeInsert*Xxx*DeviceQueue**ドライバー呼び出さない限り、キューにするには [次へ] の IRP が挿入されるため、取り込み中、デバイスのキュー オブジェクトの状態を変更**KeRemove*Xxx*DeviceQueue**最初。

デバイスのキュー オブジェクトの状態が Busy に設定されている場合、ドライバーが IRP をさらに処理デキューまたは Not busy 次サポート ルーチンのいずれかを呼び出すことによって、状態をリセットできます。

-   [**KeRemoveDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553156)キューの先頭の IRP を削除するには

-   [**KeRemoveByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553152)ドライバー決定に従って選択 IRP を削除する*SortKey*値

-   [**KeRemoveEntryDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553163)キュー内の特定の IRP を削除するか、特定の IRP がキューにあるかどうかを判断するには

    **KeRemoveEntryDeviceQueue** IRP デバイスのキューであるかどうかを示すブール値を返します。

空がビジー状態であるデバイスのキューからのエントリを削除するこれらのルーチンのいずれかを呼び出すと、キューの状態が Not ビジーに変わります。

各デバイスのキュー オブジェクトが組み込み executive スピン ロックで保護されている (に表示されていない、[デバイスのキュー オブジェクトを使用して](#setting-up-and-using-device-queues)図)。 ドライバーが Irp をキューに挿入し、ドライバーのルーチンで実行されている以下よりまたは IRQL と等しくからマルチプロセッサ セーフ方式で削除結果として、ディスパッチ =\_レベル。 この IRQL 制限のためドライバーを呼び出すことはできません、 **Ke*Xxx*DeviceQueue**その ISR からルーチンまたは[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチンは、DIRQL でを実行します。

参照してください[を管理するハードウェアの優先順位](managing-hardware-priorities.md)と[スピン ロック](spin-locks.md)詳細についてはします。 特定のサポート ルーチンの IRQL 要件、ルーチンのリファレンス ページを参照してください。

 

 




