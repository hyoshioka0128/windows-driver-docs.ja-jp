---
title: ACPI 通知
description: PEP の AcceptAcpiNotification コールバック ルーチンを受信する各 ACPI 通知は、通知の種類を示す通知パラメーターとデータのパラメーターを伴います。
ms.assetid: E4DD4386-8008-463B-B048-DE8E559A7456
keywords:
- AcceptAcpiNotification
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 654f80a38ba4ff0a2b4edc60521e3be188185c8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572060"
---
# <a name="acpi-notifications"></a>ACPI 通知

各 ACPI 通知コールバック ルーチンを受け取る、PEP の AcceptAcpiNotification、通知の種類を示す通知パラメーターと共に、データのパラメーターをデータを指す構造体の情報が含まれています、通知の種類を指定します。

この呼び出しでは、通知のパラメーターは、通知の種類を示す PEP_NOTIFY_ACPI_XXX 定数値に設定されます。 データのパラメーターは、この通知の種類に関連付けられている PEP_ACPI_XXX 構造体型を指します。

次の ACPI 通知 Id は、AcceptAcpiNotification コールバック ルーチンで使用されます。

|通知 ID |値 |関連付けられている構造|
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


## <a name="pepnotifyacpipreparedevice"></a>PEP_NOTIFY_ACPI_PREPARE_DEVICE 

通知:PEP_NOTIFY_ACPI_PREPARE_DEVICE 値。
データ:名前で、デバイスを識別する PEP_ACPI_PREPARE_DEVICE 構造体へのポインター。
 
デバイスを ACPI サービスを提供するかどうかを選択する、PEP を使用できます。

Windows の電源管理フレームワーク (PoFx) は、ACPI の Windows ドライバーは、デバイスの列挙中に、ACPI 名前空間に新しいデバイスを検出した場合、この通知を送信します。 Pep AcceptAcpiNotification コールバック ルーチンを実装するには、この通知が送信されます。

PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知を送信するには、PoFx PEP の AcceptAcpiNotification ルーチンを呼び出すとします。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_PREPARE_DEVICE、およびデバイスの名前を含む PEP_ACPI_PREPARE_DEVICE 構造をデータ パラメーターのポイントが。 PEP がこのデバイスを ACPI サービスを提供する準備が完了している場合、PEP この構造体の DeviceAccepted メンバーを TRUE に設定します。 拒否すると、このようなサービスを提供する、するには、PEP は、このメンバーを FALSE に設定します。

PEP を示している場合 (DeviceAccepted を設定して = TRUE) ことは、デバイスを ACPI サービスを提供する準備ができて、PoFx は、PEP の ACPI サービスの唯一のプロバイダーである、PEP を登録する PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知を送信して応答がデバイスです。 PoFx には、デバイスを ACPI サービス プロバイダーの役割を要求する 1 つだけの PEP が期待しています。

ベスト プラクティスとしては行いません任意のデバイスの初期化 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知に応答します。 代わりに、デバイスの PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知を受信すると、か、またはデバイスを ACPI コントロール メソッド (たとえば、_INI) が呼び出されるまでは、この初期化を延期します。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpiabandondevice"></a>PEP_NOTIFY_ACPI_ABANDON_DEVICE 

通知:PEP_NOTIFY_ACPI_ABANDON_DEVICE 値。

データ:破棄済みのデバイスを識別する PEP_ACPI_ABANDON_DEVICE 構造体へのポインター。
 
PEP を通知するは、指定したデバイスは破棄されましたし、PEP から ACPI サービスは不要します。

Windows の電源管理フレームワーク (PoFx) は、デバイスのオペレーティング システムで使用が不要になった PEP に通知するには、この通知を送信します。 PEP は、この通知を使用して、デバイスの状態を追跡するために、割り当てられている任意の内部ストレージをクリーンアップすることができます。

PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知を送信するには、PoFx は、PEP の AcceptAcpiNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_ABANDON_DEVICE と PEP_ACPI_ABANDON_DEVICE 構造体へのデータ パラメーターのポイントが。

PoFx は、ACPI サービスで、前の PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知デバイスを提供するが選択している PEP にのみ、この通知を送信します。 PoFx が、PEP_NOTIFY_ACPI_ABANDON_DEVICE を送信する前に、デバイスの PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知を送信 PEP が前回の PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知は、これらのサービスを提供する登録されている場合通知します。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_ABANDON_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpiregisterdevice"></a>PEP_NOTIFY_ACPI_REGISTER_DEVICE
通知:PEP_NOTIFY_ACPI_REGISTER_DEVICE 値。

