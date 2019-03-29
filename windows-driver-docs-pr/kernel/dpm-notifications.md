---
title: デバイス電源管理 (DPM) の通知
description: 、通知の種類を示す通知パラメーターと共にが各デバイスの電源 (DPM) 管理通知、PEP の AcceptDeviceNotification コールバック ルーチンを受信して、データを指すデータ パラメーター構造体指定した通知の種類の情報が含まれています。
ms.assetid: 47B487A3-2707-4B0F-BD61-8C4A89F99AE1
keywords:
- AcceptDeviceNotification
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 984444958b8a4ae24edcfa04188933fe7aefc204
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581141"
---
# <a name="device-power-management-dpm-notifications"></a>デバイス電源管理 (DPM) の通知

、通知の種類を示す通知パラメーターと共にが各デバイスの電源 (DPM) 管理通知、PEP の AcceptDeviceNotification コールバック ルーチンを受信して、データを指すデータ パラメーター構造体指定した通知の種類の情報が含まれています。

この呼び出しでは、通知のパラメーターは、通知の種類を示す PEP_DPM_XXX 定数値に設定されます。 データのパラメーターは、この通知の種類に関連付けられている PEP_XXX 構造体型を指します。

次の DPM 通知 Id は、AcceptDeviceNotification コールバック ルーチンで使用されます。

## <a name="pepdpmpreparedevice"></a>PEP_DPM_PREPARE_DEVICE 

通知 PEP_DPM_PREPARE_DEVICE 値。

データ。 PEP_PREPARE_DEVICE 構造へのポインター。
通知、D0 で動作するデバイスの構成に指定されたデバイスを所有している PEP (操作) デバイスの電源の状態。

Windows 電源管理フレームワーク (PoFx) は、デバイスのドライバー スタックは、オペレーティング システムを初めて開始する前に、PEP にこの通知を送信します。 この通知により、外部電源またはデバイスの動作に必要なクロック リソースを有効にする PEP です。

PEP_DPM_PREPARE_DEVICE 通知を送信するのには、オペレーティング システムは、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_PREPARE_DEVICE と PEP_PREPARE_DEVICE 構造体へのデータ パラメーターのポイントが。 項目で、この構造体の DeviceId メンバーは、デバイスを一意に識別するデバイスの識別文字列です。 、戻る前に、PEP は、デバイスが所有していないことを示す true または FALSE に、デバイスの所有権の要求の場合、この構造の DeviceAccepted メンバーを設定します。

デバイスの電源管理を所有している PEP は、デバイスの外部にあるし、デバイスの動作に必要な電源とクロックのリソースを管理する責任を負います。 この PEP は、クロック信号と PEP_DPM_PREPARE_DEVICE 通知への応答でデバイスの電源を可能にし、PEP_DPM_ABANDON_DEVICE 通知に対する応答内のデバイスからクロック信号と能力を削除します。

次の表は、このオペレーティング システムは、PEP を PEP_DPM_PREPARE_DEVICE 通知を送信すると有効になっている前提条件と、PEP は、所有するデバイスには、この通知を処理した後に有効にする必要がある事後条件を示します。


前提条件が、デバイスは、任意の電源状態であることができます。 事後条件、PEP は、デバイス、デバイス、およびそのすべてのコンポーネントの所有権を要求する場合をオンにする必要があり、デバイスに時計が ungated する必要があります。 PEP では、これらのデバイスの PEP の所有者を検索する電源マネージャーととして複数のデバイスの PEP_DPM_PREPARE_DEVICE 通知を受信できます。 PEP は、PEP_PREPARE_DEVICE 構造体の DeviceAccepted メンバーを PEP を所有していないすべてのデバイスの場合は FALSE に設定する必要があります。

中核となるデバイスの場合は、PEP_DPM_PREPARE_DEVICE 通知は送信されません。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_PREPARE_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmabandondevice"></a>PEP_DPM_ABANDON_DEVICE 
通知 PEP_DPM_ABANDON_DEVICE 値。

データ。 PEP_ABANDON_DEVICE 構造へのポインター。
指定したデバイスが不要になったオペレーティング システムによって使用されていることを PEP に指示します。

Windows 電源管理フレームワーク (PoFx) では、オペレーティング システム、デバイスのドライバー スタックから削除した後に、PEP にこの通知を送信します。 この通知は、PEP、外部電源または将来の意思決定プロセスからこのデバイスを削除して、デバイスの動作に使用される時計のリソースを無効にできます。 場合は、デバイスは、後でもう一度開始する必要があります、PEP はまず PEP_DPM_PREPARE_DEVICE 通知を受け取ります。

PEP_DPM_ABANDON_DEVICE 通知を送信するのには、オペレーティング システムは、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_ABANDON_DEVICE と PEP_ABANDON_DEVICE 構造体へのデータ パラメーターのポイントが。 項目で、この構造体の DeviceId メンバーは、デバイスを一意に識別するデバイスの識別文字列です。 、戻る前に、PEP は、デバイスが所有していないことを示す true または FALSE に、デバイスの所有権の要求の場合、この構造の DeviceAccepted メンバーを設定します。

デバイスの電源管理を所有している PEP は、デバイスの外部にあるし、デバイスの動作に必要な電源とクロックのリソースを管理する責任を負います。

