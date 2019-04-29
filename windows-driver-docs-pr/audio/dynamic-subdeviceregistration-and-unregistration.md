---
title: 動的サブデバイスの登録と登録解除
description: 動的サブデバイスの登録と登録解除
ms.assetid: 7157b7b3-655b-49d9-be45-c4a86a3cc82d
keywords:
- 動的サブデバイス WDK オーディオ
- オーディオ サブデバイス WDK
- オーディオ サブデバイス WDK を登録します。
- オーディオ サブデバイス WDK の登録を解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09d625ee56111367272c94f0575f21bb75df7e8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333817"
---
# <a name="dynamic-subdevice-registration-and-unregistration"></a>動的サブデバイスの登録と登録解除


いくつかの形式のジャック プレゼンスの検出をサポートするデバイスには、動的なデバイスと呼ばれ、ジャックをサポートする必要があります、 [ **KSPROPERTY\_ジャック\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)プロパティ。 次の手順では、作成、登録、またはこれらの動的なデバイスに関連付けられているサブデバイスの登録を解除する動的なデバイスのドライバーによって使用されるアルゴリズムを示します。 フィルターの形式で、サブデバイスが作成されます。

次の手順では、オーディオ デバイス ドライバーが読み込まれるときに、回線のモジュラー ジャックに接続されているオーディオ デバイスがあるときの動作を示しています。

1.  ドライバーはジャック プレゼンスの検出が判断するためには、ジャックに接続されているデバイスです。 ドライバー呼び出し[ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)トポロジのフィルターを登録する[Portcls](introduction-to-port-class.md)します。 A [ **KSCATEGORY\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff548261)インターフェイスは、トポロジのフィルターの登録の結果として作成されます。

2.  オーディオ スタックの通知を受け取るときに、 **KSCATEGORY\_オーディオ**インターフェイスを作成、 [AudioEndpoint ビルダー](audio-endpoint-builder-algorithm.md)作成し関連付けられているエンドポイントを初期化し、その状態に設定アクティブです。

3.  ドライバー Portcls wave フィルターに登録して、オーディオ スタックが通知されます。

4.  ドライバー呼び出し[ **PcRegisterPhysicalConnection** ](https://msdn.microsoft.com/library/windows/hardware/ff537726)トポロジ フィルターを使用して wave フィルターを接続します。 この物理的に接続し、Portcls に登録されます。

5.  ドライバーの IsConnected メンバーの設定、 [ **KSJACK\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)構造体を**TRUE**ジャックに接続されているデバイスがあることを示します。

**注**  オーディオ デバイス ジャック プレゼンスがない場合、検出、 **IsConnected**メンバーは常にあります**TRUE**。 デバイスでジャックのプレゼンスをサポートするかどうかを確認するクライアント アプリケーションが呼び出すことができますの検出、 [IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)の JackCapabilities フラグを読み取る、 [ **KSJACK\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537138)構造体。 このフラグは、JACKDESC2 場合\_プレゼンス\_検出\_機能ビットが設定、エンドポイントがジャックのプレゼンスをサポートしていることを示します検出します。 その場合、戻り値の**IsConnected**メンバーは、ジャックのカーソルの状態を正確に反映として解釈できます。

 

次の手順では、動作について説明するかどうかは、ドライバーが読み込まれるときに、回線のモジュラー ジャックに接続されているオーディオ デバイスはありません。

1.  判断するために、ドライバーはジャック プレゼンス検出には、回線のモジュラー ジャックに接続されているデバイスはありません。 Portcls をトポロジ フィルター、jack の登録しますが、 **KSCATEGORY\_オーディオ**インターフェイスを作成します。

2.  オーディオ スタックの通知を受け取るときに、 **KSCATEGORY\_オーディオ**インターフェイスを作成します。 クエリから判断するミニポート ドライバーを AudioEndpointBuilder、 **KSJACK\_説明**プロパティ電源が入っていないエンドポイントの状態を設定するかどうか。

3.  ドライバーのセット、 **IsConnected**のメンバー、 **KSJACK\_説明**構造体を**FALSE**ジャックに接続されているデバイスがないことを示します。

オーディオのエンドポイントのさまざまな状態の詳細については、次を参照してください。[オーディオ エンドポイント ビルダー アルゴリズム](audio-endpoint-builder-algorithm.md)します。

サブデバイス登録および登録解除プロセスの前の説明に準拠するには、ジャック プレゼンスの検出をサポートするデバイス ドライバーは、挿入と削除をプラグインする応答で、次のように対応する必要があります。

**プラグインの挿入にデバイス ドライバーの応答**

1.  ドライバーを呼び出す必要があります**PcRegisterSubdevice** Portcls を wave フィルターを登録します。
    **注**   、ドライバーが既に呼び出されて**PcRegisterSubdevice**トポロジ フィルターで、回線のモジュラー ジャックに接続されているデバイス ドライバーが読み込まれたときにします。

     

2.  ドライバーを呼び出す必要があります**PcRegisterPhysicalConnection** Portcls"wave トポロジのフィルターを"接続に登録します。

3.  ドライバーを設定する必要があります、 **IsConnected**のメンバー、 **KSJACK\_説明**構造体を**TRUE**します。

**削除のプラグにデバイス ドライバーの応答**

1.  ドライバーを呼び出す必要があります[ **IUnregisterPhysicalConnection::UnregisterPhysicalConnection** ](https://msdn.microsoft.com/library/windows/hardware/ff537024) wave フィルターとトポロジのフィルター間の物理接続の登録を解除します。

2.  ドライバーを呼び出す必要があります[ **IUnregisterSubdevice::UnregisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537032) wave フィルターの登録を解除します。

3.  ドライバーを設定する必要があります、 **IsConnected**のメンバー、 **KSJACK\_説明**構造**FALSE**します。

 

 