データ:デバイスを識別する PEP_ACPI_REGISTER_DEVICE 構造体へのポインター。 この通知に応答して、PEP は、このハンドルの値を構造体に記述して、デバイスを識別する有効な PEPHANDLE 値を作成する予測されます。
 
指定されたデバイスを ACPI サービスの唯一のプロバイダーである、PEP を登録します。

Windows 電源管理フレームワーク (PoFx) が示されている PEP にこの通知を送信する — 以前 PEP_NOTIFY_ACPI_PREPARE_DEVICE 通知で — ACPI サービスは、指定されたデバイスを提供する準備が整っています。

PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知を送信するには、PoFx PEP の AcceptAcpiNotification ルーチンを呼び出すとします。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_REGISTER_DEVICE、PEP の ACPI サービスの提供対象のデバイスを識別する PEP_ACPI_REGISTER_DEVICE 構造体へのデータのパラメーター項目が。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpiunregisterdevice"></a>PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 

通知:PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 値。

データ:デバイスの PEPHANDLE を格納する PEP_ACPI_UNREGISTER_DEVICE 構造体へのポインター。
 
PEP から ACPI サービスの指定したデバイスの登録をキャンセルします。

この通知に応答して、PEP は、PEP は、前の PEP_NOTIFY_ACPI_REGISTER_DEVICE 通知では、このデバイスの作成 PEPHANDLE を破棄できます。

PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知を送信するには、PoFx は、PEP の AcceptAcpiNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_UNREGISTER_DEVICE と PEP_ACPI_UNREGISTER_DEVICE 構造体へのデータ パラメーターのポイントが。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_UNREGISTER_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpienumeratedevicenamespace"></a>PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 

通知:PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 値。

データ:デバイスの ACPI 名前空間内のオブジェクトの列挙体を格納する PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 構造体へのポインター。
 
ACPI オブジェクト (ネイティブ メソッド) が、指定されたデバイスを ACPI 名前空間の下で、PEP でサポートされているの一覧については、PEP を照会します。

ACPI の Windows ドライバーでは、この通知によって列挙オブジェクトを使用して、指定したデバイスの名前空間を作成します。 その後、このデバイスの場合は、ACPI ドライバーはこれらのオブジェクトに対してのみ、PEP をクエリします。

Windows の電源管理フレームワーク (PoFx) は、デバイスが探索し、デバイスを ACPI サービスを提供する、PEP を登録後すぐに、PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知を送信します。 この登録の詳細については、PEP_NOTIFY_ACPI_REGISTER_DEVICE を参照してください。

PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知を送信するには、PoFx は、PEP の AcceptAcpiNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE と PEP_ACPI_ENUMERATE_DEVICE_NAMESPACE 構造体へのデータ パラメーターのポイントが。

PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知を処理して TRUE を返すには、AcceptAcpiNotification ルーチンが必要です。 これに失敗には、バグ チェックが実行します。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpiqueryobjectinformation"></a>PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 

通知:PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 値。

データ:ACPI オブジェクトの属性を指定する PEP_ACPI_QUERY_OBJECT_INFORMATION 構造体へのポインター。

以前に列挙された ACPI オブジェクトについては、PEP を照会します。

Windows 電源管理フレームワーク (PoFx) は、前の PEP_NOTIFY_ACPI_ENUMERATE_DEVICE_NAMESPACE 通知の処理中に列挙されたオブジェクトの属性の PEP を照会するには、この通知を送信します。 現時点では、列挙されるオブジェクトはのみ制御メソッドです。

PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知を送信するには、PoFx は、PEP の AcceptAcpiNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION と PEP_ACPI_QUERY_OBJECT_INFORMATION 構造体へのデータ パラメーターのポイントが。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_QUERY_OBJECT_INFORMATION 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpievaluatecontrolmethod"></a>PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 

通知:PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 値。

データ:このメソッドをおよび結果の出力バッファーに提供する入力引数を評価する ACPI コントロール メソッドを指定した PEP_ACPI_EVALUATE_CONTROL_METHOD 構造体へのポインター。

PEP は、登録済みハンドラー ACPI コントロール メソッドの評価に使用されます。

Windows 電源管理フレームワーク (PoFx) では、ACPI の Windows ドライバーは、PEP によって実装される ACPI コントロール メソッドを評価する必要がある場合に、PEP にこの通知を送信します。

PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知を送信するには、PoFx は、PEP の AcceptAcpiNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD と PEP_ACPI_EVALUATE_CONTROL_METHOD 構造体へのデータ パラメーターのポイントが。