次の表は、このオペレーティング システムは、PEP を PEP_DPM_ABANDON_DEVICE 通知を送信すると有効になっている前提条件と、PEP は、所有するデバイスには、この通知を処理した後に有効にする必要がある事後条件を示します。


前提条件、PEP では、デバイスとデバイスの所有権が受け入れられた PEP_DPM_PREPARE_DEVICE 通知を受信したが。 場合は、PEP のため、デバイスの PEP_DPM_REGISTER_DEVICE 通知を受信した、デバイスの登録を受け入れ、PEP_DPM_UNREGISTER_DEVICE 通知デバイスを後で受信しました。 事後条件の PEP_DPM_PREPARE_DEVICE 通知に対する応答で割り当てられたすべてのリソースを解放する必要があります。 AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_PREPARE_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmregisterdevice"></a>PEP_DPM_REGISTER_DEVICE 
通知 PEP_DPM_REGISTER_DEVICE 値。

データ。 PEP_REGISTER_DEVICE_V2 構造へのポインター。
指定したデバイスのドライバー スタックは、Windows 電源管理フレームワーク (PoFx) に登録されている PEP に指示します。

PoFx は、デバイスのドライバー スタックは、デバイスを登録する PoFxRegisterDevice ルーチンを呼び出すときに、この通知を送信します。 この通知により、デバイスの登録情報を後で参照、PEP の内部ストレージにコピーする PEP です。

PEP_DPM_REGISTER_DEVICE 通知を送信するのには、オペレーティング システムは、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_REGISTER_DEVICE、およびデバイスのカーネル ハンドルとその他の登録情報を含む PEP_REGISTER_DEVICE_V2 構造をデータ パラメーターのポイントが。 項目で、この構造体の DeviceId メンバーは、デバイスを一意に識別するデバイスの識別文字列です。 、戻る前に、PEP は、デバイスが所有していないことを示す true または FALSE に、デバイスの所有権の要求の場合、この構造の DeviceAccepted メンバーを設定します。 この構造体の他のメンバーについては、PEP_REGISTER_DEVICE_V2 を参照してください。

次の表は、このオペレーティング システムは、PEP を PEP_DPM_REGISTER_DEVICE 通知を送信すると有効になっている前提条件と、PEP は、所有するデバイスには、この通知を処理した後に有効にする必要がある事後条件を示します。

条件の種類の説明の前提条件、PEP が、所有するデバイスの PEP_DPM_PREPARE_DEVICE 通知を受信しました。 事後条件、PEP このデバイスに関連付けられているその他のデバイスの電源 (DPM) 管理通知を受信する準備ができました。 

 

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_REGISTER_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmunregisterdevice"></a>PEP_DPM_UNREGISTER_DEVICE 
通知 PEP_DPM_UNREGISTER_DEVICE 値。

データ。 PEP_UNREGISTER_DEVICE 構造へのポインター。
デバイスのドライバー スタックが、Windows 電源管理フレームワーク (PoFx) からの登録を引き出すこと、指定されたデバイスを所有している PEP に指示します。

PoFx は、前の PEP_DPM_REGISTER_DEVICE 通知中に、デバイス、PEP に格納されている任意の登録情報が無効になっている PEP に通知するには、この通知を送信します。 応答として、PEP はこのデバイスの電源管理に使用される、内部状態をクリーンアップできます。

PEP_DPM_UNREGISTER_DEVICE 通知を送信するのには、オペレーティング システムは、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_UNREGISTER_DEVICE と PEP_UNREGISTER_DEVICE 構造体へのデータ パラメーターのポイントが。 この構造体には、PEP は、デバイスの以前の PEP_DPM_REGISTER_DEVICE 通知に対する応答で作成されたハンドルが含まれています。

次の表は、このオペレーティング システムは、PEP を PEP_DPM_UNREGISTER_DEVICE 通知を送信すると有効になっている前提条件と、PEP は、所有するデバイスには、この通知を処理した後に有効にする必要がある事後条件を示します。


PEP がデバイスの PEP_DPM_REGISTER_DEVICE 通知を受信したし、デバイスの登録を受け入れる場合に前提条件です。 PEP では、このデバイスに関連付けられているデバイスの電源管理 (DPM) 通知を受信できます。 PEP では、このデバイスに関連付けられた「職場」を報告できます。 事後条件、PEP は PEP_DPM_ABANDON_DEVICE を除き、このデバイスに関連付けられているデバイスの電源 (DPM) 管理通知を受信できなくなります。 PEP では、このデバイスに関連付けられた「職場」を報告できません。 AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_UNREGISTER_DEVICE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmdevicepowerstate"></a>PEP_DPM_DEVICE_POWER_STATE 
通知 PEP_DPM_DEVICE_POWER_STATE 値。

データ。 PEP_DEVICE_POWER_STATE 構造へのポインター。
送信 PEP へたびに、デバイスのドライバー スタックが新しい Dx 電源の状態では、変更を要求するかまたは以前要求した Dx 電源の状態に遷移が完了するとします。

