---
title: デバイス オブジェクトの初期化
description: デバイス オブジェクトの初期化
ms.assetid: 97820c62-aade-4ae7-92a6-7490d0ad5697
keywords:
- デバイス オブジェクトの WDK カーネルの初期化
- デバイス オブジェクトの初期化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 348b2c19535a2cd1852ac5ffef7aa03ff20e1703
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369793"
---
# <a name="initializing-a-device-object"></a>デバイス オブジェクトの初期化





後[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)返します、呼び出し元へのポインターを提供する*デバイス オブジェクト*へのポインターを格納している、 [*デバイス拡張機能*](device-extensions.md)ドライバーは、それぞれの物理、論理、および仮想デバイスのデバイス オブジェクトの特定のフィールドを設定する必要があります。

**IoCreateDevice**設定、 **StackSize**いずれかに新しく作成したデバイス オブジェクトのフィールド。 最下位レベルのドライバーでは、このフィールドを無視できます。 高度なドライバーを呼び出すと[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)ルーチン自体を次の下位ドライバーに添付する設定に自動的に、 **StackSize**フィールド次の下位ドライバーのデバイス オブジェクトと 1 つのデバイス オブジェクト。 デバイスの種類によっては、ただしより高度なドライバーが設定する必要が、 **StackSize**デバイス固有のドキュメントで説明したように大きい値をフィールド。 スタック サイズを設定すると、ドライバーに固有では I/O スタックの場所と、I/O スタックの場所、チェーン内のすべての下位のドライバーの正しい数上位レベルのドライバーに送信される Irp にが含まれます。

**IoCreateDevice**設定、 **AlignmentRequirement**からダイレクト I/O に使用されるバッファーを正しく整列していることを確認する 1 を引いた、プロセッサのデータのキャッシュ ラインのサイズを新しく作成したデバイス オブジェクトのフィールド。 後**IoCreateDevice**返します、最下位レベルの物理的なデバイス ドライバーは、次を実行する必要があります。

1.  デバイスのアラインメント要件から 1 を減算します。

2.  デバイス オブジェクトの現在の値で、手順 1 の結果を比較**AlignmentRequirement**します。

3.  デバイスのアラインメント要件が大きい場合は、設定**AlignmentRequirement**手順 1 の結果にします。 それ以外の場合、ままにして、 **AlignmentRequirement**によって設定された値**IoCreateDevice**します。

高度なドライバーがチェーン自体別のドライバー経由で呼び出すことによって後[ **IoGetDeviceObjectPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)、上位レベルのドライバーを設定する必要があります、 **AlignmentRequirement**の下位レベルの次のドライバーのデバイス オブジェクトの新しく作成したデバイス オブジェクトのフィールド。 一般的な規則としてより高度なドライバーはこの値を変更する必要があります。 高度なドライバーを呼び出す場合[ **IoAttachDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevice)または[ **IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)、これらのルーチンが自動的に設定します**AlignmentRequirement**フィールドの下位レベルのドライバーのデバイス オブジェクトのデバイス オブジェクトにします。

[**IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)下位レベルのドライバーのデバイス オブジェクトと関連付けられているファイルのオブジェクトの両方のポインターを返します。 FSD のみ (または、場合によっては、別の最上位レベルのドライバー)、返されるファイル オブジェクト ポインターを使用することができます。 呼び出すための中間ドライバー **IoGetDeviceObjectPointer**呼び出すことによって逆参照できるように、このファイル オブジェクト ポインターを保存する必要があります[ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)ときドライバーでは、読み込まれます。

FSD は、下位のドライバーのデバイス オブジェクトを表すファイル オブジェクトを含むボリュームをマウント後、中間ドライバーことはできませんチェーン自体、ファイル システムおよび下位のドライバーの間で呼び出すことによって**IoAttachDevice**または**IoAttachDeviceToDeviceStack**します。 さらに、FSD が設定できる、**セクタサイズ**マウントが発生した場合、基になるボリュームのハードウェアのジオメトリ ベースのデバイス オブジェクトのメンバー。 詳細については、次を参照してください。 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)します。

中級以上の最下位レベルのドライバーもビットを設定、デバイス オブジェクトの**フラグ**Or で、いずれかで\_直接\_IO または操作を行います\_バッファーに格納された\_オブジェクトのすべてのデバイスの IO作成します。 論理または仮想デバイスの最上位レベルのドライバーは、設定を回避できます**フラグ**ドライバー ライターに関連する追加作業が決定した場合は、直接またはバッファー内のいずれかの I/O がドライバーのパフォーマンスが向上支払いいただけます。 中間のドライバーをセットアップする必要があります、**フラグ**次の下位ドライバーのデバイス オブジェクトの一致するように、デバイス オブジェクトのフィールド。

デバイス オブジェクトを設定**フラグ**フィールドの操作を行います\_直接\_IO または\_バッファーに格納された\_IO は、I/O マネージャーを渡す方法へのアクセスでは、すべてのデータ転送バッファーをユーザーに要求を決定します。その後、ドライバーに送信されます。

ドライバーは、デバイス オブジェクトの他のデバイスに依存する値を設定できます。 たとえば、リムーバブル メディア デバイスの非 WDM ドライバーが必要があります OR デバイス オブジェクトの**フラグ**でメンバー\_を確認してください\_ボリュームが検出 (または疑いがある) 場合、メディア、I/O 操作中に変更します。 (を参照してください[リムーバブル メディアをサポートしている](supporting-removable-media.md)詳細についてはします)。突入電力を必要とするデバイスのドライバーにする必要がありますまたは**フラグ**かメンバー\_POWER\_突入、およびシステムのページング パス上にないデバイスのドライバーにする必要がありますまたは**フラグ**かメンバー\_POWER\_PAGABLE します。 関数とフィルター ドライバーをオフに、操作を実行する必要があります\_デバイス\_フラグを初期化しています。

デバイス オブジェクトを初期化した後、ドライバーはカーネル定義オブジェクトとデバイスの拡張機能での記憶域を提供してその他のシステム定義のデータ構造も初期化できます。 ドライバーがこれらのタスクを実行する場合に正確には、そのデバイスは、オブジェクトの種類やデータの性質によって異なります。 PnP の開始を永続化および要求を停止できるオブジェクトやデータ構造を初期化してで一般に、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。 PnP で提供されたリソース情報を必要とする[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)デバイスが、要求、またはをすると、変更が必要する可能性があります停止または再起動されると、ドライバーが処理されるときに初期化する必要があります、 **IRP\_MN\_開始\_デバイス**要求。 詳細については*AddDevice*ルーチンを参照してください[、AddDevice ルーチンを記述](writing-an-adddevice-routine.md)します。

 

 