プラットフォーム デザイナーでことができます、特定の ACPI コントロール メソッドに、PEP または ACPI ファームウェアのハンドルを持つかどうか選択します。 PEP が ACPI コントロール メソッドに対する登録済みハンドラーの場合は、PoFx PEP へ PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知を送信することによって、このメソッドを評価する Windows ACPI ドライバーからの要求に応答します。

デバイスの PEP を処理できる ACPI コントロール メソッドの例の一覧を次には。

デバイスの識別と構成: _HID、_CID、_UID、_ADR、_CLS、_SUB、_CRS、_PRS、これにします。 デバイスの電源管理とウェイク アップ: _PS0 _PS3、_PR0 _PR3 や _DSW を経由します。 デバイス固有のメソッド: _DSM とデバイスのスタックの特定方法を制御します。 ACPI 時間とアラームのデバイスなどの特殊なデバイスには、この通知を使用して、時間とアラームのメソッド (_GCP、_GRT、_SRT、およびなど) を評価します。 

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_EVALUATE_CONTROL_METHOD 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpiquerydevicecontrolresources"></a>PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 

通知:PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 値。

データ:電源のリソースの一覧を含む PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 構造体へのポインター。
 
デバイスの電源を制御するために必要な生のリソースの一覧については、PEP を照会します。

この通知に応答してでは、PEP は、デバイスの電源を制御するために必要な生のリソースの一覧を提供します。 ように、デバイスに必要な電源リソースを予約し、PEP を (PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知を送信する) で、対応する翻訳済みのリソースの一覧を指定することができます、ACPI の Windows ドライバーはこの一覧が必要です. 詳細については、Raw と変換のリソースを参照してください。

PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知を送信するには、Windows 電源管理フレームワーク (PoFx) は、PEP の AcceptAcpiNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES と PEP_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 構造体へのデータ パラメーターのポイントが。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpitranslateddevicecontrolresources"></a>PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 

通知:PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 値。

データ:変換されたリソースの一覧を含む PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 構造体へのポインター。
 
変換されたリソースの一覧ではデバイスに必要なすべての電源制御リソース、PEP を提供します。

Windows の電源管理フレームワーク (PoFx) は、PEP には、前の PEP_NOTIFY_ACPI_QUERY_DEVICE_CONTROL_RESOURCES 通知に対する応答の生リソースが表示されている場合、この通知を送信します。 PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知は、対応する翻訳済みのリソースの一覧で、PEP を提供します。 詳細については、Raw と変換のリソースを参照してください。

PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知を送信するには、PoFx は、PEP の AcceptAcpiNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES と PEP_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 構造体へのデータ パラメーターのポイントが。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_TRANSLATED_DEVICE_CONTROL_RESOURCES 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepnotifyacpiwork"></a>PEP_NOTIFY_ACPI_WORK 

通知:PEP_NOTIFY_ACPI_WORK 値。

データ:PEP_WORK 構造体へのポインター。
 
毎回、PEP は、Windows 電源管理フレームワーク (PoFx) から作業項目を要求する RequestWorker ルーチンを呼び出すと、PEP に送信されます。 この通知は、ACPI のみの作業に使用されます。

PEP では、作業項目を要求する RequestWorker ルーチンを呼び出してから PoFx は PEP PEP_NOTIFY_ACPI_WORK の通知を送信して応答します。 ただし、作業項目の処理に必要なリソース (つまり、ワーカー スレッド) が使用可能になるまで、この通知は送信されません。 この方法で PoFx PEP に PoFx 通知中に渡す作業要求がリソースが不足していることはありませんによって失敗することができることが保証されます。

項目で、PEP は PEP_WORK 構造体は初期化されていないと想定されます。 この通知を処理するために、PEP は、要求されている作業を記述する PEP に割り当てられた PEP_WORK_INFORMATION 構造体を指す WorkInformation メンバーを設定する必要があります。 さらに、PEP では、PEP が PEP_NOTIFY_ACPI_WORK 通知を処理して、WorkInformation メンバーが有効な PEP_WORK_INFORMATION 構造体を指すことを確認する場合は TRUE を NeedWork、PEP_WORK 構造体のメンバーを設定する必要があります。 PEP では、通知を処理するために障害が発生したり、PEP_WORK_INFORMATION 構造を割り当てることがない、PEP は WorkInformation メンバーを NULL に設定し、NeedWork メンバーを FALSE に設定する必要があります。

AcceptAcpiNotification ルーチンに常に IRQL でと呼ばれる PEP_NOTIFY_ACPI_WORK 通知、PASSIVE_LEVEL を = です。
 