PEP では、作業項目を要求する RequestWorker ルーチンを呼び出してから PoFx は PEP PEP_DPM_DEVICE_POWER_STATE の通知を送信して応答します。 ただし、作業項目の処理に必要なリソース (つまり、ワーカー スレッド) が使用可能になるまで、この通知は送信されません。 この方法で PoFx PEP に PoFx 通知中に渡す作業要求がリソースが不足していることはありませんによって失敗することができることが保証されます。

PEP_DPM_DEVICE_POWER_STATE 通知を送信するのには、オペレーティング システムは、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_DEVICE_POWER_STATE と PEP_DEVICE_POWER_STATE 構造体へのデータ パラメーターのポイントが。 PEP は、エントリに、この構造体の内容が初期化されていないが想定してください。 この通知を処理するために、PEP は、要求されている作業を記述する PEP に割り当てられた PEP_WORK_INFORMATION 構造体を指す WorkInformation メンバーを設定する必要があります。 さらに、PEP では、PEP が PEP_DEVICE_POWER_STATE 通知を処理して、WorkInformation メンバーが有効な PEP_WORK_INFORMATION 構造体を指すことを確認する場合は TRUE を NeedWork、PEP_WORK 構造体のメンバーを設定する必要があります。 PEP では、通知を処理するために障害が発生したり、PEP_WORK_INFORMATION 構造を割り当てることがない、PEP は WorkInformation メンバーを NULL に設定し、NeedWork メンバーを FALSE に設定する必要があります。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_DEVICE_POWER_STATE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmcomponentactive"></a>PEP_DPM_COMPONENT_ACTIVE 
通知 PEP_DPM_COMPONENT_ACTIVE 値。

コンポーネントを識別する PEP_COMPONENT_ACTIVE 構造体へのデータ。 ポインターは、アクティブな状態またはアイドル状態に、このコンポーネントは遷移を行っているかどうかを示します。
コンポーネントがアイドル状態からアクティブの状態に移行する必要がある、PEP の通知またはその逆です。

Windows の電源管理フレームワーク (PoFx) は、保留中のアクティブな状態かアイドル状態に遷移は、ときに、この通知を送信します。 

PEP_DPM_COMPONENT_ACTIVE 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_COMPONENT_ACTIVE と PEP_COMPONENT_ACTIVE 構造体へのデータ パラメーターのポイントが。

アクティブな状態でアクセス可能なコンポーネントとは。 アイドル状態でアクセスできるコンポーネントとは。 アクティブな状態であるコンポーネントは、F0 コンポーネントの電源状態では常にします。 コンポーネントでは、アイドル状態になるまで F0 のままにすることはできません。 アイドル状態にあるコンポーネントには、F0 または低電力状態に [fx] があります。 コンポーネントのアクティブ/アイドル条件は、コンポーネントがアクセスできるかどうかを判断するためのドライバーの唯一の確実な手段です。 低電力状態に [fx] に切り替えよう F0 でもがアイドル状態になってもコンポーネントがあります。

アクティブなコンポーネントのアイドル状態の条件を入力する準備ができたら、切り替えはすぐに発生します。 PEP_DPM_COMPONENT_ACTIVE 通知の処理中には、コンポーネントの低電力 [fx] 状態に F0 からの移行を PEP がなど要求場合があります。

コンポーネントが低電力状態に [fx] の場合、PEP_DPM_COMPONENT_ACTIVE 通知がアイドル状態からアクティブな状態に遷移を要求したときに、PEP する必要があります最初、コンポーネントに切り替える F0 前に、コンポーネントは、アクティブな条件を入力できます。 PEP は PEP_DPM_COMPONENT_ACTIVE 通知 AcceptDeviceNotification コールバックから戻った後、非同期的にアクティブな状態に遷移のコンポーネントの準備が完了する必要があります。 コンポーネントがアクティブな状態で動作する構成が完了したら、PEP する必要があります RequestWorker ルーチンを呼び出すし、作業の種類別に設定して、結果として得られる PEP_DPM_WORK 通知を処理 PEP_WORK_INFORMATION 構造で PepWorkActiveComplete を = です。

PEP では、F0 にあり、既に完全にアクティブな状態で動作するように構成するコンポーネントの PEP_DPM_COMPONENT_ACTIVE 通知を受け取り、PEP この通知を同期的に処理を完了できず場合があります。 通知の処理を「高速パス」がサポートされている場合この通知の PEP_COMPONENT_ACTIVE 構造体の WorkInformation メンバー PEP_WORK_INFORMATION 構造体へのポインターを格納して、PEP は、この構造体への作業の種類別のメンバーを設定できます。PepWorkActiveComplete 切り替えを完了します。 ただし場合、WorkInformation = null の場合、なしの「高速パス」が使用し、前の段落で説明したように、PEP は呼び出し元の RequestWorker によって非同期的の切り替えを完了する必要があります。

アクティブでアイドル状態の条件の詳細については、コンポーネント レベルの電源管理を参照してください。

AcceptDeviceNotification ルーチンは IRQL でと呼ばれます PEP_DPM_COMPONENT_ACTIVE 通知では、< = DISPATCH_LEVEL します。
 
## <a name="pepdpmwork"></a>PEP_DPM_WORK 
通知 PEP_DPM_WORK 値。

データ。 PEP_WORK 構造へのポインター。
毎回、PEP は、Windows 電源管理フレームワーク (PoFx) から作業項目を要求する RequestWorker ルーチンを呼び出すと、PEP に送信されます。

