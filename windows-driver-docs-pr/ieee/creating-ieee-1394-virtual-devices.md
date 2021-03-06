---
title: IEEE 1394 仮想デバイスの作成
description: IEEE 1394 仮想デバイスの作成
ms.assetid: 5b6a4d7a-e116-4a68-a1f8-fd561fbc0495
keywords:
- エミュレーション ドライバー WDK IEEE 1394 バス
- ハードウェア エミュレーション ドライバー WDK IEEE 1394 バス
- 仮想デバイス WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca131b4d21ddc06a0e3618b9ed2ad4706b988844
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385781"
---
# <a name="creating-ieee-1394-virtual-devices"></a>IEEE 1394 仮想デバイスの作成





上位レベルのドライバーとユーザー モードのサービスを追加または削除できます 1394 の仮想デバイスで、デバイス制御の要求を使用して、 [ **IOCTL\_IEEE1394\_API\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537241)コードを制御します。 要求に含まれる、 [ **IEEE1394\_API\_要求**](https://docs.microsoft.com/previous-versions/ff537204(v=vs.85))持つ**RequestNumber**メンバーは、(を実行するアクションを示します。追加または削除)、バス ドライバー。 仮想デバイスには、デバイス ID がありませんか、インスタンス ID、ドライバーまたは仮想デバイスを作成することを要求するユーザーのプログラムがあるので必要があります、デバイス ID を指定し、インスタンスの ID、 [ **IEEE1394\_VDEV\_PNP\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537206)構造体。

ときに、IEEE1394\_要求\_フラグ\_IOCTL を使用して、永続的なが指定された\_IEEE1394\_API\_要求、1394 バス ドライバーに関する不揮発性のコンテキスト情報を格納する、レジストリの仮想デバイス。 これにより、バス ドライバーを自動的に次の起動時、上位レベルのドライバーからの介入なしに仮想の PDO を再作成できます。

バス ドライバーでは、このレジストリ エントリを使用して、システム内の各 1394 デバイス スタックの仮想デバイスの「列挙」。 1394 バス ドライバーの呼び出し後、仮想デバイスの仮想の PDO を作成するには、 [ **IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)、実際のデバイス用の PDO を作成した後はこれだけです。 この呼び出しは、プラグ アンド プレイ (PnP) マネージャーで新しいデバイスが到着すると、ことを通知し、PnP マネージャーが、仮想デバイスのドライバーをロードします。

複数の 1394 のホスト コント ローラーは、システム、レジストリで定義されている仮想デバイス上に存在する 1 つが複数回列挙されます。 仮想デバイスごとに一意のインスタンス ID は、仮想デバイスを作成する上位レベルのドライバーまたはユーザーのサービスは「ハード コーディングされた」特定のインスタンスを指定する必要がありますを搭載したシステム上の仮想デバイスの ID を複数の 1 つ 1394 ホスト コント ローラー。 代わりに、上位のソフトウェアが、IEEE1394 を設定する必要があります\_要求\_フラグ\_使用\_ローカル\_ホスト\_EUI フラグ、IEEE1394\_API\_を要求します。 このフラグが設定、バス ドライバーは、デバイスを列挙します。 次に、仮想デバイスのインスタンス ID としてホスト コント ローラーのインスタンス ID を使用します。 インスタンス ID は、そのホスト コント ローラーのインスタンス ID と同じでは、仮想デバイスは一意のインスタンス ID を持ちます。 も各 1394 デバイス スタックが一意のインスタンス ID を持つホスト コント ローラーであるため、

1394 バス上の仮想デバイスを公開するためにエミュレーション ドライバーは、次の手順を使用して仮想デバイス単位ディレクトリを追加する必要があります。

1.  送信、 [**要求\_設定\_ローカル\_ホスト\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff537663)バス ドライバーへの要求**u です。SetLocalHostProperties.nLevel**セットにセットのメンバー、IRB\_ローカル\_ホスト\_プロパティ\_変更\_CROM 単位ディレクトリ、システムの IEEE を追加するには1394 構成 ROM. この要求はまた、エミュレートされたデバイスの機能を公開するために、ROM 構成にその他の必要な構成データを追加します。 エミュレーション ドライバーが関連付けられている仮想 PDO を使用して、要求を送信する必要があります。

2.  バスの bus ROM システム構成が変更された上に存在する 1394 ノードを通知するためにリセットを発行します。

 

 




