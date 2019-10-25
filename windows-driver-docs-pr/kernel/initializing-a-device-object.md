---
title: デバイス オブジェクトの初期化
description: デバイス オブジェクトの初期化
ms.assetid: 97820c62-aade-4ae7-92a6-7490d0ad5697
keywords:
- デバイスオブジェクト WDK カーネル、初期化
- デバイスオブジェクトの初期化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53a64482195cfa380aec5cb09f727fa4ee8799de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828299"
---
# <a name="initializing-a-device-object"></a>デバイス オブジェクトの初期化





[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)が返された後、[*デバイス拡張機能*](device-extensions.md)へのポインターを含む*DeviceObject*へのポインターを呼び出し元に与えると、ドライバーは、デバイスオブジェクト内の特定のフィールドをそれぞれの物理、論理、および/またはに設定する必要があります。仮想デバイス。

**IoCreateDevice**は、新しく作成されたデバイスオブジェクトの**StackSize**フィールドを1に設定します。 最下位レベルのドライバーでは、このフィールドを無視できます。 上位レベルのドライバーが[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)を呼び出して、それ自体を次の下位のドライバーにアタッチすると、そのルーチンによって、デバイスオブジェクトの**StackSize**フィールドが、次に低いドライバーのデバイスオブジェクトと1つの値に自動的に設定されます。 ただし、デバイスの種類によっては、デバイス固有のドキュメントに記載されているように、上位レベルのドライバーで**StackSize**フィールドをより大きな値に設定することが必要になる場合があります。 スタックサイズを設定すると、上位レベルのドライバーに送信される Irp には、ドライバー固有の i/o スタックの場所が含まれ、チェーン内のすべての下位のドライバーに対して、正しい数の i/o スタックの場所が含まれるようになります。

**IoCreateDevice**は、直接 i/o で使用されるバッファーが適切にアラインされるように、新しく作成されたデバイスオブジェクトのの**要求**フィールドをプロセッサのデータキャッシュの行サイズから1つ引いた値に設定します。 **IoCreateDevice**が返された後、最下位レベルの物理デバイスドライバーは次の操作を行う必要があります。

1.  デバイスのアラインメント要件から1つを減算します。

2.  ステップ1の結果とデバイスオブジェクトの現在の値を比較**します。**

3.  デバイスのアラインメント要件が大きい場合は、手順 1. の結果に [配置**要件**] を設定します。 それ以外の場合は、 **IoCreateDevice**によって設定された並べ替え**要件**の値をそのまま使用します。

[**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)を呼び出すことにより上位レベルのドライバーが別のドライバーにチェーンされた後、上位レベルのドライバーは、新しく作成されたデバイスオブジェクトの [並べ替えの**要件**] フィールドを次の下位レベルのものに設定する必要があります。ドライバーのデバイスオブジェクト。 一般的な規則として、上位レベルのドライバーではこの値を変更しないでください。 上位レベルのドライバーが[**ioattachdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)または[**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)を呼び出すと、これらのルーチンによって、デバイスオブジェクトの [値の自動**設定] フィールドが下位**レベルのドライバーのデバイスオブジェクトの値に自動的に設定されます。

[**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)は、下位レベルのドライバーのデバイスオブジェクトと関連付けられているファイルオブジェクトの両方にポインターを返します。 返されたファイルオブジェクトポインターを使用できるのは、FSD (または他の最上位レベルのドライバー) だけです。 **Iogetdeviceobjectpointer**を呼び出す中間ドライバーは、ドライバーがアンロードされたときに[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出すことによって逆参照できるように、このファイルオブジェクトポインターを保存する必要があります。

FSD は、下位のドライバーのデバイスオブジェクトを表すファイルオブジェクトを含むボリュームをマウントした後、 **Ioattachdevice**または**を呼び出して、ファイルシステムと下位ドライバーの間で中間ドライバーをチェーンすることはできません。IoAttachDeviceToDeviceStack**。 また、FSD は、マウントが発生したときに、基になるボリュームハードウェアのジオメトリに基づいて、デバイスオブジェクトの**SectorSize**メンバーを設定できます。 詳細については、「[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)」を参照してください。

また、中間レベルまたは最下位のドライバーは、デバイスオブジェクトの**フラグ**にビットを設定します。これは、作成されるすべてのデバイスオブジェクトで IO\_IO\_バッファー io を使用して\_\_します。 論理デバイスまたは仮想デバイスの最上位レベルのドライバーでは、関連する追加の作業がドライバーの実行によって決定された場合に、バッファーまたは直接 i/o の**フラグ**を設定しないようにすることができます。 中間ドライバーは、デバイスオブジェクトの**Flags**フィールドを、次に低いドライバーのデバイスオブジェクトのものと一致するように設定する必要があります。

DO\_DIRECT\_IO によってデバイスオブジェクト**フラグ**フィールドを設定するか、バッファー\_IO\_実行すると、i/o マネージャーが、その後ドライバーに送信されるすべてのデータ転送要求のユーザーバッファーに対するアクセス権をどのように渡すかが決まります。

その後、ドライバーはデバイスオブジェクト内のその他のデバイスに依存する値を設定できます。 たとえば、リムーバブルメディアデバイス用の非 WDM ドライバーは、i/o 操作中に**メディアの変更**を検出 (または問題あり) する場合に、\_ボリュームを\_確認する必要があります。 (詳細については、「[リムーバブルメディアのサポート](supporting-removable-media.md)」を参照してください)。突入電流電源が必要なデバイスのドライバー、またはの**フラグ**メンバーが突入電流を\_\_使用する必要があります。また、システムのページングパスにないデバイスのドライバー、またはの**フラグ**メンバーが電源\_pagable を\_する必要があります。 関数ドライバーとフィルタードライバーは、DO\_デバイス\_初期化フラグをクリアする必要があります。

デバイスオブジェクトを初期化した後、ドライバーは、デバイス拡張機能に格納されているカーネル定義オブジェクトやその他のシステム定義データ構造を初期化することもできます。 ドライバーがこれらのタスクを実行するタイミングは、デバイス、オブジェクトの種類、またはデータの性質によって異なります。 一般に、PnP の開始要求と停止要求を通じて保持できるオブジェクトまたはデータ構造は、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで初期化できます。 PnP Irp\_によって提供されるリソース情報を必要とするものは、\_デバイスの要求を[**開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)か、デバイスの停止時または再起動時に変更が必要になる可能性があるため、ドライバーが IRP を処理するときに初期化される必要があります。 **\_は、\_デバイス**の要求を開始\_ます。 *AddDevice*ルーチンの詳細については、「 [AddDevice ルーチンを記述する](writing-an-adddevice-routine.md)」を参照してください。

 

 