PEP では、作業項目を要求する RequestWorker ルーチンを呼び出してから PoFx は PEP PEP_DPM_WORK の通知を送信して応答します。 ただし、作業項目の処理に必要なリソース (つまり、ワーカー スレッド) が使用可能になるまで、この通知は送信されません。 この方法で PoFx PEP に PoFx 通知中に渡す作業要求がリソースが不足していることはありませんによって失敗することができることが保証されます。

PEP_DPM_WORK 通知を送信するのには、オペレーティング システムは、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_WORK と PEP_WORK 構造体へのデータ パラメーターのポイントが。 PEP は、エントリに、この構造体の内容が初期化されていないが想定してください。 この通知を処理するために、PEP は、要求されている作業を記述する PEP に割り当てられた PEP_WORK_INFORMATION 構造体を指す WorkInformation メンバーを設定する必要があります。 さらに、PEP では、PEP が PEP_DPM_WORK 通知を処理して、WorkInformation メンバーが有効な PEP_WORK_INFORMATION 構造体を指すことを確認する場合は TRUE を NeedWork、PEP_WORK 構造体のメンバーを設定する必要があります。 PEP では、通知を処理するために障害が発生したり、PEP_WORK_INFORMATION 構造を割り当てることがない、PEP は WorkInformation メンバーを NULL に設定し、NeedWork メンバーを FALSE に設定する必要があります。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_WORK 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmpowercontrolrequest"></a>PEP_DPM_POWER_CONTROL_REQUEST 
通知 PEP_DPM_POWER_CONTROL_REQUEST 値。

データ。 PEP_POWER_CONTROL_REQUEST 構造へのポインター。
ドライバーには、PEP を直接制御コードを送信する PoFxPowerControl API が呼び出されて、PEP を通知します。

Windows 電源管理フレームワーク (PoFx) では、ドライバーは、PEP を直接制御コードを送信する PoFxPowerControl API を呼び出す場合に、PEP にこの通知を送信します。 この場合、通知データ ポインターは PEP_POWER_CONTROL_REQUEST 構造体を指します。 

電源管理の要求とその意味は、PEP ライターとデバイスのクラス所有者の間に定義されます。 通常、このようなインターフェイスは、汎用化された電源管理フレームワークでキャプチャされていないデバイス クラスの特定通信です。 たとえば、UART コント ローラーは、いくつかのプラットフォームのクロックの rails を変更する PEP にボー レート情報を通信可能性があります/区分線と、このような通信は電源制御要求を利用して可能性があります。 

注、PEP は PEP_DPM_DEVICE_STARTED 通知または PEP_DPM_POWER_CONTROL_REQUEST 通知を受信した後、制御コードをデバイスに送信する要求のみできます。
 

AcceptDeviceNotification ルーチンは IRQL でと呼ばれます PEP_DPM_POWER_CONTROL_REQUEST 通知では、< = DISPATCH_LEVEL します。
 
## <a name="pepdpmpowercontrolcomplete"></a>PEP_DPM_POWER_CONTROL_COMPLETE 
通知 PEP_DPM_POWER_CONTROL_COMPLETE 値。

データ。 PEP_POWER_CONTROL_COMPLETE 構造へのポインター。
ドライバーが、PEP で以前発行された電源制御要求を完了したこと、PEP の通知します。

Windows 電源管理フレームワーク (PoFx) は、ドライバー、PEP によって以前に発行された電源制御要求の完了時に、PEP にこの通知を送信します。 

注、PEP は、電源制御要求を発行しない場合、この通知を無視できます。
 
AcceptDeviceNotification ルーチンは IRQL でと呼ばれます PEP_DPM_POWER_CONTROL_COMPLETE 通知では、< = DISPATCH_LEVEL します。
 
## <a name="pepdpmsystemlatencyupdate"></a>PEP_DPM_SYSTEM_LATENCY_UPDATE 
通知 PEP_DPM_SYSTEM_LATENCY_UPDATE 値。

データ。 PEP_SYSTEM_LATENCY 構造へのポインター。
PEP に、OS が、システム全体の待機時間の許容範囲を更新することを通知します。

Windows の電源管理フレームワーク (PoFx) は、OS は、全体的なシステムの待機時間の許容範囲を更新するときに、この通知を送信します。 

PoFx の以前のバージョンでは、この通知はプロセッサとプラットフォームのアイドル状態の選択、PEP によって使用されました。 最新の PEP インターフェイスを持つ選択プロセスが OS によって処理全体とそのためこの通知は役に立たなくなった。 ここでは含まれる、完全を期すためと、PEP で無視する必要があります。 

PEP_DPM_SYSTEM_LATENCY_UPDATE 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 IRQL で AcceptDeviceNotification ルーチンを呼び出すこの通知では、< = DISPATCH_LEVEL します。
 
## <a name="pepdpmdevicestarted"></a>PEP_DPM_DEVICE_STARTED 
通知 PEP_DPM_DEVICE_STARTED 値。

データ。 PEP_DEVICE_STARTED 構造へのポインター。
PEP に power control のトランザクションの受信に使用できるように、デバイスが開始されたことを通知します。

