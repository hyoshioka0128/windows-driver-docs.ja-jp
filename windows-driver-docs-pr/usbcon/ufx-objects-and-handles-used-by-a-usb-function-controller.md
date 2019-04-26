---
Description: USB 関数クラスの拡張機能 (UFX) は、これらの特定の USB UFX オブジェクトを定義するのに WDF オブジェクトの機能を使用します。
title: USB 機能クライアント ドライバーが使用する UFX オブジェクトとハンドル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 268d3e82963c889328671c5bcc4ab1856daad554
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355166"
---
# <a name="ufx-objects-and-handles-used-by-a-usb-function-client-driver"></a>USB 機能クライアント ドライバーが使用する UFX オブジェクトとハンドル


**要約**

-   UFX オブジェクトは、エンドポイントと転送を処理するために、関数のコント ローラー ドライバーによって使用されます。
-   これらのオブジェクトは、WDF オブジェクトへのハンドルし、クライアント ドライバーの要求で UFX によって作成されます。 各オブジェクトの有効期間は、UFX によって管理されます。

**適用対象**

-   Windows 10

**最終更新日**

-   2015 年 7 月

**重要な API**

-   [**UfxDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/mt187951)
-   [**UfxEndpointCreate**](https://msdn.microsoft.com/library/windows/hardware/mt187965)

USB 関数クラスの拡張機能 (UFX) は、これらの特定の USB UFX オブジェクトを定義するのに WDF オブジェクトの機能を使用します。

これらのオブジェクトは、WDF オブジェクトへのハンドルし、関数のクライアント ドライバーの要求で UFX によって作成されます。 必要に応じてクライアント ドライバーでは、これらのオブジェクトの作成時に渡すことができるコンテキストを関連付けることができます。 UFX によって作成されたすべての WDF オブジェクトでは、2 つのデバイス コンテキストを持つことがあります。UFX によって、オブジェクトの作成時に設定されている 1 つのデバイス コンテキストその他のデバイス コンテキストのクライアント ドライバーによって渡され、UFX でを使用して設定が[ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723) WDF オブジェクトを作成した後。

## <a name="usb-device-object"></a>USB デバイス オブジェクト


**UFXDEVICE**

コント ローラーによって作成された USB デバイスを表します。 オブジェクトは、USB プロトコルの仕様に従って USB 状態を管理して、USB デバイスに関連付けられた 1 つまたは複数のエンドポイントを管理する責任を負います。 関数のコント ローラー ドライバー内でこのオブジェクトを作成し、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバックを呼び出すことによって、 [ **UfxDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt187951)メソッド。

[*EVT\_UFX\_デバイス\_ホスト\_接続*](https://msdn.microsoft.com/library/windows/hardware/mt187852)  
ホストとの接続を開始します。

[*EVT\_UFX\_デバイス\_ホスト\_切断*](https://msdn.microsoft.com/library/windows/hardware/mt187853)  
関数のコント ローラーのホストとの通信を無効にします。

[*EVT\_UFX\_デバイス\_アドレス*](https://msdn.microsoft.com/library/windows/hardware/mt187847)  
関数のコント ローラーのアドレスが割り当てられます。

[*EVT\_UFX\_デバイス\_エンドポイント\_追加*](https://msdn.microsoft.com/library/windows/hardware/mt187851)  
既定のエンドポイントを作成します。

[*EVT\_UFX\_デバイス\_既定\_エンドポイント\_追加*](https://msdn.microsoft.com/library/windows/hardware/mt187849)  
既定のエンドポイントを作成します。

[*EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://msdn.microsoft.com/library/windows/hardware/mt187863)  
USB デバイスの状態を更新します。

[*EVT\_UFX\_デバイス\_ポート\_変更*](https://msdn.microsoft.com/library/windows/hardware/mt187854)  
USB デバイスが接続されている新しいポートの種類を更新します。

[*EVT\_UFX\_デバイス\_ポート\_検出*](https://msdn.microsoft.com/library/windows/hardware/mt187855)  
ポートの検出を開始します。

[*EVT\_UFX\_DEVICE\_REMOTE\_WAKEUP\_SIGNAL*](https://msdn.microsoft.com/library/windows/hardware/mt187859)  
関数のコント ローラーにリモート ウェイク アップを開始します。

[*EVT\_UFX\_デバイス\_検出\_機密にかかわる\_充電器*](https://msdn.microsoft.com/library/windows/hardware/mt187850)  
独自の充電器の検出を開始します。

[*EVT\_UFX\_デバイス\_機密にかかわる\_充電器\_リセット*](https://msdn.microsoft.com/library/windows/hardware/mt187857)  
独自の充電器をリセットします。

[*EVT\_UFX\_デバイス\_機密にかかわる\_充電器\_設定\_プロパティ*](https://msdn.microsoft.com/library/windows/hardware/mt187858)  
USB 経由での課金を有効にするために使用する充電器の情報を設定します。

## <a name="usb-endpoint-object"></a>USB endpoint オブジェクト


**UFXENDPOINT**

ホストとデバイスの間の論理接続を表します。 オブジェクトは、ホストからのデータの転送を担当します。 すべてのデバイス オブジェクト、1 つまたは複数のエンドポイントがあります。 既定のエンドポイントは、コントロール エンドポイントでは常に、残りの部分はクラス ドライバーの特定のオブジェクト。 関数のコント ローラー ドライバー内のオブジェクトを作成する、 [ *EVT\_UFX\_デバイス\_エンドポイント\_追加*](https://msdn.microsoft.com/library/windows/hardware/mt187851) を呼び出すことによってコールバック[ **UfxEndpointCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt187965)メソッド。

## <a name="related-topics"></a>関連トピック
[USB ファンクション コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)  



