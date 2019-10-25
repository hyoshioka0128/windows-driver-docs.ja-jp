---
title: ACPI 通知
description: PEP の AcceptAcpiNotification コールバックルーチンが受信する各 ACPI 通知には、通知の種類とデータパラメーターを示す通知パラメーターが付属しています。
ms.assetid: E4DD4386-8008-463B-B048-DE8E559A7456
keywords:
- AcceptAcpiNotification
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: cffafd3bdb8d2af44411ade19f480294d065cbfe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828678"
---
# <a name="acpi-notifications"></a>ACPI 通知

PEP の[*AcceptAcpiNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifyacpi)コールバックルーチンによって受信される各 ACPI 通知には、通知の種類を示す通知パラメーターと、そのデータ構造を指すデータパラメーター (指定された通知の種類に関する情報です。

この呼び出しでは、通知パラメーターは、通知の種類を示す PEP_NOTIFY_ACPI_XXX 定数値に設定されます。 データパラメーターが、この通知の種類に関連付けられている PEP_ACPI_XXX 構造体の型を指しています。

AcceptAcpiNotification コールバックルーチンでは、次の ACPI 通知 Id が使用されます。

|通知 ID |Value |関連付けられた構造体|
|---|---|---| 
|PEP_NOTIFY_ACPI_PREPARE_DEVICE| 0x01 |PEP_ACPI_PREPARE_DEVICE| 
|PEP_NOTIFY_ACPI_ABANDON_DEVICE |0x02 |PEP_ACPI_ABANDON_DEVICE |
|PEP_NOTIFY_ACPI_REGISTER_DEVICE |0x03 |PEP_ACPI_REGISTER_DEVICE |
|PEP_NOTIFY_ACPI_UNREGISTER_DEVICE |0x04 |PEP_ACPI_UNREGISTER_DEVICE |
|PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE |0x05 |PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE |
|PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION |0x06 |PEP_ACPI_QUERY_OBJECT_INFORMATION |
|PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD |0x07 |PEP_ACPI_EVALUATE_CONTROL_METHOD |
|PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES |0x08 |PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES |
|PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES |0x09 |PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES |


## <a name="pep_notify_acpi_prepare_device"></a>PEP_NOTIFY_ACPI_PREPARE_DEVICE 

通知: 値 PEP_NOTIFY_ACPI_PREPARE_DEVICE。
Data: 名前によってデバイスを識別する PEP_ACPI_PREPARE_DEVICE 構造体へのポインター。
 
PEP がデバイスに ACPI サービスを提供するかどうかを選択できるようにします。

Windows ACPI ドライバーがデバイスの列挙中に ACPI 名前空間で新しいデバイスを検出すると、Windows の電源管理フレームワーク (PoFx) はこの通知を送信します。 この通知は、AcceptAcpiNotification コールバックルーチンを実装する PEPs に送信されます。

PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知を送信するために、PoFx は PEP の AcceptAcpiNotification ルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_PREPARE_DEVICE であり、データパラメーターはデバイスの名前を含む PEP_ACPI_PREPARE_DEVICE 構造体を指します。 PEP がこのデバイスの ACPI サービスを提供する準備ができている場合、PEP はこの構造体の DeviceAccepted メンバーを TRUE に設定します。 このようなサービスの提供を拒否するために、PEP はこのメンバーを FALSE に設定します。

PEP が、デバイスの ACPI サービスを提供する準備ができていることを (DeviceAccepted = TRUE に設定することにより) 指定した場合、PoFx は、の ACPI サービスの唯一のプロバイダーとして pep を登録するために PEP a PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知を送信することで応答します。デバイス。 PoFx では、デバイスの ACPI サービスプロバイダーの役割を要求する PEP は1つだけです。

ベストプラクティスとして、PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知に対する応答としてデバイスの初期化を実行しないでください。 代わりに、デバイスの PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知が受信されるか、デバイスに対して ACPI 制御メソッド (たとえば、INI) が呼び出されるまで、この初期化を遅延させます。

PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_abandon_device"></a>PEP_NOTIFY_ACPI_ABANDON_DEVICE 

通知: 値 PEP_NOTIFY_ACPI_ABANDON_DEVICE。

Data: 破棄されたデバイスを識別する PEP_ACPI_ABANDON_DEVICE 構造体へのポインター。
 
指定されたデバイスが破棄され、PEP からの ACPI サービスが不要になったことを PEP に通知します。

Windows 電源管理フレームワーク (PoFx) は、デバイスがオペレーティングシステムによって使用されていないことを PEP に通知するために、この通知を送信します。 PEP は、この通知を使用して、デバイスの状態を追跡するために割り当てられた内部ストレージをクリーンアップします。

PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知を送信するために、PoFx は PEP の AcceptAcpiNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_ABANDON_DEVICE、データパラメーターは PEP_ACPI_ABANDON_DEVICE 構造体を指します。

PoFx は、前の PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知でデバイスの ACPI サービスを提供することを選択した PEP にのみ、この通知を送信します。 PEP が前の PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知でこれらのサービスを提供するように登録されている場合、PoFx は PEP_NOTIFY_ACPI_ABANDON_DEVICE を送信する前にデバイスの PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知を送信します。警告.

PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_register_device"></a>PEP_NOTIFY_ACPI_REGISTER_DEVICE
通知: 値 PEP_NOTIFY_ACPI_REGISTER_DEVICE。

Data: デバイスを識別する PEP_ACPI_REGISTER_DEVICE 構造体へのポインター。 この通知に対する応答として、PEP は、デバイスを識別するための有効な PEPHANDLE 値を作成し、このハンドル値を構造体に書き込むことを想定しています。
 
指定されたデバイスの ACPI サービスの唯一のプロバイダーとして PEP を登録します。

Windows 電源管理フレームワーク (PoFx) は、指定されたデバイスに対して ACPI サービスを提供する準備ができていることを示す PEP にこの通知を送信します。これは、以前の PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知で示されています。

PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知を送信するために、PoFx は PEP の AcceptAcpiNotification ルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_REGISTER_DEVICE であり、データパラメーターは、PEP が ACPI サービスを提供するデバイスを識別する PEP_ACPI_REGISTER_DEVICE 構造体を指します。

PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_unregister_device"></a>PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 

通知: 値 PEP_NOTIFY_ACPI_UNREGISTER_DEVICE。

Data: デバイスの PEPHANDLE が格納されている PEP_ACPI_UNREGISTER_DEVICE 構造体へのポインター。
 
PEP からの ACPI サービス用に指定されたデバイスの登録をキャンセルします。

この通知に対する応答として、PEP は、前の PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知で、このデバイス用に PEP が作成した PEPHANDLE を破棄できます。

PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知を送信するために、PoFx は PEP の AcceptAcpiNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_UNREGISTER_DEVICE、データパラメーターは PEP_ACPI_UNREGISTER_DEVICE 構造体を指します。

PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_enumerate_device_namespace"></a>PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 

通知: 値 PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE。

Data: デバイスの ACPI 名前空間内のオブジェクトの列挙体を含む PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 構造体へのポインター。
 
PEP に対して、指定されたデバイスで、ACPI 名前空間でサポートされる ACPI オブジェクト (ネイティブメソッド) の一覧を照会します。

Windows ACPI ドライバーは、この通知で列挙されたオブジェクトを使用して、指定したデバイスの名前空間を作成します。 その後、このデバイスを参照するときに、ACPI ドライバーは、これらのオブジェクトについてのみ PEP に対してクエリを実行します。

Windows 電源管理フレームワーク (PoFx) は、デバイスが検出された直後に PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知を送信し、PEP がデバイスの ACPI サービスを提供するように登録します。 この登録の詳細については、「PEP_NOTIFY_ACPI_REGISTER_DEVICE」を参照してください。

PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知を送信するために、PoFx は PEP の AcceptAcpiNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE、データパラメーターは PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 構造体を指します。

AcceptAcpiNotification ルーチンは、PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知を処理し、TRUE を返すことが想定されています。 そうしないと、バグチェックが発生します。

PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_query_object_information"></a>PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 

通知: 値 PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION。

Data: ACPI オブジェクトの属性を指定する PEP_ACPI_QUERY_OBJECT_INFORMATION 構造体へのポインター。

以前に列挙された ACPI オブジェクトに関する情報を PEP に照会します。

Windows 電源管理フレームワーク (PoFx) は、この通知を送信して、以前の PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知の処理中に列挙されたオブジェクトの属性を PEP に照会します。 現時点で列挙されるオブジェクトは、コントロールメソッドだけです。

PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知を送信するために、PoFx は PEP の AcceptAcpiNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION、データパラメーターは PEP_ACPI_QUERY_OBJECT_INFORMATION 構造体を指します。

PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_evaluate_control_method"></a>PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 

通知: 値 PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD。

Data: 評価する ACPI コントロールメソッド、このメソッドに渡す入力引数、および結果の出力バッファーを指定する PEP_ACPI_EVALUATE_CONTROL_METHOD 構造体へのポインター。

は、PEP が登録済みハンドラーである ACPI 制御メソッドを評価するために使用されます。

Windows ACPI ドライバーが PEP によって実装されている ACPI 制御方式を評価する必要がある場合、Windows 電源管理フレームワーク (PoFx) はこの通知を PEP に送信します。

PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知を送信するために、PoFx は PEP の AcceptAcpiNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD、データパラメーターは PEP_ACPI_EVALUATE_CONTROL_METHOD 構造体を指します。

プラットフォームデザイナーでは、PEP と ACPI ファームウェアのどちらを使用して特定の ACPI 制御方法を処理するかを選択できます。 PEP が ACPI 制御メソッド用に登録されたハンドラーである場合、PoFx は、PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知を PEP に送信することによって、このメソッドを評価するために Windows ACPI ドライバーからの要求に応答します。

PEP がデバイスに対して処理できる ACPI コントロールメソッドの例を次に示します。

デバイスの識別と構成: HID、_C、UID、ADR、CLS、_ SUB、CRS、_PRS、その他です。 デバイスの電源管理とウェイクアップ: PS0 から PS3、_DSW、およびその他の手順を実行します。 デバイス固有のメソッド: DSM と任意のデバイススタック固有の制御メソッド。 ACPI 時間やアラームデバイスなどの特殊なデバイスでは、この通知を使用して時間とアラームの方法 ((GCP、_SRT など) を評価します。 

PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_query_device_control_resources"></a>PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 

通知: 値 PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES。

Data: 電源リソースのリストを含む PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 構造体へのポインター。
 
デバイスの電力制御に必要な生のリソースの一覧を PEP に照会します。

この通知に対する応答として、PEP はデバイスの電力制御に必要な未加工のリソースの一覧を提供します。 Windows ACPI ドライバーでは、デバイスが必要とする電力リソースを予約し、対応する翻訳されたリソースの一覧を PEP に提供できるように、この一覧が必要になります (PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知を送信します). 詳細については、「未加工のリソースと変換されたリソース」を参照してください。

PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知を送信するために、Windows 電源管理フレームワーク (PoFx) は PEP の AcceptAcpiNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES、データパラメーターは PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 構造体を指します。

PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_translated_device_control_resources"></a>PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 

通知: 値 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES。

Data: 翻訳されたリソースの一覧を含む PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 構造体へのポインター。
 
PEP に、デバイスに必要なすべての電源管理リソースの変換されたリソースの一覧を提供します。

Windows の電源管理フレームワーク (PoFx) は、前の PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知に応答して、PEP に生のリソースが一覧表示された場合にこの通知を送信します。 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知は、PEP に、翻訳されたリソースの対応するリストを提供します。 詳細については、「未加工のリソースと変換されたリソース」を参照してください。

PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知を送信するために、PoFx は PEP の AcceptAcpiNotification コールバックルーチンを呼び出します。 この呼び出しでは、通知パラメーターの値は PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES、データパラメーターは PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 構造体を指します。

PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 
## <a name="pep_notify_acpi_work"></a>PEP_NOTIFY_ACPI_WORK 

通知: 値 PEP_NOTIFY_ACPI_WORK。

Data: PEP_WORK 構造体へのポインター。
 
PEP が RequestWorker ルーチンを呼び出して Windows 電源管理フレームワーク (PoFx) から作業項目を要求するたびに、PEP に1回送信されます。 この通知は、ACPI 専用の作業に使用されます。

PEP は、RequestWorker ルーチンを呼び出して作業項目を要求した後、PEP a PEP_NOTIFY_ACPI_WORK 通知を送信して応答します。 ただし、この通知は、作業項目を処理するために必要なリソース (ワーカースレッド) が使用可能になるまで送信されません。 このようにして、PoFx は、通知中に PEP が PoFx に渡す作業要求がリソース不足のために失敗することを保証します。

入力時、PEP は PEP_WORK 構造体が初期化されていないと想定する必要があります。 この通知を処理するには、PEP は、要求されている作業を記述する PEP に割り当てられた PEP_WORK_INFORMATION 構造体を指すように、ワーク情報メンバーを設定する必要があります。 さらに、pep は、PEP_WORK 構造体の必要な作業メンバーを TRUE に設定して、PEP が PEP_NOTIFY_ACPI_WORK 通知を処理したこと、および work INFORMATION メンバーが有効な PEP_WORK_INFORMATION 構造を指していることを確認する必要があります。 PEP が通知を処理できなかった場合、または PEP_WORK_INFORMATION 構造体を割り当てることができない場合は、PEP で WORK INFORMATION メンバーを NULL に設定し、必要な作業メンバーを FALSE に設定する必要があります。

PEP_NOTIFY_ACPI_WORK 通知の場合、AcceptAcpiNotification ルーチンは常に IRQL = PASSIVE_LEVEL で呼び出されます。
 