デバイス スタックは、2 段階のプロセスで実行時の電源管理 OS を登録します。 ドライバーは、コンポーネント、アイドル状態および対応する属性の数に関する情報を提供する PoFxRegisterDevice 最初を呼び出します。 この呼び出しに応答してでは、PEP は PEP_DPM_REGISTER_DEVICE 通知を受け取ります。 

登録が成功すると、ドライバー、(つまりセット アクティブ、更新の待機時間の要件、アイドル状態の保存場所の更新が必要ですなど) は、そのコンポーネントを初期化できるようになります。 ドライバーの初期化タスクが完了すると、PoFxStartDevicePowerManagement を呼び出すことによって電源マネージャーを通知します。 PEP では、応答で PEP_DPM_DEVICE_STARTED 通知が表示されます。 この時点では、デバイスは、実行時の電源管理を完全に有効にすると見なされます。 

結果として、か、最初に受信した PEP_DPM_DEVICE_STARTED 通知または PEP_DPM_POWER_CONTROL_REQUEST 通知しない限りに、PEP は電源制御要求をドライバーに発行できません。 

注、PEP は、電源制御要求を発行しない場合、この通知を無視できます。
 
AcceptDeviceNotification ルーチンは IRQL でと呼ばれます PEP_DPM_DEVICE_STARTED 通知では、< = DISPATCH_LEVEL します。
 
## <a name="pepdpmnotifycomponentidlestate"></a>PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 
通知 PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 値。

データ。 PEP_NOTIFY_COMPONENT_IDLE_STATE 構造へのポインター。
OS は、特定のコンポーネントに、アイドル状態の移行を発行するときに、PEP に送信されます。 

Windows の電源管理フレームワーク (PoFx) は、OS は、特定のコンポーネントに、アイドル状態の移行を発行すると、この通知を送信します。


重要な PEP では、この通知を処理する必要があります。
 

アイドル状態の遷移ごとに、PEP は、ドライバーに通知された前後に通知されます。 PEP は、PEP_NOTIFY_COMPONENT_IDLE_STATE 構造体の DriverNotified メンバーを調べることで、事前/事後の通知を区別します。 後の通知、DriverNotified メンバーは TRUE になります。

前の通知は F0 に遷移するときに通常使用されます。 この場合、PEP では、ハードウェアが使用可能なドライバーは、F0 通知を処理するときに、クロックまたは電源のリソースを再度有効にする必要があります。 したがって、F0 からより深いアイドル状態に遷移するときに後の通知が通常使用されます。 ドライバーは、アイドル状態の通知を処理した後、PEP がリソースのクロックと電源オフに安全にできます。 

特定のコンポーネントに、アイドル状態の移行を処理するには、非同期処理、操作にかなりの時間または IRQL がかかる場合が多すぎます切り替えを同期的に完了する必要があります。 その結果、PEP して完了できますこの通知同期または非同期で完了メンバーを TRUE または FALSE に設定すると、それぞれします。 

通知を非同期的に完了する場合は、PEP には、作業者を要求することによって完了時に、OS を通知 (RequestWorker を参照してください) の作業の種類を使用して、結果として得られる PEP_DPM_WORK 通知で指定された作業情報の構造情報を入力し、PepWorkCompleteIdleState します。 

PEP_DPM_NOTIFY_COMPONENT_IDLE_STATE 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 このルーチンは IRQL で呼び出されます < = DISPATCH_LEVEL します。
 
## <a name="pepdpmregisterdebugger"></a>PEP_DPM_REGISTER_DEBUGGER 
通知 PEP_DPM_REGISTER_DEBUGGER 値。

データ。 PEP_REGISTER_DEBUGGER 構造へのポインター。
登録済みデバイスは、デバッグ ポートとして使用可能性があります、PEP を通知します。

Windows の電源管理フレームワーク (PoFx) は、PEP デバッグ ポートとして登録されたデバイスを使用することがあることを通知するには、この通知を送信します。 

AcceptDeviceNotification ルーチンは IRQL でと呼ばれます PEP_DPM_REGISTER_DEBUGGER 通知では、< = DISPATCH_LEVEL します。
 
## <a name="pepdpmregistercrashdumpdevice"></a>PEP_DPM_REGISTER_CRASHDUMP_DEVICE 
通知 PEP_DPM_REGISTER_CRASHDUMP_DEVICE 値。

データ。 PEP_REGISTER_CRASHDUMP_DEVICE 構造へのポインター。
Windows の電源管理フレームワーク (PoFx) は、クラッシュ ダンプのハンドラーとしてデバイスの登録時に、この通知を送信します。

致命的なエラーが生じた場合に、メモリ ダンプ (クラッシュ ダンプ) を生成する機能が、クラッシュの原因を特定するのには欠かせません。 Windows、既定ではクラッシュ ダンプを生成、システムでバグチェックを検出したとき。 このコンテキストでは、システムは、割り込みを無効になっているとシステムで HIGH_LEVEL IRQL を非常に制約付きの運用環境下です。

関連するデバイス ディスク (記憶域コント ローラー、コント ローラーの PCI など) へのクラッシュ ダンプの書き込みがの電源を切断、クラッシュの時点で、OS がデバイスの電源を PEP に呼び出す必要があります。 そのため、OS は、クラッシュ ダンプのスタック上のすべてのデバイスに対して PEP からコールバック (PowerOnDumpDeviceCallback) を要求し、ダンプ ファイルを生成するときにコールバックを呼び出します。 

