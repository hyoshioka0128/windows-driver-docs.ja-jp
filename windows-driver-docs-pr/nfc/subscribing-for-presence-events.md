---
title: プレゼンス イベントのサブスクライブ
description: プレゼンス イベントのサブスクライブ
ms.assetid: 4AA6C7DA-5301-4356-8AF9-5567322FAB46
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e63a19110ec5ff2a22def2f13025d115f7cc207
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373584"
---
# <a name="subscribing-for-presence-events"></a>プレゼンス イベントのサブスクライブ


プレゼンスのサブスクリプションは、ドライバー内で一意のオープン ハンドルとして表されます。 NFP プロバイダーから遷移非近接近接または近接に近接非たびにイベントは、ドライバーからスローをクライアントにします。

**注**  近接デバイスを取得する機能の削除や、2 つのデバイスが近接の両方である場合、サブスクリプションが近接デバイスから到着したこのインターフェイスを現在提供しません。

 

プレゼンスのイベントは、サブスクリプションの一般的なパスを使用して実装されます。 プロトコル"DeviceArrived"または"DeviceDeparted"を持つメッセージは、特別なサブスクリプションとして解釈する必要があります。 到着メッセージは、最初のメッセージの受信を配信する前に、すぐに配信する必要がありますメッセージ。 出発メッセージは、後のメッセージが可能な配信、最後のメッセージである必要があります。

## <a name="subscription"></a>サブスクリプション


これは、次の特定の要件を除く標準のサブスクリプションのように検索します。

近接デバイスからメッセージを受信、プロトコル フローには、近接デバイスとそのドライバーが関わります。

### <a name="required-actions"></a>必要な操作

ドライバーは、そのまま使用し、同じクライアントでサブスクライブしている場合でも、重複するサブスクリプションをレポートする必要があります。

-   近接ときに最初のメッセージを受信する前に、ドライバーは、仮想"DeviceArrived"メッセージを受信したかのように動作する必要があります。
-   プロバイダーが非近接中に移行するときに、仮想"DeviceDeparted"メッセージを受信した場合、ドライバーする必要があります機能します。
-   "DeviceDeparted"メッセージ MUST NOT するクライアントに配信前に、そのクライアントによって処理されたその他のすべてのメッセージ。
-   DeviceArrived メッセージのペイロードが 1 つの DWORD の高 31 ビットを 0 に設定をする必要があり、最下位ビットが直前に最初のデバイスが持続的な双方向通信できる場合にのみを設定します。

    **注**  NFC では、これは LLCP サポートに相当します。

     

-   近接になる最初のデバイスがタグの種類のデバイス (たとえば、NFC フォーラム タグ) だけの場合は、ドライバーは、DeviceArrived メッセージのペイロードの最下位ビットをクリアする必要があります。

     

-   DeviceDeparted メッセージのペイロードは、1 つの DWORD 値は 0 である必要があります。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