制約のある環境を指定すると、クラッシュ時に、PEP によって提供されるコールバックする必要がありますいないコード ページにアクセス、ブロック、イベントのまたは同じ処理を行うことがあるすべてのコードを呼び出します。 さらに、必要なリソースの電源を投入するプロセスは、割り込みを使用できません。 その結果、PEP では、ポーリングする必要がありますには、有効にするさまざまなリソースを待機する必要があります元に戻す必要があります。 PEP は、これらの制約の下で、デバイスの電源ことはできない場合、は、通知を処理しないか、または、コールバック ルーチンを指定しないにする必要があります。 

PEP_DPM_REGISTER_CRASHDUMP_DEVICE 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 IRQL でこの通知で AcceptDeviceNotification ルーチンと呼ばれる < HIGH_LEVEL を = です。
 
## <a name="pepdpmdeviceidleconstraints"></a>PEP_DPM_DEVICE_IDLE_CONSTRAINTS 
通知 PEP_DPM_DEVICE_IDLE_CONSTRAINTS 値。

データ。 PEP_DEVICE_PLATFORM_CONSTRAINTS 構造へのポインター。
D 状態のデバイスとプラットフォームのアイドル状態の間の依存関係のクエリに PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、D 状態のデバイスとプラットフォームのアイドル状態の間の依存関係を照会する PEP にこの通知を送信します。 PEP では、この通知を使用して、最も明るい D 状態機器がまだにして各プラットフォームのアイドル状態を返します。 OS は、関連付けられているプラットフォームのアイドル状態に入る前に、デバイスが最小の D 状態が維持されます。 プラットフォームのアイドル状態が、このデバイスの D 状態になることに依存しない、PEP は PowerDeviceD0 の最小 D 状態を指定する必要があります。 このデバイスは特定の D 状態でプラットフォームのアイドル状態が依存していない場合は、この通知を無視できます。 

この通知は、PEP の PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知が受信した後、各デバイスに送信されます。 

PEP_DPM_DEVICE_IDLE_CONSTRAINTS 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_DEVICE_IDLE_CONSTRAINTS と PEP_DEVICE_PLATFORM_CONSTRAINTS 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる、PEP_DPM_DEVICE_IDLE_CONSTRAINTS 通知 DISPATCH_LEVEL を = です。
 
## <a name="pepdpmcomponentidleconstraints"></a>PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 
通知 PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 値。

データ。 PEP_COMPONENT_PLATFORM_CONSTRAINTS 構造へのポインター。
F 状態のコンポーネントとプラットフォームのアイドル状態の間の依存関係のクエリに PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) は、F 状態のコンポーネントとプラットフォームのアイドル状態の間の依存関係を照会する PEP にこの通知を送信します。 PEP では、この通知を使用して、最も明るい F 状態コンポーネントことができますもに、各プラットフォームのアイドル状態を返します。 OS は、コンポーネントが関連付けられているプラットフォームのアイドル状態に入る前に、最小の F 状態が維持されます。 プラットフォームのアイドル状態が、このコンポーネントが、F 状態になることに依存しない、PEP は 0 の最小 F 状態を指定する必要があります。 このコンポーネントが特定の F 状態でないアイドル状態のプラットフォームは依存している場合は、この通知を無視できます。 

D0 よりも深くのデバイスのアイドル状態制約とは、デバイス上のコンポーネントのアイドル状態のコンポーネントよりも詳細に制限します。 特定のプラットフォーム アイドル状態インデックスの場合、デバイスには、デバイスのアイドル状態制約が指定されている場合、デバイスに関連付けられたすべてのコンポーネントの対応するコンポーネントのアイドル状態制約は無視されます。 

この通知は、PEP は PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知を受信した後、各デバイスで各コンポーネントに送信されます。 

PEP_DPM_COMPONENT_IDLE_CONSTRAINTS 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 AcceptDeviceNotification ルーチンは IRQL で常に呼び出されます = DISPATCH_LEVEL します。
 
## <a name="pepdpmquerycomponentperfcapabilities"></a>PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 
通知 PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 値。

データ。 PEP_QUERY_COMPONENT_PERF_CAPABILITIES 構造へのポインター。
PEP コンポーネントに対して定義されているパフォーマンスの状態 (P 状態) のセットの数を照会していることを通知します。

PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES と PEP_QUERY_COMPONENT_PERF_CAPABILITIES 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_QUERY_COMPONENT_PERF_CAPABILITIES 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmquerycomponentperfset"></a>PEP_DPM_QUERY_COMPONENT_PERF_SET 
通知 PEP_DPM_QUERY_COMPONENT_PERF_SET 値。

データ。 PEP_QUERY_COMPONENT_PERF_SET 構造へのポインター。
コンポーネントのパフォーマンスの状態値 (P 状態セット) のセットに関する情報を照会していることを PEP に通知します。

PEP_DPM_QUERY_COMPONENT_PERF_SET 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_QUERY_COMPONENT_PERF_SET と PEP_QUERY_COMPONENT_PERF_SET 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_QUERY_COMPONENT_PERF_SET 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmquerycomponentperfsetname"></a>PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 
通知 PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 値。

データ。 PEP_QUERY_COMPONENT_PERF_SET_NAME 構造へのポインター。
コンポーネントのパフォーマンスの状態値 (P 状態セット) のセットに関する情報を照会していることを PEP に通知します。

PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME と PEP_QUERY_COMPONENT_PERF_SET_NAME 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_QUERY_COMPONENT_PERF_SET_NAME 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmquerycomponentperfstates"></a>PEP_DPM_QUERY_COMPONENT_PERF_STATES 
通知 PEP_DPM_QUERY_COMPONENT_PERF_STATES 値。

データ。 PEP_QUERY_COMPONENT_PERF_STATES 構造へのポインター。
PEP P 状態の指定されたセットの個別のパフォーマンスの状態 (P 状態) の値の一覧の照会されることを通知します。

PEP_DPM_QUERY_COMPONENT_PERF_STATES 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_QUERY_COMPONENT_PERF_STATES と PEP_QUERY_COMPONENT_PERF_STATES 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_QUERY_COMPONENT_PERF_STATES 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmregistercomponentperfstates"></a>PEP_DPM_REGISTER_COMPONENT_PERF_STATES 
通知 PEP_DPM_REGISTER_COMPONENT_PERF_STATES 値。

データ。 PEP_REGISTER_COMPONENT_PERF_STATES 構造へのポインター。
指定したコンポーネントのパフォーマンス状態 (P 状態)、PEP を通知します。

PEP_DPM_REGISTER_COMPONENT_PERF_STATES 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_REGISTER_COMPONENT_PERF_STATES と PEP_REGISTER_COMPONENT_PERF_STATES 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_REGISTER_COMPONENT_PERF_STATES 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmrequestcomponentperfstate"></a>PEP_DPM_REQUEST_COMPONENT_PERF_STATE 
通知 PEP_DPM_REQUEST_COMPONENT_PERF_STATE 値。

データ。 PEP_REQUEST_COMPONENT_PERF_STATE 構造へのポインター。
1 つまたは複数のパフォーマンスの状態 (P 状態) の変更が、Windows 電源管理フレームワーク (PoFx) によって要求されたことを PEP に通知します。

PEP_DPM_REQUEST_COMPONENT_PERF_STATE 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_REQUEST_COMPONENT_PERF_STATE と PEP_REQUEST_COMPONENT_PERF_STATE 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_REQUEST_COMPONENT_PERF_STATE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmquerycurrentcomponentperfstate"></a>PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 
通知 PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 値。

データ。 PEP_QUERY_CURRENT_COMPONENT_PERF_STATE 構造へのポインター。
PEP P 状態の指定されたセット内の現在の P 状態に関する情報を照会していることを通知します。

PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 この呼び出しでは、通知のパラメーター値は、PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE と PEP_QUERY_CURRENT_COMPONENT_PERF_STATE 構造体へのデータ パラメーターのポイントが。

AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれる PEP_DPM_QUERY_CURRENT_COMPONENT_PERF_STATE 通知、PASSIVE_LEVEL を = です。
 
## <a name="pepdpmquerydebuggertransitionrequirements"></a>PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 
通知 PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 値。

データ。 PEP_DEBUGGER_TRANSITION_REQUIREMENTS 構造へのポインター。
一連のクエリを調整またはプラットフォームの状態を PEP に送信される電源がオフにデバッガーを必要とします。

Windows 電源管理フレームワーク (PoFx) は、一連のクエリに PEP にこの通知を送信調整や、電源がオフにデバッガーを必要とするプラットフォームの状態します。 この通知が受け入れられた場合は、OS は、デバッガーのすべての power デバッガーの遷移、PEP と、PEP では、電源を TransitionCriticalResource は使用が管理します。 

この通知は、PEP PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE または PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 通知を受け取った後、デバッガーの各デバイスに送信されます。 

PEP_DPM_QUERY_DEBUGGER_TRANSITION_REQUIREMENTS 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 AcceptDeviceNotification ルーチンに常に IRQL でと呼ばれるこの通知で = DISPATCH_LEVEL します。
 
## <a name="pepdpmlowpowerepoch"></a>PEP_DPM_LOW_POWER_EPOCH 
通知 PEP_DPM_LOW_POWER_EPOCH 値。

データ。 PEP_LOW_POWER_EPOCH 構造へのポインター。
この通知は非推奨とされます。 
 
## <a name="pepdpmquerysocsubsystem"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM 値。

データ。 PEP_QUERY_SOC_SUBSYSTEM 構造へのポインター。
チップ (SoC) サブシステムに特定のシステムに関する基本情報を収集するために、PEP に送信されます。

Windows 電源管理フレームワーク (PoFx) では、プラットフォームのアイドル状態が、特定の SoC サブシステムに関する基本的な情報を収集するために初期化された後に、PEP にこの通知を送信します。 SoC サブシステムのアカウンティングを実装していませんか、指定されたプラットフォームのアイドル状態には実装しない PEP では、FALSE を返します。 このプラットフォームのアイドル状態の PEP への診断の通知の送信を停止する OS に指示します。

システムの SubsystemCount とサブシステムの MetadataCount は、PEP/BSP の更新プログラムで変更できます。 SubsystemIndex は、OS が起動するたびに変更できます。 

重要な PEP は、この通知を無視することはできません。 非ゼロ SubsystemCount でこの PlatformIdleStateIndex PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知に応答があるために、PEP はこの通知を受信です。
 
PEP_DPM_QUERY_SOC_SUBSYSTEM 通知を送信するには、PoFx では、IRQL で PEP の AcceptDeviceNotification コールバック ルーチンを呼び出す < DISPATCH_LEVEL します。
 
## <a name="pepdpmquerysocsubsystemblockingtime"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 値。

データ。 PEP_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 構造へのポインター。
チップ (SoC) サブシステム上の特定のシステムの OS が時間の集計を収集するときに、PEP に送信される、OS の知識がなくても、特定のプラットフォームのアイドル状態にエントリがブロックされています。

通常、OS 呼び出して拡張のコネクテッド スタンバイ セッションの最後に、この通知、OS が指定されたプラットフォームのアイドル状態にしようとします。 PEP_QUERY_SOC_SUBSYSTEM_COUNT します。SubsystemCount 値が、入力前、PEP でサブコンポーネントの初期化中には、PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知の数は、一度に PEP に送信されますを指定します。 PEP では、指定されたサブシステムに対して複数の PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知を受信できます。 これらの通知は、PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 通知の使用はインターリーブいない可能性があります。

重要な PEP は、この通知を無視することはできません。 非ゼロ SubsystemCount でこの PlatformIdleStateIndex PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知に応答があるために、PEP はこの通知を受信です。
 
PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知を送信するには、PoFx では、IRQL で PEP の AcceptDeviceNotification コールバック ルーチンを呼び出す < DISPATCH_LEVEL します。

 
## <a name="pepdpmquerysocsubsystemcount"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 値。

データ。 PEP_QUERY_SOC_SUBSYSTEM_COUNT 構造へのポインター。
特定のプラットフォームのアイドル状態のチップ (SoC) サブシステム会計上、PEP がシステムをサポートするかどうかを OS に指示するプラットフォームのアイドル状態が初期化された後に、PEP に送信されます。 

これは、最初 SoC サブシステム診断通知 PEP に送信します。 SoC サブシステムのアカウンティングを実装していませんか、指定されたプラットフォームのアイドル状態には実装しない PEP は FALSE を返します、この場合、OS 通知は送信されません、PEP の詳細について SoC サブシステム診断このプラットフォームのアイドル状態の。


注、PEP は、指定されたプラットフォームのアイドル状態の SoC 診断通知を実装していない場合、この通知を無視できます。
 

PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知を送信するには、PoFx では、IRQL で PEP の AcceptDeviceNotification コールバック ルーチンを呼び出す < DISPATCH_LEVEL します。

 
## <a name="pepdpmquerysocsubsystemmetadata"></a>PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 
通知 PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 値。

データ。 PEP_QUERY_SOC_SUBSYSTEM_METADATA 構造へのポインター。
ブロック時間がクエリだけが行われたサブシステムに関する省略可能なメタデータを収集するために、PEP に送信されます。

この通知は通常、PEP_DPM_QUERY_SOC_SUBSYSTEM_BLOCKING_TIME 通知の直後に続く PEP に送信されます。 1 つの PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 通知は、サブシステムを記述するすべてのメタデータのキー値ペアを収集します。

重要な PEP は、この通知を無視することはできません。 非ゼロ SubsystemCount でこの PlatformIdleStateIndex PEP_DPM_QUERY_SOC_SUBSYSTEM_COUNT 通知に応答があるために、PEP はこの通知を受信です。
 
PEP_DPM_QUERY_SOC_SUBSYSTEM_METADATA 通知を送信するには、PoFx は、PEP の AcceptDeviceNotification コールバック ルーチンを呼び出します。 IRQL でこの通知で AcceptDeviceNotification ルーチンと呼ばれる < DISPATCH_LEVEL します。
 
## <a name="pepdpmresetsocsubsystemaccounting"></a>PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 
通知 PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 値。

PEP_RESET_SOC_SUBSYSTEM_ACCOUNTING 構造に A ポインターへのデータ。 ポインター。 構造体。
時間とメタデータのアカウンティングをブロックしているすべてのサブシステムをオフにして、必要に応じて、追加の初期化を実行、アカウンティングを再起動する PEP に送信されます。 

Windows の電源管理フレームワーク (PoFx) 通知を送信この PEP にいつでも OS とすべてのサブシステムが初期化された後です。 通常、この通知と呼ばれる、OS、チップ (SoC)、システムは保持する内容の周囲の分析の新しい期間の開始時に (コネクト スタンバイの入力時に DRIPS を対象とする場合)、指定されたプラットフォームのアイドル状態から。 OS には、プラットフォームのアイドル状態、PEP を 1 つまたは複数の SoC サブシステムが初期化されるは、この通知のみ送信します。

PEP_DPM_RESET_SOC_SUBSYSTEM_ACCOUNTING 通知を送信するには、PoFx では、IRQL で PEP の AcceptDeviceNotification コールバック ルーチンを呼び出す < DISPATCH_LEVEL します。
 
